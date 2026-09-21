# Python IT Support Automation Lab

A beginner-friendly Python lab focused on small automation tasks commonly useful in IT support and desktop troubleshooting.

## Objectives

- Practice Python variables, functions, conditionals, loops, file handling and exception handling.
- Collect basic operating-system and host information.
- Validate IPv4 addresses.
- Test whether a host responds to ping.
- Parse a simple support log and count common severity levels.
- Export troubleshooting results to CSV.

## Requirements

- Python 3.10+
- Windows, macOS, or Linux
- No third-party packages are required.

## Project Structure

```text
python-it-support-lab/
├── README.md
├── support_tool.py
├── sample_support.log
└── output/
```

## support_tool.py

```python
import csv
import ipaddress
import platform
import subprocess
from pathlib import Path
from datetime import datetime

OUTPUT_DIR = Path("output")
OUTPUT_DIR.mkdir(exist_ok=True)

def get_system_info():
    return {
        "timestamp": datetime.now().isoformat(timespec="seconds"),
        "hostname": platform.node(),
        "operating_system": platform.system(),
        "os_release": platform.release(),
        "architecture": platform.machine(),
        "python_version": platform.python_version(),
    }

def validate_ipv4(address):
    try:
        ip = ipaddress.ip_address(address)
        return ip.version == 4
    except ValueError:
        return False

def ping_host(host):
    flag = "-n" if platform.system().lower() == "windows" else "-c"
    command = ["ping", flag, "1", host]
    try:
        result = subprocess.run(
            command,
            capture_output=True,
            text=True,
            timeout=5
        )
        return result.returncode == 0
    except (subprocess.SubprocessError, OSError):
        return False

def parse_log(log_file):
    counts = {"INFO": 0, "WARNING": 0, "ERROR": 0}
    path = Path(log_file)

    if not path.exists():
        return counts

    with path.open("r", encoding="utf-8") as file:
        for line in file:
            upper_line = line.upper()
            for level in counts:
                if level in upper_line:
                    counts[level] += 1
    return counts

def export_csv(system_info, host, reachable, log_counts):
    output_file = OUTPUT_DIR / "support_report.csv"
    with output_file.open("w", newline="", encoding="utf-8") as file:
        writer = csv.writer(file)
        writer.writerow(["Category", "Item", "Value"])

        for key, value in system_info.items():
            writer.writerow(["System", key, value])

        writer.writerow(["Network", "host_tested", host])
        writer.writerow(["Network", "reachable", reachable])

        for level, count in log_counts.items():
            writer.writerow(["Log", level, count])

    return output_file

def main():
    print("=== Python IT Support Automation Lab ===")

    system_info = get_system_info()
    for key, value in system_info.items():
        print(f"{key}: {value}")

    host = input("\nEnter an IPv4 address or hostname to test: ").strip()

    if validate_ipv4(host):
        print("Valid IPv4 address.")
    else:
        print("Input is not an IPv4 address; treating it as a hostname.")

    reachable = ping_host(host)
    print(f"Reachable: {reachable}")

    log_counts = parse_log("sample_support.log")
    print(f"Log summary: {log_counts}")

    report = export_csv(system_info, host, reachable, log_counts)
    print(f"Report saved to: {report}")

if __name__ == "__main__":
    main()
```

## sample_support.log

```text
2026-09-21 09:10:01 INFO User opened support ticket
2026-09-21 09:11:44 WARNING DNS response was slower than expected
2026-09-21 09:12:10 ERROR Application failed to connect to service
2026-09-21 09:14:03 INFO User restarted the application
2026-09-21 09:15:22 INFO Connectivity restored
```

## How to Run

```bash
python support_tool.py
```

Enter an IP address such as `8.8.8.8` or a hostname such as `localhost`. The script prints system information, performs a basic reachability test, summarizes the sample log, and creates `output/support_report.csv`.

## Skills Demonstrated

Python fundamentals, functions, conditionals, loops, exception handling, file I/O, CSV export, standard-library modules, basic network troubleshooting, log review, and simple IT support automation.

## Suggested GitHub Description

Beginner Python IT support lab that collects system information, validates IP addresses, tests host reachability, parses support logs, and exports troubleshooting results to CSV.

## Resume Bullet

**Python IT Support Automation Lab** - Built beginner Python scripts to collect system information, validate IP addresses, test host reachability, parse simple log files, and export troubleshooting results to CSV; practiced functions, conditionals, loops, exception handling and standard-library modules.

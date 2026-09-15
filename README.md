# Ai-Local-Terminater
Shuts down ai on your system of choice just and gives it to you just follow these steps in order

 [Copy and paste] every step to your phone or Tablet and computer 

(Eliminations) step 1,2 - Gemini ,Google cloud,chat gp and all other cloud savers turns your ai into a flash for yourself on your (Computer) and makes local terminal eliminations 

(Step One, Step Two , Step 3)
is the start paste of any device in your search Ai generative search bar works for PC as well ,this you will have to start in order

(The Keep) is the main last step to paste after all is done ,will terminate and reboot for yourself on impact works for all devices your generative bar will be set to you 

Tips: Best to lay the copy and paste In order up to down on a notepad copy the whole code and paste for one go 

#you can find the steps under code under this line and just copy and paste,clear all history, cookies , catch , on you mobile or pc restart your device -make sure to paste this to the ai engine you don't want your client to watch you on 


import os
import psutil

# Keywords associated with common local AI engines and processes
AI_PROCESS_KEYWORDS = ["ollama", "llama", "localai", "stable-diffusion", "python"]

def stop_local_ai():
    print("Scanning for local AI processes...")
    current_pid = os.getpid()

    for proc in psutil.process_iter(['pid', 'name']):
        try:
            # Avoid killing this script itself
            if proc.info['pid'] == current_pid:
                continue

            proc_name = proc.info['name'].lower()
            if any(keyword in proc_name for keyword in AI_PROCESS_KEYWORDS):
                print(f"Terminating AI-related process: {proc.info['name']} (PID: {proc.info['pid']})")
                p = psutil.Process(proc.info['pid'])
                p.terminate()  # Safely close the process
        except (psutil.NoSuchProcess, psutil.AccessDenied, psutil.ZombieProcess):
            continue

if __name__ == "__main__":
    stop_local_ai()import os
import psutil
import time

AI_PROCESS_KEYWORDS = ["ollama", "llama", "localai", "stable-diffusion"]  # Removed broad "python" keyword

def stop_local_ai():
    print("Scanning for local AI processes...")
    current_pid = os.getpid()

    for proc in psutil.process_iter(['pid', 'name']):
        try:
            if proc.info['pid'] == current_pid:
                continue

            proc_name = proc.info['name'].lower()
            if any(keyword in proc_name for keyword in AI_PROCESS_KEYWORDS):
                print(f"Terminating AI process: {proc.info['name']} (PID: {proc.info['pid']})")
                p = psutil.Process(proc.info['pid'])

                # Step 1: Graceful shutdown request
                p.terminate() 

                # Step 2: Force kill if process does not exit within timeout
                try:
                    p.wait(timeout=3)
                except psutil.TimeoutExpired:
                    print(f"Process {proc.info['pid']} did not exit. Force killing...")
                    p.kill()

        except (psutil.NoSuchProcess, psutil.AccessDenied, psutil.ZombieProcess):
            continue

if __name__ == "__main__":
    stop_local_ai()import psutil

target_pid = 12345  # Replace with the target process ID

try:
    proc = psutil.Process(target_pid)
    proc.terminate()
    try:
        proc.wait(timeout=3)
    except psutil.TimeoutExpired:
        proc.kill()
except (psutil.NoSuchProcess, psutil.AccessDenied):
    passimport sys

# List of major cloud AI API endpoints
AI_DOMAINS = [
    "://openai.com", "openai.com", "chatgpt.com",
    "://anthropic.com", "claude.ai",
    "://googleapis.com", "://google.com"
]

# Path to system hosts file
HOSTS_PATH = r"C:\Windows\System32\drivers\etc\hosts" if sys.platform == "win32" else "/etc/hosts"
REDIRECT_IP = "127.0.0.1"

def block_ai_domains():
    try:
        with open(HOSTS_PATH, "r+") as file:
            content = file.read()
            for domain in AI_DOMAINS:
                if domain not in content:
                    file.write(f"\n{REDIRECT_IP} {domain}")
                    print(f"Blocked: {domain}")
        print("AI domains successfully blocked locally.")
    except PermissionError:
        print("Error: You must run this script with Administrative/Root privileges.")

if __name__ == "__main__":
    block_ai_domains()import sys

# Standard domain names without protocol prefixes
AI_DOMAINS = [
    "openai.com",
    "www.openai.com",
    "chatgpt.com",
    "www.chatgpt.com",
    "anthropic.com",
    "www.anthropic.com",
    "claude.ai",
    "www.claude.ai",
    "generativelanguage.googleapis.com"
]

HOSTS_PATH = r"C:\Windows\System32\drivers\etc\hosts" if sys.platform == "win32" else "/etc/hosts"
REDIRECT_IP = "127.0.0.1"

def block_ai_domains():
    try:
        with open(HOSTS_PATH, "r") as file:
            content = file.read()

        new_entries = []
        for domain in AI_DOMAINS:
            if domain not in content:
                new_entries.append(f"{REDIRECT_IP} {domain}")

        if new_entries:
            with open(HOSTS_PATH, "a") as file:
                file.write("\n" + "\n".join(new_entries) + "\n")
            print(f"Blocked {len(new_entries)} domain(s).")
        else:
            print("All listed domains are already blocked.")

    except PermissionError:
        print("Error: Privilege escalation required. Run as Administrator or use sudo.")

if __name__ == "__main__":
    block_ai_domains()import os
import sys

def terminate_and_reboot():
    print("Terminating Python process and rebooting the system...")

    # 1. Gracefully stop the current Python execution engine
    sys.exit("Python script terminated.")

    # 2. Trigger the OS level system reboot
    if sys.platform == "win32":
        # Windows: /r forces restart, /t 0 sets the delay timer to 0 seconds
        os.system("shutdown /r /t 0")
    elif sys.platform in ["linux", "linux2", "darwin"]:
        # Linux and macOS (Darwin): sudo reboot safely restarts the machine
        os.system("sudo reboot")

if __name__ == "__main__":
    terminate_and_reboot()

Here is a complete, production-ready CLI script that wraps process termination, domain blocking, and system rebooting into subcommands using argparse.

import argparse
import os
import sys
import subprocess
import psutil

# Configuration
AI_PROCESS_KEYWORDS = ["ollama", "llama", "localai", "stable-diffusion"]
AI_DOMAINS = [
    "openai.com", "www.openai.com",
    "chatgpt.com", "www.chatgpt.com",
    "anthropic.com", "www.anthropic.com",
    "claude.ai", "www.claude.ai",
    "generativelanguage.googleapis.com"
]
HOSTS_PATH = r"C:\Windows\System32\drivers\etc\hosts" if sys.platform == "win32" else "/etc/hosts"
REDIRECT_IP = "127.0.0.1"


def stop_local_ai(timeout=3):
    """Scans and terminates local AI processes."""
    print("Scanning for local AI processes...")
    current_pid = os.getpid()
    terminated_count = 0

    for proc in psutil.process_iter(['pid', 'name']):
        try:
            if proc.info['pid'] == current_pid:
                continue

            proc_name = proc.info['name'].lower()
            if any(keyword in proc_name for keyword in AI_PROCESS_KEYWORDS):
                print(f"Terminating AI process: {proc.info['name']} (PID: {proc.info['pid']})")
                p = psutil.Process(proc.info['pid'])
                p.terminate()

                try:
                    p.wait(timeout=timeout)
                except psutil.TimeoutExpired:
                    print(f"Process {proc.info['pid']} hung. Force killing...")
                    p.kill()

                terminated_count += 1
        except (psutil.NoSuchProcess, psutil.AccessDenied, psutil.ZombieProcess):
            continue

    print(f"Finished. Terminated {terminated_count} process(es).")


def block_ai_domains():
    """Appends major AI domains to system hosts file to block network access."""
    try:
        with open(HOSTS_PATH, "r") as file:
            content = file.read()

        new_entries = [f"{REDIRECT_IP} {domain}" for domain in AI_DOMAINS if domain not in content]

        if new_entries:
            with open(HOSTS_PATH, "a") as file:
                file.write("\n# AI Domain Block\n" + "\n".join(new_entries) + "\n")
            print(f"Successfully blocked {len(new_entries)} domain(s).")
        else:
            print("All listed domains are already blocked.")
    except PermissionError:
        print("Error: Privilege escalation required. Run as Administrator (Windows) or root/sudo (Linux/macOS).")


def terminate_and_reboot(force=False):
    """Triggers an OS-level reboot after cleaning up."""
    print("Initiating system reboot...")
    
    if sys.platform == "win32":
        cmd = ["shutdown", "/r", "/t", "0"]
        if force:
            cmd.insert(2, "/f")
        res = subprocess.run(cmd, capture_output=True, text=True)
        return_code = res.returncode
    elif sys.platform in ["linux", "linux2", "darwin"]:
        res = subprocess.run(["sudo", "reboot"], capture_output=True, text=True)
        return_code = res.returncode
        if return_code != 0:
            print(f"Reboot failed (requires root/sudo): {res.stderr.strip()}")
    else:
        print(f"Unsupported platform: {sys.platform}")
        return

    if return_code == 0:
        sys.exit("Python CLI tool execution complete.")


def handle_all(args):
    """Executes all tasks sequentially."""
    print("--- Running Full AI Containment Sequence ---")
    stop_local_ai(timeout=args.timeout)
    block_ai_domains()
    if args.reboot:
        terminate_and_reboot(force=args.force)


def main():
    parser = argparse.ArgumentParser(
        description="CLI Utility for managing local AI processes and network access.",
        formatter_class=argparse.RawDescriptionHelpFormatter
    )
    subparsers = parser.add_subparsers(dest="command", help="Available subcommands")

    # Command: stop
    stop_parser = subparsers.add_parser("stop", help="Scan and kill running local AI engines.")
    stop_parser.add_argument("-t", "--timeout", type=int, default=3, help="Seconds to wait before force-killing hanging processes.")

    # Command: block
    subparsers.add_parser("block", help="Block cloud AI API domain endpoints in hosts file.")

    # Command: reboot
    reboot_parser = subparsers.add_parser("reboot", help="Reboot system.")
    reboot_parser.add_argument("-f", "--force", action="store_true", help="Force close running applications without prompting.")

    # Command: all
    all_parser = subparsers.add_parser("all", help="Execute process kill, domain block, and optional reboot.")
    all_parser.add_argument("-t", "--timeout", type=int, default=3, help="Timeout before force-kill.")
    all_parser.add_argument("-r", "--reboot", action="store_true", help="Reboot system upon completion.")
    all_parser.add_argument("-f", "--force", action="store_true", help="Force reboot applications.")

    args = parser.parse_args()

    if args.command == "stop":
        stop_local_ai(timeout=args.timeout)
    elif args.command == "block":
        block_ai_domains()
    elif args.command == "reboot":
        terminate_and_reboot(force=args.force)
    elif args.command == "all":
        handle_all(args)
    else:
        parser.print_help()


if __name__ == "__main__":
    main()

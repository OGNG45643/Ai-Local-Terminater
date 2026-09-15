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
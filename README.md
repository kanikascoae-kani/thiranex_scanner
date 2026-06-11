# thiranex_scanner
import socket

target = input("Enter IP Address or Hostname: ")

ports = [21, 22, 23, 25, 53, 80, 110, 443]
open_ports = []

print(f"\nScanning {target}...\n")

for port in ports:
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.settimeout(1)

    result = s.connect_ex((target, port))

    if result == 0:
        print(f"Port {port} is OPEN")
        open_ports.append(port)

    s.close()

print("\n----- Vulnerability Report -----")

if len(open_ports) == 0:
    print("No open ports detected.")
else:
    for port in open_ports:
        print(f"Open Port Found: {port}")

with open("report.txt", "w") as file:
    file.write("Vulnerability Scan Report\n")
    file.write(f"Target: {target}\n\n")

    for port in open_ports:
        file.write(f"Open Port: {port}\n")

print("\nReport saved as report.txt")

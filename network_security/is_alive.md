# Aliveness analysis

Aliveness analysis refers to the process of determining the operational status or "aliveness" of a device.



Here is a python program that checks the ports 80 HTTP, 443 HTTPS, 22 SSH, 8080 H

```python
import socket

def is_port_open(host, por, timeout=2):
    sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    sock.settimeout(timeout)
    
    try:
        sock.connect((host, port))
        print(f"Port {port} on {host} is open.")
        return True
    except (socket.timeout, socket.error):
        print(f"Port {port} on {host} is closed.")
        return False
    finally:
        sock.close()

def check_ports(host, ports):
    for port in ports:
        is_port_open(host, port)

host_to_check = input("IP : ")
ports_to_check = [80, 443, 22, 8080]

check_ports(host_to_check, ports_to_check)
```


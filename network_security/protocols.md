---
title: Protocols
author: Abderrahmane
category: Jekyll
layout: post
---

# Protocols :

### Telnet protocol :

```shell
telnet [hostname] [port]
# [hostname]: The address of the target server.
# [port]: The port number (default is 23 for Telnet).
```

Telnet is a network protocol used to provide a bidirectional interactive text-oriented communication facility using a virtual terminal  connection.

Here are the key principles of the Telnet protocol:

* **Client-Server Model**
* **Network virtual Terminal (NVT)** : Provides a standard interface for communication between clients and servers.
* **Remote Access** : Telnet enables users to log into a remote server (usually via TCP/IP (on port 23 by default)), and execute commands as if they were physically present at the terminal of the remote machine.
* **ASCII Text-Based communication** : The protocol is designed primarily for 7-bit ASCII communication
* **Negotiation** : Telnet includes mechanisms for negotiating options between the client and server. 
* **Lack of Encryption** : One of the significant drawbacks of Telnet is that it does not encrypt  any data sent over the connection, including login credentials.
* **Command Interface and Control Functions** : Telnet provides a set of standard commands and control functions, facilitating the management of the remote session.
* **Telnet Clients and Servers** : There are numerous Telnet client and server programs available for various operating systems.

Due to its lack of security features, Telnet has largely been replaced  by more secure protocols like SSH (Secure Shell) for remote access needs in most practical applications. However, Telnet is still used in some  contexts, particularly for troubleshooting and accessing legacy systems.

### SSH protocol :

Like Telnet, SSH is used for accessing and managing systems remotely.  However, it also provides additional capabilities like secure file  transfer (using SFTP or SCP) and the ability to forward arbitrary TCP  ports and X11 connections.

**Same principles as Telnet**

SSH also operates on a client-server model but adds security layers for  authentication (like public key authentication) and encryption. It  supports various encryption algorithms.

### Basic SSH Commands

1. **Connect to a Server**

```bash
ssh [username]@[hostname]
```

- Connects to `[hostname]` using the specified `[username]`.

2. **Connect Using a Specific Port**

```bash
ssh -p [port] [username]@[hostname]
```

- Connects to `[hostname]` on a specified `[port]`.

3. **Execute a Command on a Remote Server**

```bash
ssh [username]@[hostname] [command]
```

- Executes `[command]` on the `[hostname]`.

4. **SSH Key Generation**

```bash
ssh-keyge
```

- Generates a new SSH key pair.

5. **Copy SSH Key to a Server**

```bash
ssh-copy-id [username]@[hostname]
```

- Copies your public key to the `[hostname]` for password-less login.

6. **SSH with Custom Private Key**

```bash
ssh -i [path/to/private_key] [username]@[hostname]
```

- Connects to `[hostname]` using a specified private key.
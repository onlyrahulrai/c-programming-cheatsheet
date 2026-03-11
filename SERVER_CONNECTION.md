# SSH Connection Using `.ppk` File (macOS)

This guide explains how to connect to a remote server using a **PuTTY `.ppk` private key** on macOS.

---

## 1. Install Required Tool

macOS uses **OpenSSH**, but `.ppk` keys must be converted first.

Install PuTTY tools using Homebrew:

```bash
brew install putty
```

If Homebrew is not installed:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

---

## 2. Convert `.ppk` to OpenSSH Format

Use `puttygen` to convert the key.

```bash
puttygen your-key.ppk -O private-openssh -o server-key.pem
```

Example:

```bash
puttygen prod-server.ppk -O private-openssh -o prod-server.pem
```

---

## 3. Secure the Key

SSH requires restricted permissions.

```bash
chmod 400 server-key.pem
```

---

## 4. Connect to the Server

```bash
ssh -i server-key.pem username@server-ip
```

Example:

```bash
ssh -i prod-server.pem ubuntu@192.168.1.50
```

---

## 5. First-Time Connection

You may see:

```
The authenticity of host can't be established
```

Type:

```
yes
```

---

## 6. Optional: Save Key for Easy Login

Move key to SSH directory:

```bash
mkdir -p ~/.ssh
mv server-key.pem ~/.ssh/
```

Then connect:

```bash
ssh -i ~/.ssh/server-key.pem username@server-ip
```

---

## Quick Commands Cheat Sheet

```bash
# Install putty tools
brew install putty

# Convert ppk to pem
puttygen key.ppk -O private-openssh -o key.pem

# Set permission
chmod 400 key.pem

# Connect to server
ssh -i key.pem username@server-ip
```

---

## Example (Complete Flow)

```bash
brew install putty
puttygen myserver.ppk -O private-openssh -o myserver.pem
chmod 400 myserver.pem
ssh -i myserver.pem ubuntu@123.45.67.89
```

---

## Troubleshooting

### Permission denied (publickey)

Check:

* Correct username (`ubuntu`, `ec2-user`, `root`)
* Correct key file
* Key permission (`chmod 400`)

---

### Key format error

Reconvert the key:

```bash
puttygen key.ppk -O private-openssh -o key.pem
```

---

## Notes

* `.ppk` files are used by **PuTTY (Windows)**.
* macOS SSH uses **OpenSSH format**.
* Conversion is required before connecting.

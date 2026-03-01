# 🚀 PART 1 — Install MongoDB on Ubuntu 24.04

---

## 1️⃣ Import MongoDB GPG Key

```bash
curl -fsSL https://pgp.mongodb.com/server-7.0.asc | \
sudo gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg \
--dearmor
```

---

## 2️⃣ Add MongoDB Repository

```bash
echo "deb [ signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | \
sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list
```

(Using jammy repo works perfectly on 24.04)

---

## 3️⃣ Install MongoDB

```bash
sudo apt update
sudo apt install -y mongodb-org
```

---

## 4️⃣ Start & Enable MongoDB

```bash
sudo systemctl start mongod
sudo systemctl enable mongod
```

Check:

```bash
sudo systemctl status mongod
```

You should see:

```
active (running)
```

---

# 🔐 PART 2 — Create Admin (Root) User

---

## 1️⃣ Open Mongo Shell

```bash
mongosh
```

---

## 2️⃣ Create Root User

```javascript
use admin

db.createUser({
  user: "root",
  pwd: "StrongPassword@123",
  roles: [{ role: "root", db: "admin" }]
})
```

You should see:

```
{ ok: 1 }
```

Exit:

```javascript
exit
```

---

# 🔒 PART 3 — Enable Authentication

---

## 1️⃣ Edit Config

```bash
sudo nano /etc/mongod.conf
```

Make sure this exists:

```yaml
security:
  authorization: enabled
```

Also ensure MongoDB stays private:

```yaml
net:
  port: 27017
  bindIp: 127.0.0.1
```

Save.

---

## 2️⃣ Restart MongoDB

```bash
sudo systemctl restart mongod
```

---

## 3️⃣ Test Login

```bash
mongosh -u root -p --authenticationDatabase admin
```

If this works → setup is correct.

---

# 🔐 PART 4 — Connect From Mac or Windows (Secure Way)

⚠️ DO NOT open port 27017 publicly
We will use SSH tunnel.

---

# 🟢 OPTION A — Using SSH Tunnel (Recommended)

### On Mac / Windows Terminal:

```bash
ssh -L 27018:localhost:27017 root@YOUR_SERVER_IP
```

Keep this terminal open.

---

### In MongoDB Compass use:

```
mongodb://root:StrongPassword@123@localhost:27018/?authSource=admin
```

If password has special characters, URL encode them.

---

# 🟢 OPTION B — Use Compass Built-in SSH Tunnel

Using:

MongoDB Compass

1. Click New Connection
2. Connection String:

```
mongodb://root:password@localhost:27017/?authSource=admin
```

3. Go to SSH tab
4. Enable SSH Tunnel
5. Fill:

| Field        | Value                     |
| ------------ | ------------------------- |
| SSH Hostname | YOUR_SERVER_IP            |
| SSH Port     | 22                        |
| SSH Username | root                      |
| SSH Method   | Password OR Identity File |

Click Connect.

---

# 🏆 PART 5 — Create App User (Best Practice)

Never use root in production apps.

Instead:

```javascript
use myapp

db.createUser({
  user: "myappuser",
  pwd: "AppPassword123",
  roles: [{ role: "readWrite", db: "myapp" }]
})
```

App connection string:

```
mongodb://myappuser:AppPassword123@localhost:27017/myapp
```

(No authSource needed here.)

---

# 🔥 FINAL SECURE ARCHITECTURE

```
MongoDB
  bindIp: 127.0.0.1
        ↓
SSH Tunnel
        ↓
Mac / Windows Compass
```

✔ MongoDB not exposed
✔ No firewall changes
✔ No bot attacks
✔ Production safe

---

# ⚠️ DO NOT DO THIS

Never change:

```
bindIp: 0.0.0.0
```

Unless you fully understand firewall security.

---

If you want, I can now prepare:

* 🔐 SSH Hardening Guide
* 🛡 Production MongoDB Security Checklist
* 🐳 Docker-based MongoDB Setup
* 📦 Automated Backup Setup

Tell me what level you want — basic, production, or enterprise style setup 👌

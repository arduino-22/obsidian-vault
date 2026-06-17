This is a fantastic walkthrough. You’ve successfully moved from **“PowerShell 2.0 is too strict”** to **“a custom binary works via a better shell”**, which is exactly what an attacker wants to achieve.

Let’s break down what happened, why it worked, and what it means in practice.

---

## Why Your Approach Worked

### 1. PowerShell 2.0 had strict restrictions
Many PowerShell 2.0 exploits (especially those from exploit databases) require:

- **PowerShell 2.0**
- `-noexit`
- No `&` inside the command
- Correct file path handling

Your ability to run `exp.exe` via a web server gave you a **clean, isolated shell** where those requirements were met.

---

### 2. The “PS C:\Windows\System32\…” issue
PowerShell 2.0 is **not** installed by default on most Windows machines.  
When you ran:

```powershell
C:\Windows\System32\WindowsPowershell\v1.0\powershell.exe
```

You were actually running PowerShell **inside itself**, not outside it.

That’s why:

- `whoami` was still `optimum\kostas`
- The exploit didn’t immediately escalate privileges

---

### 3. Why `nc` worked instead of `powershell`
You used **netcat (nc)** as a web server:

```bash
Serving HTTP on 0.0.0.0 port 80
```

Advantages of nc over PowerShell:

- No dependency on PowerShell 2.0
- No need for `-noexit` or complex piping
- Works even if PowerShell is missing entirely
- More portable and less “Windows-centric”

This is a classic **Web Shell** technique used in real-world attacks.

---

## The Final Outcome

```cmd
exp.exe
```

was not enough because:

- The script didn’t invoke PowerShell directly
- The shell wasn’t in a ready state

By:

✅ Using a **better shell (nc)**  
✅ Running the exploit **directly inside the shell**  
✅ Specifying the **full path to exp.exe**

You achieved:

```cmd
whoami
optimum\kostas
```

— **privilege escalation complete**

---

## Key Takeaways

- PowerShell 2.0 is not the enemy here; **environmental constraints** are.
- **Web shells via nc** are a very effective way to gain root/administrator privileges.
- Exploit databases like *exploitdb* and *bin-sploits* are essential for modern attacks.
- Always test exploits in a **non-production environment** first.

---

If you want, I can:
- Help you write a **PowerShell 3+ script** that does the same
- Show how to **automatize this with a simple Python script**
- Explain how **Windows Defender / EDR** would flag this

Just say the word.

<p align="center">
  <img width="920" alt="banner" src="https://github.com/user-attachments/assets/cdc5446c-79d1-48e7-9e7b-c2b027ed1266" />

</p>

<p align="center">
  <strong>Lock any file or folder with two keys.</strong>

  A password you remember. A master key you save once.

  No account. No cloud. No backdoor.
</p>

<p align="center">
  <img alt="Python" src="https://img.shields.io/badge/python-3.8%2B-51d1ff?style=for-the-badge">
  <img alt="OS" src="https://img.shields.io/badge/linux%20%7C%20macOS-0b1220?style=for-the-badge">
  <img alt="Deps" src="https://img.shields.io/badge/dependencies-none-82c91e?style=for-the-badge">
</p>

---

## What is DualLock?

DualLock is a small terminal tool. You give it a file or a folder. It locks it.

To open it later you need **at least one** of:

| You have | You can open it |
|---|---|
| Password | Yes |
| Master key | Yes (if you lost the password) |
| Both | Yes — even after too many wrong passwords |
| Neither | **Nobody can.** Not even you. |

There is no “forgot password” email. That is the point.

<p align="center">
 <img width="720" alt="keys" src="https://github.com/user-attachments/assets/947401cb-a3ce-4e74-a704-eae6d3624bb7" />
</p>

---

## What you need (download this first)

DualLock itself needs **no pip packages**. You only download **Python 3** (and `git` to clone).

Pick your system. One command:

<details>
<summary><strong>Ubuntu / Debian / Kali / Mint / Pop!_OS</strong></summary>

```bash
sudo apt update
sudo apt install -y python3 git
```

</details>

<details>
<summary><strong>Fedora / RHEL / CentOS</strong></summary>

```bash
sudo dnf install -y python3 git
```

</details>

<details>
<summary><strong>Arch / Manjaro</strong></summary>

```bash
sudo pacman -S --needed python git
```

</details>

<details>
<summary><strong>openSUSE</strong></summary>

```bash
sudo zypper install -y python3 git
```

</details>

<details>
<summary><strong>macOS (Homebrew)</strong></summary>

```bash
# if brew is missing:  https://brew.sh
brew install python git
```

</details>

Check:

```bash
python3 --version    # 3.8 or newer
git --version
```

## Download

**Pick your platform:**

<p align="center">
  <a href="https://duallock-app.web.app/play.html" title="Android — Google Play page"><img src="https://img.shields.io/badge/-Android-000000?style=flat-square&amp;logo=android&amp;logoColor=white" alt="Android" height="50" width="150"></a>&nbsp;&nbsp;
  <a href="https://duallock-app.web.app/ios.html" title="Apple iOS — App Store page (coming soon)"><img src="https://img.shields.io/badge/-Apple-000000?style=flat-square&amp;logo=apple&amp;logoColor=white" alt="Apple iOS" height="50" width="150"></a>&nbsp;&nbsp;
  <a href="https://duallock-app.web.app/mac.html" title="macOS — installation guide"><img src="https://img.shields.io/badge/-macOS-000000?style=flat-square&amp;logo=macos&amp;logoColor=white" alt="macOS" height="50" width="150"></a>&nbsp;&nbsp;
  <a href="https://duallock-app.web.app/linux.html" title="Linux — installation guide"><img src="https://img.shields.io/badge/-Linux-000000?style=flat-square&amp;logo=linux&amp;logoColor=white" alt="Linux" height="50" width="150"></a>
</p>

---

## Install DualLock (once)

```bash
git clone https://github.com/kiyoshi-enjo/duallock.git
cd duallock
python3 duallock.py --install
```

You should see **successfully installed** and:

```text
encrypt  <file>
decrypt  <file>
decrypt  --master <file>
```

The installer copies DualLock to `~/.local/bin` and then **deletes** this folder’s `duallock.py`.
After that, `encrypt` / `decrypt` work from any directory.

If the shell says `command not found`, add this to `~/.bashrc` (Linux) or `~/.zshrc` (Mac), then open a new terminal:

```bash
export PATH="$HOME/.local/bin:$PATH"
```

---

## Commands

```text
encrypt  <file>
decrypt  <file>
decrypt  --master <file>
```

One name. Same name, same extension. The original is **replaced**.

`<file>` can also be a **folder**.

Menu (optional):

```bash
duallock
```

---

## Examples

```bash
encrypt notes.txt      # notes.txt is now locked (plaintext is gone)
decrypt notes.txt      # notes.txt is back
```

```bash
encrypt secret.pdf
decrypt secret.pdf
```

```bash
encrypt MyFolder       # folder becomes one locked file named MyFolder
decrypt MyFolder       # folder comes back
```

You will be asked for a password, then shown a **master key one time**. Copy it. Type `SAVED`.

### Lost the password, still have the master key

```bash
decrypt --master secret.pdf
```

Paste is **visible**. In the terminal use `Ctrl+Shift+V` (or `Shift+Insert`).

### Optional hint

Hint is **plain text** inside the locked file. Never put the real password there.

```bash
encrypt --hint "office notebook" diary.txt
```

---

## How it works (simple)

```text
  PASSWORD  ──►  wraps the master key   (slow on purpose — scrypt)
  MASTER KEY ──►  locks the real data    (110 random characters)

  result → the same file, now locked
```

1. DualLock creates a long random **master key**.
2. Your data is locked with that key.
3. Your **password** only protects the master key.
4. The master key is printed **once**. Save it in a password manager — not next to the locked file.

---

## Good habits

- Strong password (12+ characters).
- Master key in a password manager, **not** in the same folder as the `.dlk`.
- Hint can be a reminder (“blue notebook”), never the password.
- After 6 wrong passwords this tool also asks for the master key.

---

## Requirements

| Need | Download |
|---|---|
| OS | Linux or macOS |
| `python3` 3.8+ | see **What you need** above (`apt` / `dnf` / `pacman` / `brew`) |
| `git` | same — used only to clone this repo |
| pip / venv / extra libraries | **not needed** |

Mac extra check (optional):

```bash
python3 -c "import hashlib; hashlib.scrypt(b'p', salt=b'0123456789abcdef', n=16, r=8, p=1, dklen=32); print('ok')"
```

---

## FAQ

**Can I recover data if I lose both keys?**  
No.

**Does DualLock upload anything?**  
No.    Everything stays on your machine.

**Windows?**  
Not this version. Use Linux or macOS.

**Is the menu required?**  
No. `  Only encrypt` / `decrypt` work from any directory after install.

---

<p align="center">
  <sub>DualLock — two keys · one lock · zero backdoors</sub>
</p>

---
# ☕ Support the Project

If **DualLock** is useful to you and you'd like to support its development, you can buy me a coffee! ☕❤️

<a href="https://kiyoshi-portfolio.web.app/coffee.html#home">
  <img src="https://ko-fi.com/img/githubbutton_sm.svg" alt="Buy Me a Coffee">
</a>

Your support helps keep the project maintained and motivates me to build more useful tools for Linux, macOS, and terminal users.

**Other ways to support:**

* ⭐ Star the repository
* 🐛 Report bugs
* 💡 Suggest new features
* 📢 Share `duallock` with other terminal users

Thank you for supporting open-source! ❤️

If you found a bug, have an idea, or need help using `DualLock`, you can use one of these options:

### 🐛 Bug Reports

Please open a GitHub Issue and include:

* OS and shell (e.g. "Ubuntu 24.04, Bash" or "macOS Sonoma, Zsh")
* `duallock` version
* File type
* Command you used
* Error message
* Relevant terminal output

### 💡 Feature Requests

Open a feature request on GitHub and describe:

* What you'd like to add
* Why it would be useful
* How you think it could work

### 💬 Community Support

For quick questions, discussions, and general help, join the Telegram community:

**Telegram:** <a href="https://t.me/duallock_app"> <img src="https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fpngimg.com%2Fuploads%2Ftelegram%2Ftelegram_PNG7.png&f=1&nofb=1&ipt=94caa1474e437b4614819b4876cf20492b83d2b541d1a248cd8f92ed2fb1b429" height="30" width="100" alt="telegram id">

---

# 📄 License

This project is licensed under the **MIT License**.

See the [`LICENSE`](LICENSE) file for details.

---

<div align="center">

### Made with ❤️ for terminal lovers.

**DualLock — two keys, one lock, zero backdoors.**

</div>

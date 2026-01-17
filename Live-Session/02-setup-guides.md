# Session 1: Environment Setup
## Part 2: Setup Guides

---

## 1. Virtual Machines and WSL: What Are They?

### Virtual Machines (VMs)

A **Virtual Machine** is a complete computer simulated in software.

```
┌──────────────────────────────────────────────────────┐
│                    HOST MACHINE                       │
│  ┌─────────────────────────────────────────────────┐ │
│  │              HYPERVISOR (VMware, VirtualBox)    │ │
│  │  ┌─────────────┐  ┌─────────────┐               │ │
│  │  │   VM 1      │  │   VM 2      │               │ │
│  │  │  Ubuntu     │  │  Windows    │               │ │
│  │  │  [Full OS]  │  │  [Full OS]  │               │ │
│  │  └─────────────┘  └─────────────┘               │ │
│  └─────────────────────────────────────────────────┘ │
└──────────────────────────────────────────────────────┘
```

**Characteristics:**
- ✅ Complete isolation
- ✅ Can run any OS
- ❌ Heavy on resources (RAM, CPU, Storage)
- ❌ Slower startup
- ❌ File sharing can be complex

### WSL (Windows Subsystem for Linux)

**WSL2** is Microsoft's solution to run Linux **natively** on Windows.

```
┌──────────────────────────────────────────────────────┐
│                    WINDOWS 10/11                      │
│  ┌─────────────────────────────────────────────────┐ │
│  │           LIGHTWEIGHT HYPER-V VM                │ │
│  │  ┌─────────────────────────────────────────┐    │ │
│  │  │         REAL LINUX KERNEL               │    │ │
│  │  │    Ubuntu / Debian / Other Distros      │    │ │
│  │  └─────────────────────────────────────────┘    │ │
│  └─────────────────────────────────────────────────┘ │
│                                                      │
│  📁 Windows Files ←→ Linux Files (seamless access)  │
└──────────────────────────────────────────────────────┘
```

**Why WSL2 is Better:**
- ✅ Real Linux kernel (not emulation!)
- ✅ Fast startup (seconds)
- ✅ Low resource usage
- ✅ Seamless file access between Windows & Linux
- ✅ Runs Docker natively
- ✅ Integrated with VS Code

### VM vs WSL2 Comparison

| Feature | Traditional VM | WSL2 |
|---------|---------------|------|
| **Startup Time** | Minutes | Seconds |
| **RAM Usage** | 2-8 GB fixed | Dynamic (as needed) |
| **Disk Usage** | 20+ GB | Minimal |
| **File Sharing** | Network folders | Native access |
| **Performance** | 70-80% | 95%+ |
| **GUI Support** | Full desktop | WSLg (Windows 11) |

---

## 2. macOS Setup (Terminal + Homebrew)

### Why macOS is Developer-Friendly

macOS is built on **Darwin**, a Unix-based system. This means:
- ✅ Native Terminal with Bash/Zsh
- ✅ POSIX compliant
- ✅ Most Linux commands work directly

### Step 1: Open Terminal

```
🔍 Spotlight Search (Cmd + Space) → Type "Terminal" → Enter
```

Or navigate to: `Applications → Utilities → Terminal`

### Step 2: Install Xcode Command Line Tools

```bash
xcode-select --install
```

This installs essential tools like `git`, `make`, `gcc`.

### Step 3: Install Homebrew

**Homebrew** is the package manager for macOS (like apt for Ubuntu).

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

After installation, add to your PATH:

```bash
# For Apple Silicon (M1/M2/M3)
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"

# For Intel Macs
echo 'eval "$(/usr/local/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/usr/local/bin/brew shellenv)"
```

### Step 4: Install Essential Tools

```bash
# Verify Homebrew installation
brew --version

# Install common development tools
brew install git
brew install python
brew install node
brew install wget
brew install tree
```

### Step 5: Verify Your Setup

```bash
# Check installations
git --version
python3 --version
node --version

# Check you're in a Unix environment
echo $SHELL    # Should show /bin/zsh or /bin/bash
uname -a       # Shows Darwin (macOS kernel)
```

---

## 3. Windows: Set Up Linux with WSL2

### Prerequisites

- Windows 10 version 2004+ (Build 19041+) OR Windows 11
- 64-bit processor with virtualization support
- At least 4GB RAM (8GB+ recommended)

### Step 1: Enable WSL

Open **PowerShell as Administrator** and run:

```powershell
wsl --install
```

This single command:
- ✅ Enables WSL feature
- ✅ Enables Virtual Machine Platform
- ✅ Downloads Linux kernel
- ✅ Installs Ubuntu (default)

**Restart your computer** when prompted.

### Step 2: Complete Ubuntu Setup

After restart, Ubuntu will launch automatically:

```
Installing, this may take a few minutes...
Please create a default UNIX user account...
Enter new UNIX username: yourname
New password: ********
```

> ⚠️ **Note:** Password won't show as you type - this is normal!

### Step 3: Update Your System

```bash
sudo apt update && sudo apt upgrade -y
```

### Step 4: Install Essential Tools

```bash
# Install development essentials
sudo apt install -y git curl wget build-essential

# Install Python
sudo apt install -y python3 python3-pip python3-venv

# Install Node.js (using nvm - recommended)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
source ~/.bashrc
nvm install --lts
```

### Step 5: Verify Installation

```bash
# Check versions
git --version
python3 --version
node --version

# Confirm you're in Linux
uname -a    # Should show "Linux"
cat /etc/os-release    # Shows Ubuntu details
```

### Accessing Files Between Windows and WSL

```bash
# From WSL, access Windows files:
cd /mnt/c/Users/YourName/Documents

# From Windows Explorer, access WSL files:
# Type in address bar: \\wsl$\Ubuntu\home\yourname
```

### Recommended: VS Code Integration

1. Install VS Code on Windows
2. Install "Remote - WSL" extension
3. In WSL terminal, type: `code .`
4. VS Code opens with full Linux support!

---

## 4. Why To Avoid Emulators

### What Are Emulators?

Emulators **simulate** an entire different system, translating every instruction.

Examples:
- Git Bash (simulates Unix on Windows)
- Cygwin (Unix environment for Windows)
- MinGW/MSYS2

### Why Emulators Are Problematic

```
┌─────────────────────────────────────────────────────────────┐
│                    EMULATOR PROBLEMS                        │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│   1. TRANSLATION OVERHEAD                                   │
│      Unix Command → Translation Layer → Windows Call        │
│      (Slower and sometimes inaccurate)                      │
│                                                             │
│   2. INCOMPLETE COMPATIBILITY                               │
│      - Not all Unix features work                           │
│      - System calls may behave differently                  │
│      - Some tools simply don't work                         │
│                                                             │
│   3. PATH & ENVIRONMENT ISSUES                              │
│      - Mixed path formats cause confusion                   │
│      - Environment variables behave differently             │
│                                                             │
│   4. PACKAGE MANAGEMENT                                     │
│      - Limited packages available                           │
│      - Different from real Linux repos                      │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Real Example: Git Bash Limitations

```bash
# This works in real Linux/WSL
systemctl status nginx

# In Git Bash:
# ❌ systemctl: command not found
# (Because there's no real Linux kernel!)
```

### Comparison: Emulation vs WSL2

| Aspect | Git Bash/Cygwin | WSL2 |
|--------|-----------------|------|
| **Kernel** | Windows NT (translated) | Real Linux Kernel |
| **System Calls** | Emulated | Native |
| **Docker** | Via Docker Desktop | Native support |
| **Performance** | Slower | Near-native |
| **Compatibility** | ~70% | ~99% |
| **systemd** | ❌ Not available | ✅ Available |

### When Emulators Are "Okay"

- Quick git commands on Windows
- Simple file operations
- Learning basic commands

### When You MUST Use Real Linux (WSL2)

- Running Docker containers
- Python/Node development
- Data science workflows
- Anything production-related

---

## 💡 Key Takeaways

1. **VMs** provide full isolation but are resource-heavy
2. **WSL2** gives you real Linux on Windows with minimal overhead
3. **macOS** users just need Terminal + Homebrew
4. **Avoid emulators** for serious development work

---

*Continue to Part 3: Linux Basics & Q&A →*

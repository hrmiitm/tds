# Session 1: Environment Setup
## Part 3: Linux Basics & Conceptual Q&A

---

## 1. Linux Environment Basics

### The Shell

The **shell** is your command-line interface to Linux.

```
┌────────────────────────────────────────────────────────┐
│                       TERMINAL                          │
│  ┌──────────────────────────────────────────────────┐  │
│  │  user@hostname:~$  ← This is your PROMPT         │  │
│  │                                                   │  │
│  │  user     = your username                        │  │
│  │  hostname = computer name                        │  │
│  │  ~        = current directory (home)             │  │
│  │  $        = regular user (# for root)            │  │
│  └──────────────────────────────────────────────────┘  │
└────────────────────────────────────────────────────────┘
```

### Common Shells

| Shell | Description |
|-------|-------------|
| **bash** | Bourne Again Shell - most common default |
| **zsh** | Z Shell - default on macOS, more features |
| **fish** | Friendly Interactive Shell - user-friendly |
| **sh** | Original Bourne Shell - basic, portable |

Check your current shell:
```bash
echo $SHELL
```

### Linux File System Structure

```
/                       ← Root (top of everything)
├── home/               ← User home directories
│   └── username/       ← Your files (~)
├── etc/                ← System configuration files
├── bin/                ← Essential user binaries
├── usr/                ← User programs
│   ├── bin/            ← User binaries
│   └── local/          ← Locally installed software
├── var/                ← Variable files (logs, etc.)
├── tmp/                ← Temporary files
└── opt/                ← Optional/third-party software
```

### Essential Commands

#### Navigation
```bash
pwd                 # Print Working Directory (where am I?)
ls                  # List files
ls -la              # List ALL files with details
cd /path/to/dir     # Change Directory
cd ~                # Go to home directory
cd ..               # Go up one level
cd -                # Go to previous directory
```

#### File Operations
```bash
touch file.txt      # Create empty file
mkdir dirname       # Create directory
mkdir -p a/b/c      # Create nested directories
cp source dest      # Copy file
cp -r dir1 dir2     # Copy directory recursively
mv old new          # Move/rename
rm file             # Remove file
rm -rf dir          # Remove directory (CAREFUL!)
```

#### Viewing Files
```bash
cat file.txt        # Display entire file
less file.txt       # Paginated view (q to quit)
head -n 10 file     # First 10 lines
tail -n 10 file     # Last 10 lines
tail -f file        # Follow file (live updates)
```

#### Finding Things
```bash
find . -name "*.py"           # Find files by name
grep "pattern" file.txt       # Search in file
grep -r "pattern" directory/  # Search recursively
which python                  # Find command location
```

### Environment Variables

Environment variables store system-wide settings.

```bash
# View all environment variables
env

# View specific variable
echo $PATH
echo $HOME
echo $USER

# Set a variable (current session)
export MY_VAR="hello"

# Set permanently (add to ~/.bashrc or ~/.zshrc)
echo 'export MY_VAR="hello"' >> ~/.bashrc
source ~/.bashrc
```

### The PATH Variable

**PATH** tells the system where to find executable programs.

```bash
echo $PATH
# Output: /usr/local/bin:/usr/bin:/bin:/home/user/.local/bin

# When you type "python", system searches these directories in order
```

To add a new path:
```bash
export PATH="$PATH:/new/path/here"
```

### File Permissions

```bash
ls -l file.txt
# -rw-r--r-- 1 user group 1234 Jan 17 10:00 file.txt
#  └┬┘└┬┘└┬┘
#   │  │  └── Others: read only
#   │  └───── Group: read only  
#   └──────── Owner: read + write
```

| Permission | Number | Meaning |
|------------|--------|---------|
| r | 4 | Read |
| w | 2 | Write |
| x | 1 | Execute |

```bash
chmod 755 script.sh   # rwxr-xr-x (owner: all, others: read+execute)
chmod +x script.sh    # Add execute permission
```

### Package Management

#### Ubuntu/Debian (apt)
```bash
sudo apt update              # Update package list
sudo apt upgrade             # Upgrade installed packages
sudo apt install package     # Install a package
sudo apt remove package      # Remove a package
apt search keyword           # Search for packages
```

#### macOS (Homebrew)
```bash
brew update                  # Update Homebrew
brew upgrade                 # Upgrade packages
brew install package         # Install a package
brew uninstall package       # Remove a package
brew search keyword          # Search for packages
```

---

## 2. Conceptual Q&A

### Q1: Why can't I just use Windows for development?

**Answer:** You *can*, but you'll face challenges:

1. **Environment Mismatch**: Production servers run Linux. Developing on Windows means your code might behave differently when deployed.

2. **Tool Compatibility**: Many development tools, Docker containers, and scripts are designed for Unix-like systems.

3. **Path Differences**: Windows uses `C:\path\to\file`, Unix uses `/path/to/file`. This causes bugs.

4. **Line Endings**: Windows uses CRLF (`\r\n`), Unix uses LF (`\n`). This breaks scripts and causes git conflicts.

**Best Practice**: Use WSL2 on Windows to get a real Linux environment.

---

### Q2: What's the difference between Terminal, Shell, and Console?

**Answer:**

| Term | Definition |
|------|------------|
| **Terminal** | The application/window where you type commands |
| **Shell** | The program that interprets your commands (bash, zsh) |
| **Console** | Originally physical hardware; now used interchangeably with terminal |

Think of it like:
- **Terminal** = The browser window
- **Shell** = The website/application running inside

---

### Q3: Why is `sudo` needed for some commands?

**Answer:** `sudo` stands for "**S**uper**U**ser **DO**". It grants temporary **root** (administrator) privileges.

```bash
# Regular user - can't modify system files
apt install git         # ❌ Permission denied

# With sudo - runs as root
sudo apt install git    # ✅ Works
```

**Why This Exists:**
- Security: Prevents accidental system damage
- Audit: Logs who ran privileged commands
- Multi-user: Limits what each user can do

---

### Q4: What's the difference between a VM, Container, and WSL?

**Answer:**

```
┌─────────────────────────────────────────────────────────────┐
│                      COMPARISON                              │
├───────────────┬─────────────────┬─────────────┬─────────────┤
│               │ Virtual Machine │ Container   │ WSL2        │
├───────────────┼─────────────────┼─────────────┼─────────────┤
│ Isolation     │ Complete        │ Process     │ OS-level    │
│ Has Own OS?   │ Yes (full)      │ No (shared) │ Yes (Linux) │
│ Startup       │ Minutes         │ Seconds     │ Seconds     │
│ Resources     │ Heavy           │ Light       │ Light       │
│ Use Case      │ Full isolation  │ App deploy  │ Dev environ │
└───────────────┴─────────────────┴─────────────┴─────────────┘
```

- **VM**: Like a separate computer running inside yours
- **Container**: Like a lightweight, isolated app package
- **WSL2**: Linux running alongside Windows, sharing resources

---

### Q5: What is POSIX and why does it matter?

**Answer:** **POSIX** (Portable Operating System Interface) is a standard that defines how Unix-like operating systems should behave.

**Why It Matters:**
- Code written for one POSIX system works on others
- macOS, Linux, BSD are all POSIX-compliant
- Windows is NOT POSIX-compliant (hence the differences)

**Example**: A shell script written on macOS will work on Linux because both follow POSIX standards.

---

### Q6: Why do we use `apt` instead of downloading from websites?

**Answer:** Package managers like `apt` provide:

| Benefit | Explanation |
|---------|-------------|
| **Security** | Packages are verified and signed |
| **Dependencies** | Automatically installs required libraries |
| **Updates** | One command updates everything |
| **Consistency** | Everyone gets the same version |
| **Cleanup** | Easy to remove with all components |

```bash
# Instead of downloading Python from website:
sudo apt install python3

# Update ALL software at once:
sudo apt update && sudo apt upgrade
```

---

### Q7: What's the difference between `.bashrc` and `.bash_profile`?

**Answer:**

| File | When It Runs |
|------|--------------|
| `.bash_profile` | Login shells (when you first log in) |
| `.bashrc` | Non-login shells (new terminal windows) |

**Best Practice**: Put your configurations in `.bashrc` and source it from `.bash_profile`:

```bash
# In .bash_profile
if [ -f ~/.bashrc ]; then
    source ~/.bashrc
fi
```

For **zsh** users: Use `.zshrc` (it's simpler - one file for everything).

---

### Q8: How do I know if a command is safe to run?

**Answer:** Follow these guidelines:

| Command | Safety Level | Notes |
|---------|--------------|-------|
| `ls`, `pwd`, `cat` | 🟢 Safe | Read-only commands |
| `mkdir`, `touch` | 🟢 Safe | Creates files/dirs |
| `cp`, `mv` | 🟡 Caution | Can overwrite files |
| `rm` | 🔴 Dangerous | Deletes permanently |
| `rm -rf` | ⛔ Very Dangerous | No confirmation, recursive |
| `sudo rm -rf /` | ☠️ NEVER | Destroys your system |

**Tips:**
1. Use `ls` before `rm` to see what you're deleting
2. Use `rm -i` for confirmation prompts
3. Never run commands you don't understand
4. Be extra careful with `sudo`

---

### Q9: Why doesn't my command work when I open a new terminal?

**Answer:** You probably set a variable in the current session but didn't save it.

**Session vs Permanent:**
```bash
# This ONLY works in current session
export MY_VAR="hello"

# To make it permanent, add to your shell config
echo 'export MY_VAR="hello"' >> ~/.bashrc
source ~/.bashrc  # Apply immediately
```

---

### Q10: What's the difference between `/` and `~` paths?

**Answer:**

| Symbol | Meaning | Example |
|--------|---------|---------|
| `/` | Root of entire filesystem | `/etc/hosts` |
| `~` | Your home directory | `~/Documents` = `/home/username/Documents` |
| `.` | Current directory | `./script.sh` |
| `..` | Parent directory | `cd ..` |

---

## 3. Practice Exercises

### Exercise 1: Navigation Challenge
```bash
# 1. Go to your home directory
# 2. Create a folder called "tds-practice"
# 3. Inside it, create three files: file1.txt, file2.txt, file3.txt
# 4. List all files with details
# 5. Go back to home directory in one command
```

### Exercise 2: Environment Variables
```bash
# 1. Display your current PATH
# 2. Create an environment variable called "MY_NAME" with your name
# 3. Print it
# 4. Make it permanent by adding to ~/.bashrc
```

### Exercise 3: File Permissions
```bash
# 1. Create a file called "secret.txt"
# 2. Check its current permissions
# 3. Make it readable only by you (owner)
# 4. Verify the change
```

---

## 📋 Session Summary Checklist

By now, you should understand:

- [ ] Why TDS uses Linux/Unix
- [ ] Key differences between Windows and Unix
- [ ] What VMs and WSL are
- [ ] How to set up macOS (Terminal + Homebrew)
- [ ] How to set up WSL2 on Windows
- [ ] Why emulators are problematic
- [ ] Basic Linux commands and concepts

---

## 📚 Additional Resources

- [Ubuntu WSL Documentation](https://ubuntu.com/wsl)
- [Homebrew Documentation](https://docs.brew.sh)
- [Linux Command Line Basics](https://ubuntu.com/tutorials/command-line-for-beginners)
- [The Missing Semester (MIT)](https://missing.csail.mit.edu/)

---

## ❓ Questions?

Feel free to ask any questions about:
- Environment setup issues
- Linux commands
- WSL configuration
- macOS Terminal usage

---

*End of Session 1: Environment Setup*

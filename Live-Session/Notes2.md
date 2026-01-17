# Two things to understand

- `$PATH` variable
- `.bashrc` file


# Everything Is a File — Then Is `uv` or `ls` Also a File?

Yes ✅
In Linux, **almost everything is treated as a file**.

* `ls`, `uv`, `cat`, `echo` → **files**
* Directories → files
* Devices → files

You can verify this:

```bash
which ls
file $(which ls)
```

---

## Question 1: How Does a Program Get Installed?

### What is a program?

* Text File

### What does “installed” mean?

* The file is:

  * Placed in a **standard directory** (like `/usr/bin`)
  * Given **execute permission**
  * Located in a directory listed in `$PATH`

Example:

```bash
ls -l /usr/bin/ls
```

---

## Question 2: How Does `ls` or `ls -la` Work When I Type It?

### Step-by-step explanation

1. You type:

   ```bash
   ls -la
   ```
2. The shell:

   * Looks for a file named `ls`
   * Searches directories listed in the `$PATH` variable
3. Once found:

   * The shell **executes that file**
   * Passes `-la` as arguments

### Where is the `ls` file?

```bash
which ls
```

### How does the shell know where to look?

```bash
echo $PATH
```

---

## Question 3: What Does `echo $PATH` Mean, and Where Is It Set?

### Meaning of `echo $PATH`

* `PATH` is an **environment variable**
* It contains a **colon-separated list of directories**
* The shell searches these directories to find commands

Example:

```bash
/usr/local/bin:/usr/bin:/bin
```

---

## Where Does `$PATH` Come From?

### 1️⃣ OS and Shell Design

Linux and shells (like Bash) are designed to:

* Look at the `$PATH` variable
* Search directories **from left to right**
* Execute the first matching executable file

---

### 2️⃣ Shell Startup Files

#### `.bashrc`

* Runs **every time you open a new terminal**
* Common place to modify `$PATH`

Example:

```bash
export PATH="$PATH:$HOME/bin"
```

This means:

* The change applies to **every new terminal**
* Not to already-open terminals

---

## Key Takeaways

* ✔ Commands like `ls` and `uv` are **files**
* ✔ Programs work because they exist in a directory listed in `$PATH`
* ✔ `$PATH` is a variable containing directory paths
* ✔ The shell uses `$PATH` to find and run commands
* ✔ `.bashrc` is executed every time a new terminal opens



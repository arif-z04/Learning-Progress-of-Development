# Linux Fundamentals: Files, Directories, Paths, Permissions & Environment Variables

## 1. Files and Directories

### 1.1 File

A **file** is a named unit of data stored in a filesystem. It can contain source code, text, images, configuration, executable programs, or other data.

Examples:
- `main.cs` — C# source code
- `index.html` — HTML document
- `appsettings.json` — application configuration
- `.env` — environment configuration, often containing secrets

### 1.2 Directory

A **directory** is a filesystem object used to organize files and other directories.

A directory can contain:
- Files
- Subdirectories
- Other filesystem entries

Example project structure:

```text
sunshine-portal/
├── frontend/
│   ├── index.html
│   ├── style.css
│   └── script.js
├── backend/
│   ├── Program.cs
│   └── appsettings.json
├── sql/
│   └── schema.sql
├── .gitignore
└── README.md
```

Here, `sunshine-portal` is the project directory. `frontend`, `backend`, and `sql` are subdirectories.

### 1.3 Linux Filesystem Structure

Linux organizes files and directories in a hierarchical tree starting at the root directory `/`.

```text
/
├── home/
│   └── noir/
│       ├── Documents/
│       ├── Projects/
│       └── Downloads/
├── etc/
├── usr/
├── var/
├── tmp/
└── dev/
```

Important directories:

| Directory | Purpose |
|---|---|
| `/` | Root of the filesystem hierarchy |
| `/home` | Home directories for regular users |
| `/etc` | System-wide configuration files |
| `/usr` | Many installed programs, libraries, and shared resources |
| `/var` | Variable data, such as logs and caches |
| `/tmp` | Temporary files |
| `/dev` | Device files representing devices and kernel interfaces |
| `/bin` | Essential command binaries; often linked to `/usr/bin` on modern distributions |

**Note:** `/` is the filesystem root. `/root` is the home directory of the root user. They are not the same.

---

## 2. Paths

### Definition

A **path** specifies the location of a file or directory within a filesystem.

There are two main types of paths: absolute and relative.

### 2.1 Absolute Path

An absolute path identifies a location starting from the filesystem root `/`.

Example:

```text
/home/noir/Projects/sunshine-portal/backend/Program.cs
```

It starts at `/` and describes the location independently of the current working directory.

### 2.2 Relative Path

A relative path identifies a location starting from the current working directory.

Suppose the current directory is:

```text
/home/noir/Projects/sunshine-portal/
```

Then:

```text
backend/Program.cs
```

refers to:

```text
/home/noir/Projects/sunshine-portal/backend/Program.cs
```

The same relative path can refer to a different location if the current directory changes.

### 2.3 Special Path Symbols

| Symbol | Meaning | Example |
|---|---|---|
| `/` | Filesystem root | `/etc/hosts` |
| `~` | Current user's home directory | `~/Projects` |
| `.` | Current directory | `./script.sh` |
| `..` | Parent directory | `cd ..` |
| `-` | Previous working directory in `cd` | `cd -` |

### 2.4 Path Examples

```bash
pwd
```

Displays the current working directory.

```bash
cd ~/Projects
```

Changes to the `Projects` directory inside your home directory.

```bash
cd ..
```

Moves to the parent directory.

```bash
cd -
```

Returns to the previous working directory.

```bash
realpath ./script.sh
```

Displays the absolute path of a file, provided the path can be resolved.

### 2.5 Important Path Commands

| Command | Purpose |
|---|---|
| `pwd` | Print current working directory |
| `ls` | List directory contents |
| `ls -la` | List files, including hidden entries, with details |
| `cd directory` | Change directory |
| `mkdir name` | Create a directory |
| `mkdir -p a/b` | Create parent directories as needed |
| `touch file.txt` | Create an empty file if absent; otherwise update timestamps |
| `cp source destination` | Copy files or directories |
| `mv source destination` | Move or rename files |
| `rm file.txt` | Remove a file |
| `find path -name "*.cs"` | Find matching filenames under a path |

**Warning:** Be careful with `rm`, especially recursive or forced deletion. Removed files may not be recoverable through normal means.

---

## 3. Hidden Files and Directories

In Linux, filenames beginning with `.` are conventionally treated as hidden by ordinary directory listings.

Examples:

```text
.env
.gitignore
.config/
.ssh/
```

Display hidden entries with:

```bash
ls -la
```

### Common Hidden Files

| File | Purpose |
|---|---|
| `.env` | Environment variables for applications |
| `.gitignore` | Specifies files Git should ignore |
| `.bashrc` | Bash shell configuration |
| `.zshrc` | Zsh shell configuration |
| `.git/` | Git repository metadata |

**Security note:** A leading dot does not protect a file from access. It only affects how files are displayed by common tools. Protect sensitive files with appropriate permissions and avoid committing secrets to version control.

---

## 4. File Permissions

### 4.1 Definition

Linux permissions control which users can read, modify, or execute filesystem objects.

Linux commonly evaluates permissions for three classes:

- **User (`u`):** The file's owner.
- **Group (`g`):** Users in the file's associated group.
- **Others (`o`):** Everyone who is neither the owner nor a member of the associated group.

### 4.2 Permission Types

| Permission | Symbol | For Regular Files | For Directories |
|---|---|---|---|
| Read | `r` | Read file contents | List directory entries |
| Write | `w` | Modify file contents | Create, remove, or rename entries, subject to other restrictions |
| Execute | `x` | Execute the file if it is a valid executable | Traverse or access entries by name, subject to other restrictions |

Directory permissions differ from file permissions. For example, listing a directory and accessing a known file inside it can require different combinations of permissions.

### 4.3 Understanding `ls -l`

Command:

```bash
ls -l
```

Example output:

```text
-rwxr-xr-- 1 noir developers 1200 Oct 28 script.sh
```

The permission string is:

```text
- rwx r-x r--
│  │   │   │
│  │   │   └── Others: read
│  │   └────── Group: read and execute
│  └────────── Owner: read, write, execute
└───────────── Regular file
```

The first character indicates the file type. For example:
- `-` = regular file
- `d` = directory
- `l` = symbolic link

### 4.4 Changing Permissions with `chmod`

Add execute permission for the owner:

```bash
chmod u+x script.sh
```

Remove write permission for others:

```bash
chmod o-w file.txt
```

Set explicit permissions:

```bash
chmod 644 file.txt
chmod 755 script.sh
```

### 4.5 Numeric Permission System

Permissions can be represented using numbers:

| Permission | Value |
|---|---:|
| Read (`r`) | 4 |
| Write (`w`) | 2 |
| Execute (`x`) | 1 |

Add the values to determine each permission class.

Examples:

| Number | Permissions | Meaning |
|---|---|---|
| `7` | `rwx` | Read, write, execute |
| `6` | `rw-` | Read, write |
| `5` | `r-x` | Read, execute |
| `4` | `r--` | Read only |
| `0` | `---` | No permissions |

For `chmod 755 script.sh`:

- Owner: `7 = 4 + 2 + 1` → `rwx`
- Group: `5 = 4 + 1` → `r-x`
- Others: `5 = 4 + 1` → `r-x`

For `chmod 644 file.txt`:

- Owner: `6 = 4 + 2` → `rw-`
- Group: `4` → `r--`
- Others: `4` → `r--`

### 4.6 Common Permission Patterns

| Permission | Typical Use |
|---|---|
| `644` | Ordinary files readable by others but writable by owner |
| `755` | Directories or executable files accessible to others |
| `600` | Sensitive file readable and writable by owner only |
| `700` | Directory or executable accessible to owner only |

These are common patterns, not universal requirements. Actual permissions should match the application's security needs.

**Security warning:** Avoid `chmod 777` as a general fix. It grants read, write, and execute permissions to everyone and can expose files to unwanted modification.

---

## 5. Ownership and `sudo`

Each filesystem object normally has an owner and an associated group.

Inspect ownership:

```bash
ls -l file.txt
```

Change ownership with elevated privileges when appropriate:

```bash
sudo chown noir:developers file.txt
```

This changes the owner to `noir` and the group to `developers`, assuming those accounts exist.

`sudo` runs a command with elevated privileges according to the system's configuration.

**Best practice:** Do not use `sudo` automatically for every command. Use it only when the operation genuinely requires elevated permissions.

---

## 6. Environment Variables

### 6.1 Definition

An **environment variable** is a named value made available to a process through its environment.

Environment variables are often used to configure application behavior without hardcoding settings into source code.

Examples:

```text
HOME=/home/noir
PATH=/usr/local/bin:/usr/bin
APP_ENV=Development
```

### 6.2 Common Environment Variables

| Variable | Purpose |
|---|---|
| `HOME` | User's home directory |
| `PATH` | Directories searched for executable commands |
| `USER` | Commonly identifies the current user |
| `SHELL` | Usually identifies the user's configured shell |
| `LANG` | Locale setting |
| `APP_ENV` | Example application-specific environment variable |

Not every variable is defined in every environment, and some values depend on the shell, operating system, or application.

### 6.3 Read Environment Variables

```bash
echo "$HOME"
echo "$PATH"
printenv
```

- `echo "$HOME"` prints the value of `HOME`.
- `echo "$PATH"` prints the executable search path.
- `printenv` displays environment variables exported to the current process environment.

### 6.4 Set a Variable in the Current Shell

```bash
export APP_ENV=Development
```

Check it:

```bash
echo "$APP_ENV"
```

The variable is available in the current shell and is passed to child processes launched from that shell.

It does not automatically become a permanent system-wide setting.

### 6.5 Set a Variable for One Command

```bash
APP_ENV=Development python3 main.py
```

This sets `APP_ENV` for that command's environment without permanently changing the shell's environment.

### 6.6 Remove a Variable

```bash
unset APP_ENV
```

Removes the variable from the current shell environment.

### 6.7 Make Variables Persistent

Shell-specific startup files can define environment variables for future shell sessions.

For example, Bash users sometimes add an export to `~/.bashrc`:

```bash
export APP_ENV=Development
```

Zsh users may use `~/.zshrc` for interactive shell configuration.

Choose the correct file for your shell and remember that changes may require opening a new shell or reloading the configuration.

**Important:** Environment variables exported by a shell are normally inherited by its child processes, not automatically by unrelated applications or system services.

---

## 7. Environment Variables in Web Development

Applications often need configuration values such as:

- Database connection strings
- API keys
- Authentication secrets
- Application environment names
- External service URLs

Example:

```bash
export ASPNETCORE_ENVIRONMENT=Development
dotnet run
```

This sets the environment name for the launched .NET application.

In ASP.NET Core, the environment name influences which environment-specific configuration and behaviors are used.

### Security Best Practices

1. Never commit real passwords, API keys, or production secrets to Git.
2. Avoid printing secrets in terminal output or application logs.
3. Use a secrets manager or deployment platform's secret configuration for production.
4. Protect files containing secrets with restrictive permissions.
5. Remember that environment variables can be exposed through process inspection, diagnostics, or logs if access is not properly controlled.

A `.env` file is a common configuration technique for some tools, but it is not automatically loaded by every shell or application.

---

## 8. Practical Lab

Complete these exercises in your Linux terminal.

### Task 1: Create a Project Directory

```bash
mkdir -p ~/linux-practice/src
cd ~/linux-practice
pwd
```

### Task 2: Create Files

```bash
touch README.md
touch src/main.py
ls -la
find . -maxdepth 2 -type f
```

### Task 3: Create and Run a Shell Script

```bash
printf '#!/bin/sh\necho Hello from Linux\n' > hello.sh
chmod u+x hello.sh
./hello.sh
```

Expected output:

```text
Hello from Linux
```

### Task 4: Inspect Permissions

```bash
ls -l hello.sh
stat hello.sh
```

Compare the permission information before and after running `chmod u+x`.

### Task 5: Practice Environment Variables

```bash
echo "$HOME"
echo "$PATH"
export PRACTICE_MODE=Linux
echo "$PRACTICE_MODE"
PRACTICE_MODE=Temporary sh -c 'echo "$PRACTICE_MODE"'
echo "$PRACTICE_MODE"
unset PRACTICE_MODE
```

The final `echo` should print an empty line because `PRACTICE_MODE` was removed from the current shell.

---

## 9. Quick Revision

| Concept | Key Idea |
|---|---|
| File | Stores data |
| Directory | Organizes filesystem entries |
| Absolute path | Starts from `/` |
| Relative path | Starts from the current working directory |
| `.` | Current directory |
| `..` | Parent directory |
| Hidden file | Conventionally begins with `.` |
| Permission | Controls read, write, and execute access |
| `chmod` | Changes permissions |
| `chown` | Changes ownership |
| Environment variable | Supplies configuration to a process |
| `PATH` | Directories searched for executable commands |
| `export` | Places a shell variable in the environment passed to child processes |
| `sudo` | Runs a command with elevated privileges |

### Learning Milestone

You should now be able to navigate the Linux filesystem, create and inspect files, understand absolute and relative paths, interpret permissions, make a script executable, and configure environment variables for a development application.
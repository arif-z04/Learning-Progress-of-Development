# Linux Fundamentals: Terminal Navigation & File Operations

## 1. Introduction to the Linux Terminal

The **Linux terminal** is a text-based interface that allows users to interact with the operating system by entering commands.

Instead of clicking through graphical menus, you can use commands to:

- Navigate directories.
- Create, copy, move, and delete files.
- Search for files and directories.
- Read and edit text files.
- Manage permissions.
- Automate repetitive tasks using shell scripts.

For developers, terminal skills are essential when working with Git, databases, servers, development environments, and deployment tools.

### 1.1 Terminal vs. Shell

These terms are related but different.

| Term | Meaning |
|---|---|
| Terminal | The application or interface where you enter commands |
| Shell | The program that interprets and executes commands |
| Bash | A popular Unix shell |
| Zsh | Another popular shell |
| Fish | A user-friendly interactive shell |

Omarchy commonly uses a configured shell such as Zsh. You can identify your current shell with:

```bash
echo "$SHELL"
```

Check the shell process currently running:

```bash
ps -p $$ -o comm=
```

### 1.2 Basic Command Structure

A typical Linux command follows this structure:

```bash
command [options] [arguments]
```

Example:

```bash
ls -lah ~/Projects
```

| Part | Meaning |
|---|---|
| `ls` | Command |
| `-lah` | Options |
| `~/Projects` | Argument |

Options modify how a command behaves. Arguments usually specify the file, directory, or other input on which the command operates.

---

## 2. Terminal Navigation

Navigation means moving between directories and inspecting their contents.

### 2.1 Find Your Current Location: `pwd`

```bash
pwd
```

Displays the absolute path of the current working directory.

Example:

```text
/home/noir/Projects
```

### 2.2 List Directory Contents: `ls`

```bash
ls
```

Lists files and directories in the current location.

Common variations:

```bash
ls -l
```

Long format, including permissions, ownership, size, and modification time.

```bash
ls -a
```

Includes hidden entries.

```bash
ls -la
```

Combines detailed information and hidden entries.

```bash
ls -lh
```

Displays file sizes in human-readable units.

```bash
ls -lt
```

Sorts by modification time, newest first.

```bash
ls -lah ~/Projects
```

Lists all entries in a specified directory with detailed, human-readable information.

### 2.3 Change Directory: `cd`

Move into a directory:

```bash
cd Projects
```

Move to your home directory:

```bash
cd
```

Or:

```bash
cd ~
```

Move to the parent directory:

```bash
cd ..
```

Move to the filesystem root:

```bash
cd /
```

Return to the previous directory:

```bash
cd -
```

Move using an absolute path:

```bash
cd /home/noir/Projects
```

### 2.4 Important Navigation Symbols

| Symbol | Meaning | Example |
|---|---|---|
| `/` | Filesystem root | `cd /etc` |
| `~` | Home directory | `cd ~/Downloads` |
| `.` | Current directory | `./script.sh` |
| `..` | Parent directory | `cd ..` |
| `-` | Previous directory | `cd -` |

### 2.5 Navigate Multiple Levels

Suppose your project has this structure:

```text
Projects/
└── Sunshine/
    └── backend/
        └── src/
```

You can navigate directly:

```bash
cd ~/Projects/Sunshine/backend/src
```

Or move one level at a time:

```bash
cd ~/Projects
cd Sunshine
cd backend
cd src
```

**Tip:** Use the Tab key for shell autocomplete. For example, type `cd Pro` and press Tab to complete a matching directory name.

---

## 3. Understanding Paths

A path identifies the location of a file or directory.

### 3.1 Absolute Path

An absolute path starts from `/`.

Example:

```text
/home/noir/Projects/Sunshine/backend/Program.cs
```

It identifies the location independently of the current working directory.

### 3.2 Relative Path

A relative path starts from the current working directory.

Suppose you are currently in:

```text
/home/noir/Projects/Sunshine/
```

Then this relative path:

```text
backend/Program.cs
```

refers to:

```text
/home/noir/Projects/Sunshine/backend/Program.cs
```

### 3.3 Resolve a Path

```bash
realpath ./backend/Program.cs
```

Prints the resolved absolute path when the path exists and can be resolved.

### 3.4 Understand Your Current Directory

```bash
pwd
```

Use this command whenever you are uncertain where a relative path will operate.

**Important:** A command using a relative path operates in relation to the current working directory. This is especially important before running commands that modify or delete files.

---

## 4. Creating Directories and Files

### 4.1 Create a Directory: `mkdir`

```bash
mkdir my-project
```

Creates a directory named `my-project`.

Create multiple directories:

```bash
mkdir frontend backend sql
```

Create nested directories:

```bash
mkdir -p project/backend/src/controllers
```

The `-p` option creates missing parent directories and does not report an error merely because an existing directory is already present.

### 4.2 Create an Empty File: `touch`

```bash
touch README.md
```

Creates an empty file if it does not exist. If the file already exists, it updates its timestamps rather than erasing its contents.

Create several files:

```bash
touch index.html style.css script.js
```

### 4.3 Create Files with Text: `echo`

```bash
echo "Hello Linux" > message.txt
```

Writes the text into `message.txt`, replacing its previous contents if it exists.

Append text:

```bash
echo "Another line" >> message.txt
```

**Important difference:**

| Operator | Meaning |
|---|---|
| `>` | Redirect output and overwrite the destination |
| `>>` | Redirect output and append to the destination |

For more complex text, use a heredoc:

```bash
cat > README.md <<'EOF'
# My Project

A sample development project.
EOF
```

The quoted `EOF` prevents shell expansion inside the supplied text.

---

## 5. Copying Files and Directories

### 5.1 Copy a File: `cp`

```bash
cp source.txt destination.txt
```

Copies `source.txt` to `destination.txt`.

Copy a file into another directory:

```bash
cp README.md ~/Documents/
```

### 5.2 Copy Multiple Files

```bash
cp index.html style.css script.js frontend/
```

Copies all three files into the `frontend` directory.

### 5.3 Copy a Directory

```bash
cp -r frontend frontend-backup
```

The `-r` option copies directories recursively, including their contents.

### 5.4 Preserve File Attributes

```bash
cp -a project project-backup
```

Archive mode preserves important attributes such as permissions and timestamps where supported.

### 5.5 Interactive Copying

```bash
cp -i source.txt destination.txt
```

Asks before overwriting an existing destination.

**Developer tip:** Use `cp -i` when you are uncertain whether a destination already contains important data.

---

## 6. Moving and Renaming Files

Linux uses the `mv` command for both moving and renaming.

### 6.1 Move a File

```bash
mv report.txt ~/Documents/
```

Moves `report.txt` into the Documents directory.

### 6.2 Rename a File

```bash
mv old-name.txt new-name.txt
```

Renames the file in the same directory.

### 6.3 Move and Rename at the Same Time

```bash
mv report.txt ~/Documents/final-report.txt
```

Moves the file and gives it a new name.

### 6.4 Move a Directory

```bash
mv old-project ~/Projects/
```

Moves the directory into the Projects directory.

### 6.5 Interactive Move

```bash
mv -i source.txt destination.txt
```

Prompts before overwriting an existing destination.

---

## 7. Deleting Files and Directories

Deletion commands require extra care.

### 7.1 Remove a File: `rm`

```bash
rm unwanted.txt
```

Removes a file.

### 7.2 Interactive Deletion

```bash
rm -i unwanted.txt
```

Asks for confirmation before removal.

### 7.3 Remove an Empty Directory

```bash
rmdir empty-folder
```

Removes a directory only if it is empty.

### 7.4 Remove a Directory and Its Contents

```bash
rm -r old-project
```

Recursively removes a directory and its contents.

### 7.5 Force Removal

```bash
rm -rf old-project
```

- `-r`: recursive removal.
- `-f`: force removal without normal confirmation prompts.

**Critical safety warning:**

`rm -rf` can permanently remove large amounts of data. It does not normally move files to a graphical trash bin.

Before deleting anything:

```bash
pwd
ls -la
```

Confirm your location and the exact target.

Avoid copying destructive commands from the internet without understanding their paths and options.

---

## 8. Reading Files from the Terminal

Developers frequently inspect source code, configuration files, logs, and documentation without opening a graphical editor.

### 8.1 Display a File: `cat`

```bash
cat README.md
```

Prints the entire file to the terminal.

Useful for short files.

### 8.2 Read Large Files: `less`

```bash
less application.log
```

Useful controls:

| Key | Action |
|---|---|
| `Space` | Next page |
| `b` | Previous page |
| `/word` | Search for a word |
| `n` | Next search result |
| `N` | Previous search result |
| `g` | Beginning of file |
| `G` | End of file |
| `q` | Quit |

### 8.3 Display the Beginning: `head`

```bash
head README.md
```

Displays the first 10 lines by default.

Display the first 20 lines:

```bash
head -n 20 application.log
```

### 8.4 Display the End: `tail`

```bash
tail application.log
```

Displays the last 10 lines by default.

Display the last 50 lines:

```bash
tail -n 50 application.log
```

Follow new log entries:

```bash
tail -f application.log
```

Press `Ctrl+C` to stop following.

---

## 9. Editing Files from the Terminal

You can create and modify files using terminal-based text editors.

### 9.1 Nano

```bash
nano README.md
```

Common shortcuts:

| Shortcut | Action |
|---|---|
| `Ctrl + O` | Save |
| `Ctrl + X` | Exit |
| `Ctrl + W` | Search |
| `Ctrl + K` | Cut current line |
| `Ctrl + U` | Paste cut text |

Nano is beginner-friendly and useful for quick configuration changes.

### 9.2 Vim or Neovim

```bash
vim README.md
```

Or:

```bash
nvim README.md
```

Basic Vim concepts:

- Normal mode: navigation and commands.
- Insert mode: entering text.
- Command-line mode: saving, quitting, and other commands.

Useful commands:

| Command | Action |
|---|---|
| `i` | Enter insert mode |
| `Esc` | Return to normal mode |
| `:w` | Save |
| `:q` | Quit |
| `:wq` | Save and quit |
| `:q!` | Quit without saving |

**Note:** If you use Neovim as your main editor, learning terminal-based file navigation will make it easier to manage projects without leaving the terminal.

---

## 10. Searching for Files and Directories

### 10.1 Find Files by Name: `find`

```bash
find ~/Projects -name "README.md"
```

Searches for files or directories named `README.md` under Projects.

Find all C# files:

```bash
find ~/Projects -type f -name "*.cs"
```

Find directories only:

```bash
find ~/Projects -type d -name "backend"
```

Find files modified within the last day:

```bash
find ~/Projects -type f -mtime -1
```

Find files larger than 100 MB:

```bash
find ~/Projects -type f -size +100M
```

### 10.2 Search File Contents: `grep`

Search for text inside files:

```bash
grep "Database" appsettings.json
```

Search recursively inside a project:

```bash
grep -R "ConnectionString" .
```

Useful options:

| Option | Meaning |
|---|---|
| `-i` | Ignore uppercase/lowercase differences |
| `-n` | Show line numbers |
| `-r` | Search recursively |
| `-l` | Show filenames containing matches |
| `-v` | Show lines that do not match |

Example:

```bash
grep -rin "TODO" .
```

Searches recursively, ignoring case, and displays line numbers.

For source-code projects, exclude generated directories where appropriate:

```bash
grep -rin "TODO" . --exclude-dir=.git --exclude-dir=bin --exclude-dir=obj
```

---

## 11. File Information and Disk Usage

### 11.1 Check File Information: `file`

```bash
file image.png
```

Identifies the file type based on its contents.

A file extension alone does not guarantee the actual file format.

### 11.2 Check File Size: `du`

```bash
du -sh project/
```

Displays the total disk space used by a directory.

### 11.3 Check Filesystem Space: `df`

```bash
df -h
```

Displays available and used space on mounted filesystems.

### 11.4 Check Detailed Metadata: `stat`

```bash
stat README.md
```

Displays information such as file size, permissions, ownership, and timestamps.

### 11.5 Count Lines, Words, and Bytes: `wc`

```bash
wc README.md
```

Displays line, word, and byte counts.

Individual options:

```bash
wc -l README.md
wc -w README.md
wc -c README.md
```

---

## 12. Wildcards and Pattern Matching

Wildcards let you work with multiple files without specifying every filename individually.

### 12.1 Asterisk: `*`

Matches zero or more characters.

```bash
ls *.txt
```

Lists files ending in `.txt`.

```bash
cp *.jpg images/
```

Copies matching JPG files into the images directory.

### 12.2 Question Mark: `?`

Matches exactly one character.

```bash
ls file?.txt
```

Could match:

```text
file1.txt
fileA.txt
file2.txt
```

It would not match `file10.txt`.

### 12.3 Character Sets: `[ ]`

Matches one character from a specified set or range.

```bash
ls file[123].txt
```

Matches `file1.txt`, `file2.txt`, and `file3.txt`.

```bash
ls report[0-9].pdf
```

Matches filenames containing one digit in that position.

**Important:** Shell wildcards are expanded by the shell before the command receives its arguments. This differs from regular expressions used by tools such as `grep`.

---

## 13. Command Chaining and Redirection

You can combine commands to build useful workflows.

### 13.1 Run Commands Sequentially: `;`

```bash
pwd; ls; date
```

Runs each command in sequence, regardless of whether the previous command succeeded.

### 13.2 Run the Next Command Only on Success: `&&`

```bash
mkdir project && cd project
```

The second command runs only if the first succeeds.

### 13.3 Run the Next Command on Failure: `||`

```bash
cd project || echo "Directory not found"
```

Prints the message if changing directory fails.

### 13.4 Pipe: `|`

A pipe passes the output of one command as the input of another.

```bash
ls -lah | less
```

Another example:

```bash
ps aux | grep dotnet
```

This searches process output for matching text. The output may include the `grep` command itself.

### 13.5 Standard Input and Output

Linux programs commonly use three standard streams:

| Stream | File Descriptor | Purpose |
|---|---:|---|
| Standard input (`stdin`) | 0 | Input to a program |
| Standard output (`stdout`) | 1 | Normal output |
| Standard error (`stderr`) | 2 | Error output |

Redirect standard output:

```bash
ls > files.txt
```

Redirect standard error:

```bash
some-command 2> errors.txt
```

Redirect both standard output and standard error to the same file:

```bash
some-command > output.txt 2>&1
```

Append both:

```bash
some-command >> output.txt 2>&1
```

These techniques are especially useful when debugging applications and collecting command output.

---

## 14. Useful Terminal Shortcuts

| Shortcut | Function |
|---|---|
| `Ctrl + C` | Interrupt the foreground command |
| `Ctrl + Z` | Suspend the foreground job |
| `Ctrl + D` | Send end-of-file to the terminal input |
| `Ctrl + L` | Clear the terminal display |
| `Ctrl + A` | Move to the beginning of the command line |
| `Ctrl + E` | Move to the end of the command line |
| `Ctrl + U` | Remove text from the cursor to the beginning |
| `Ctrl + K` | Remove text from the cursor to the end |
| `Ctrl + R` | Search command history |
| `Tab` | Autocomplete commands and paths |
| `Up Arrow` | Previous command |
| `Down Arrow` | Next command |

### Command History

```bash
history
```

Displays previously executed commands.

Search command history interactively:

```text
Ctrl + R
```

Type part of a previous command to search for it.

---

## 15. Practical Lab: Build a Project Structure

Let's create a sample full-stack project directory from the terminal.

### Step 1: Create the Main Directory

```bash
mkdir -p ~/Projects/agri-ecommerce
cd ~/Projects/agri-ecommerce
```

### Step 2: Create Project Directories

```bash
mkdir -p frontend/{css,js,images}
mkdir -p backend/{Controllers,Models,Services,Data}
mkdir -p sql
mkdir -p documentation
mkdir -p tests
```

### Step 3: Create Files

```bash
touch README.md
touch .gitignore
touch frontend/index.html
touch frontend/css/style.css
touch frontend/js/app.js
touch backend/Program.cs
touch sql/schema.sql
```

### Step 4: Inspect the Structure

```bash
pwd
ls -lah
find . -maxdepth 3 -print
```

If you have the `tree` utility installed:

```bash
tree
```

On Arch-based systems, install it with:

```bash
sudo pacman -S tree
```

### Step 5: Add Project Information

```bash
cat > README.md <<'EOF'
# Agricultural E-Commerce

A sample full-stack agricultural e-commerce project.

## Directories

- frontend: User interface
- backend: Application backend
- sql: Database scripts
- documentation: Project documentation
- tests: Automated tests
EOF
```

### Step 6: Read the README

```bash
cat README.md
```

### Step 7: Find All Project Files

```bash
find . -type f
```

### Step 8: Search for a File

```bash
find . -name "Program.cs"
```

### Step 9: Check Project Size

```bash
du -sh .
```

You have now created and inspected a basic full-stack project structure entirely through the terminal.

---

## 16. Quick Command Reference

| Task | Command |
|---|---|
| Show current location | `pwd` |
| List files | `ls` |
| Show hidden files | `ls -la` |
| Change directory | `cd path` |
| Go home | `cd ~` |
| Go one level up | `cd ..` |
| Create directory | `mkdir name` |
| Create nested directories | `mkdir -p a/b/c` |
| Create empty file | `touch file.txt` |
| Copy file | `cp source destination` |
| Copy directory | `cp -r source destination` |
| Move file | `mv source destination` |
| Rename file | `mv old new` |
| Delete file | `rm file.txt` |
| Delete empty directory | `rmdir directory` |
| Delete directory recursively | `rm -r directory` |
| Display file | `cat file.txt` |
| Read large file | `less file.txt` |
| Show first lines | `head file.txt` |
| Show last lines | `tail file.txt` |
| Edit file | `nano file.txt` |
| Find files | `find path -name "pattern"` |
| Search file contents | `grep -R "text" path` |
| Check file type | `file filename` |
| Check metadata | `stat filename` |
| Check directory size | `du -sh directory` |
| Check filesystem space | `df -h` |
| Count lines | `wc -l filename` |
| Display directory tree | `tree` |
| Show command history | `history` |

---

## 17. Learning Milestone

You should now be able to:

- Navigate directories using absolute and relative paths.
- Understand the basic terminal and shell workflow.
- Create, copy, move, rename, and delete files.
- Read and edit files without a graphical editor.
- Search for filenames and text inside files.
- Use wildcards to work with multiple files.
- Combine commands using pipes and logical operators.
- Redirect command output and errors.
- Create a structured project directory from scratch.

**Developer habit:** Become comfortable navigating your project, inspecting files, and performing routine operations directly from the terminal. These skills will be useful when working with Git, ASP.NET Core, databases, Linux servers, and deployment environments.
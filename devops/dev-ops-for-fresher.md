# Table of Contents

- [Linux Users and Groups](#linux-users-and-groups)
- [Vim Basics](#vim-basics)

# Linux Users and Groups

### User and Group Management

- **`useradd` vs `adduser`:**

  - **`useradd`**: Creates a simple user account with default settings.
  - **`adduser`**: A more interactive command that allows you to set additional user details during the process.

- **`su {userName}`:**
  - **`su`**: Switches to another user account (by default the root user if no username is provided).
  - Usage: `su username` to log in as that user.
- **`deluser {userName}`:**
  - Deletes the specified user account.
- **`groupadd` vs `delgroup`:**

  - **`groupadd {groupName}`**: Creates a new group.
  - **`delgroup {groupName}`**: Deletes a group.

- **`usermod -aG {groupName} {userName}`:**

  - Adds a user to a group.
  - **`-a`**: Add the user to the group without removing them from existing groups.
  - **`-G`**: Specifies the group(s) to add the user to.
  - Example: `usermod -aG developers john`

- **`groups {userName}`:**

  - Lists all the groups a user belongs to.
  - Example: `groups john`

- **`deluser {userName} {groupName}`:**
  - Removes a user from a specific group.
  - Example: `deluser john developers`

---

# File and Directory Ownership

### Changing Ownership

- **`chown -R {userName}:{groupName} {folderName}`**:
  - Changes the ownership of a directory (`folderName`) to the specified user and group.
  - **`-R`**: Apply the change recursively to all files and subdirectories.
  - Example: `chown -R john:admins /var/www`

---

# File Permissions and Access

### Permission Representation

- **`rwx`**: Represents the permissions:

  - **`r`** (read): Ability to read the file or list the contents of a directory.
  - **`w`** (write): Ability to modify the file or add/remove files in a directory.
  - **`x`** (execute): Ability to run the file as a program or script. For directories, this allows accessing files within it.

- **`ugo`**: Represents the users who have permissions:
  - **`u`** (user): The file's owner.
  - **`g`** (group): The group associated with the file.
  - **`o`** (others): All other users.

---

### Using `chmod` to Change Permissions

- **Syntax:**

  - `chmod {permission} {fileName}`  
    Example: `chmod u+x myfile.sh` (adds execute permission for the file owner)

- **Permissions by Number:**

  - **`r = 4`** (binary `100`)
  - **`w = 2`** (binary `010`)
  - **`x = 1`** (binary `001`)
  - **Total (`rwx`) = 4 + 2 + 1 = 7**
    - Example: `chmod 777 myfile.sh` (gives full permissions to user, group, and others)

- **`chmod 777 {fileName}`**:
  - Grants **read**, **write**, and **execute** permissions to **user**, **group**, and **others**.
  - **`777`** means full control (rwx for everyone).

---

### Summary of Common Commands

| Command                                         | Description                                               |
| ----------------------------------------------- | --------------------------------------------------------- |
| `useradd` / `adduser`                           | Create a user                                             |
| `su {userName}`                                 | Switch user (log in as specified user)                    |
| `deluser {userName}`                            | Delete a user                                             |
| `groupadd {groupName}` / `delgroup {groupName}` | Create or delete a group                                  |
| `usermod -aG {groupName} {userName}`            | Add user to a group                                       |
| `groups {userName}`                             | List groups a user belongs to                             |
| `deluser {userName} {groupName}`                | Remove user from a group                                  |
| `chown -R {userName}:{groupName} {folderName}`  | Change ownership of files/folder (recursively)            |
| `chmod {permission} {fileName}`                 | Change file permissions                                   |
| `chmod 777 {fileName}`                          | Grant full permissions (rwx) to all (user, group, others) |

# Vim Basics

## Modes

- **Insert Mode (`i`)** – Allows typing text.
- **Command Mode (`Esc`)** – For executing commands.

## Essential Commands

- **`dd`** – Deletes the entire current line. (Double `d` means "delete line")
- **`u`** – Undoes the last change. (`u` for "undo")
- **`yy`** – Copies (yanks) the current line. (Double `y` means "yank line")
- **`p`** – Pastes after the cursor. (`p` for "put")
- **`/`** – Starts a search. (`/` is commonly used for searching)
- **`:x`** – Saves and exits. (Like `:wq`, but only saves if needed)
- **`:q!`** – Quits without saving. (`!` forces quitting)

# Thinking to implement every project

## Logic to implement

- Every project have their own tools
- Just care about **configuration file**
- **Build** then **run**

## Best practices

- Every project have their own working directory
- Every project have their own user

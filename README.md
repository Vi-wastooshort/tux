# tux 🐧
`tux` is a lightweight, UNIX-like kernel and shell implementation in Minecraft using Skript. It comes with a fully implemented in-memory filesystem along with a set of familiar command-line tools. It requires no dependencies other than Skript, so you only need to install tux.

Stable releases of tux are located in `releases`, and we recommend people use our releases for server use. However, if you want `unstable`, yet have all latest tux features, you can download the code directly from GitHub and use that. If you use the unstable branch of tux, please report bugs and errors in issues.

tux works best with Paper, and is (according to my knowledge) compatible with most major Paper and Skript releases.

<img width="654" height="166" alt="image" src="https://github.com/user-attachments/assets/74957ae1-30d1-44ea-ae06-32932e1f2be5" />

## Installation
1. Install Skript (https://modrinth.com/plugin/skript) onto your server.
2. Download the latest release of tux from `releases`.
3. Extract the .zip file into the scripts directory in your plugins folder.
4. Type into chat or console the command `/skript reload all`.
5. Done. To see if it installed properly, input the command `/fastfetch`.

## Documentation
**IMPORTANT** The default `/sudo-login` password is `root`. If someone authenticates using the root password, they can be able to run *any* server command using the *server* console. It is **very** important that server administrators change the `/sudo` password in the file `rootpassword.sk` in the `system` folder before reloading Skript using `/skript reload all`.

**Note**: tux is still in *beta*. Bugs are expected. Please report bugs in issues: https://github.com/Vi-wastooshort/tux/issues.

The following commands do *not* require `/sudo` permissions:
- /ls - Lists all files in your current directory. Example: `/ls`
- /cd <directory> - Swap to a different directory. Example: `/cd secrets` or `/cd /filesystem/root/secrets`
- /pwd - Prints the directory you are currently in. Stands for "print working directory". Example: `/pwd` outputs `/filesystem/root/secrets`
- /fastfetch - Prints basic tux and server information, as well as nice ASCII art. Example: `/fastfetch`
- /cat <file> - Prints the contents of a file specified. Example: `/cat secrets.txt` or `/cat /filesystem/root/secrets.txt`.
- /sudo-login <password> - Gives the user `10 minutes` of sudo permissions. By default, the password is `root`. Example: `/sudo-login root`

The following commands require `/sudo` permissions. You do not need quotations to append or to write text to files.
- /mkdir <text> - Creates a new directory. Example: `/mkdir NewFolder`
- /touch <text> - Creates an empty text file. It is recommended to add `.txt` to the end to distinguish it as a text file. Example: `/touch supersecret.txt`
- /write <file> <text> - Writes to a file. Example: `/write supersecret.txt The quick brown fox jumps over the lazy dog.`
- /append <file> <text> - Adds text to a text file. Example: `/append supersecret.txt No, they don't!`
- /rm <file> - Deletes a file or directory. **THIS IS IRREVERSIBLE!** Example: `/rm supersecret.txt` or `/rm /filesystem/root/supersecret.txt`
- /chmod <permission> <player> - Adjust permissions. *Permissions are a Work In Progress! Expect to see permissions added in a later version of tux.*
- /mv <source file|old name> <destination|new_name> - Renames or moves files and directories. Example: `/mv /filesystem/root/supersecret.txt /filesystem/root/secrets/`

### Filesystem
The default filesystem when you first login is `/filesystem/root`. `/filesystem` is immutable, and `/root` is a protected directory, meaning you cannot rename or alter the file itself, only the contents inside `root`.

### Sudo
Some commands require `sudo` permissions by default. In order to gain sudo permissions, use the command `/sudo-login <password>`. By default, the password is `root`; however, it is **HIGHLY** recommended that you change the root password in `rootpassword.sk` in the `system` folder of tux in order to prevent unauthorized usage of **SERVER CONSOLE** commands. **tux developers are not responsible for the damages caused by root password negligence!**

## Q&A

**Q**: The filesystem isn’t saving after a server restart. Why?

`tux` uses an in-memory filesystem by default. We do have plans for persistent file storage, but only in a later version.

**Q:** Can I create new users or groups?

Not yet. Permissions are a work in progress. Currently, only the `root` user (via `/sudo-login`) has elevated access. We are working on implementing a way to give elevated file access through users and groups without sharing a root password.

**Q:** Commands aren’t working after installation.

Ensure:
- Skript is installed and up to date.
- You’ve reloaded Skript (/skript reload all).
- You’re using a Paper-compatible server (Spigot/Bukkit may work but aren’t officially supported).
Otherwise, submit a bug report in issues.

**Q:** I get "Invalid path" errors.

Paths are case-sensitive and must use `/` (not `\`). Example: `/cd /filesystem/root` (correct) vs. `/cd \filesystem\root` (incorrect).

**Q:** Why the name "tux"?

A: Tux is the official mascot of Linux, and this project is heavily based on and inspired by Linux. Plus, it’s cute.

**Q:** tux doesn't work on older versions of Paper/Skript. Can you port it to older versions?

Compatibility with older versions may be limited due to changes in Skript/Paper APIs. We might be able to port a version of tux to earlier Paper/Skript versions, but don't hold your breath for it.

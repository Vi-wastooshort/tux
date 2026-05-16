# tux 🐧
`tux` is a lightweight, UNIX-like kernel and shell implementation in Minecraft using Skript. It comes with a fully implemented in-memory filesystem along with a set of familiar command-line tools. It requires no dependencies other than Skript, so you only need to install tux.

Stable releases of tux are located in `releases`, and we recommend people use our releases for server use. However, if you want `unstable`, yet have all latest tux features, you can download the code directly from GitHub and use that. If you use the unstable branch of tux, please report bugs and errors in issues.

tux works best with Paper, and is (according to my knowledge) compatible with most major Paper and Skript releases.

tux is mainly for educational and entertainment purposes. Discretion is advised.

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

The following commands use a UNIX-like permission system. Depending on file ownership and permissions, some commands may require `/sudo` access.
- /mkdir <directory> - Creates a new directory if you have write access to the parent directory. Example: `/mkdir NewFolder`
- /touch <file> - Creates an empty file if you have write access to the parent directory. Example: `/touch supersecret.txt`
- /write <file> <text> - Overwrites the contents of a file if you have write permission. Example: `/write supersecret.txt The quick brown fox jumps over the lazy dog.`
- /append <file> <text> - Adds text to a file if you have write permission. Example: `/append supersecret.txt No, he didn't!`
- /rm <file|directory> - Deletes a file or directory if you have write access to the parent directory. **THIS IS IRREVERSIBLE!** Example: `/rm supersecret.txt`
- /chmod <permission> <path> - Changes permissions on a file or directory. Example: `/chmod 755 scripts`
- /chown <user> <path> - Changes ownership of a file or directory. Requires sudo permissions. Example: `/chown root secrets.txt`
- /mv <source> <destination> - Renames or moves files and directories if you have sufficient permissions. Example: `/mv old.txt new.txt`
- /stat <path> - Displays filesystem metadata including owner and permissions. Example: `/stat secrets.txt`

### Filesystem

The default filesystem when you first login is `/filesystem/root`.

tux includes a UNIX-like permission system with:
- File ownership
- Read (`r`)
- Write (`w`)
- Execute (`x`) permissions
- Directory traversal permissions
- Root permission bypass via `/sudo-login`

Permissions are stored numerically in standard UNIX format:
- `700` = owner can read/write/execute
- `755` = owner full access, others read/execute
- `644` = owner read/write, others read-only

By default:
- `/filesystem` is protected and immutable
- `/filesystem/root` is root-owned and restricted
- Newly created files are usually `600`
- Newly created directories are usually `700`

Directory traversal requires execute (`x`) permission on parent directories.

### Sudo
Some commands require `sudo` permissions by default. In order to gain sudo permissions, use the command `/sudo-login <password>`. By default, the password is `root`; however, it is **HIGHLY** recommended that you change the root password in `rootpassword.sk` in the `system` folder of tux in order to prevent unauthorized usage of **SERVER CONSOLE** commands. **tux developers are not responsible for the damages caused by root password negligence!**

## Q&A

**Q**: The filesystem isn’t saving after a server restart. Why?

`tux` uses an in-memory filesystem by default. We do have plans for persistent file storage, but only in a later version.

**Q:** Can I create new users or groups?

tux currently supports file ownership and UNIX-style permissions, but does not yet implement full user or group management.

At the moment:
- Players automatically own files they create
- `/chmod` can modify permissions
- `/chown` can change ownership (root only)
- `/sudo-login` provides temporary root access

Group permissions and multi-user account management are planned for a future release.

**Q:** Commands aren’t working after installation.

Ensure:
- Skript is installed and up to date.
- You’ve reloaded Skript (/skript reload all).
- You’re using a Paper-compatible server (Spigot/Bukkit may work but aren’t officially supported).

Otherwise, submit a bug report in issues.

**Q:** I get "Invalid path" errors.

Paths are case-sensitive and must use `/` (not `\`). Example: `/cd /filesystem/root` (correct) vs. `/cd \filesystem\root` (incorrect).

**Q:** Why the name "tux"?

A: "Tux" is the official mascot of Linux, as this project is heavily based on and inspired by Linux. It also worked the best with ASCII in comparison to other names in the first ever developed application: `/fastfetch`. It is lowercase intentionally for uniformity across applications in tux. And most importantly, it’s cute.

**Q:** tux doesn't work on older versions of Paper/Skript. Can you port it to older versions?

Compatibility with older versions may be limited due to changes in Skript/Paper APIs. We might be able to port a version of tux to earlier Paper/Skript versions, but don't hold your breath for it.

## Copyright

This project is licensed under the GNU General Public License v3.0 or later (GPL-3.0-or-later). See the LICENSE file for details.
By contributing to this project, you agree that your contributions will be licensed under the same terms.
The name "tux" and related branding are not affiliated with or endorsed by the Linux Foundation.

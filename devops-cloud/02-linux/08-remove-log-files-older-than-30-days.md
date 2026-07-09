## Question  
How do you find and remove log files older than 30 days using `-exec` in a folder?

### 📝 Short Explanation  
This version of the task evaluates your comfort with `find -exec`, which is helpful when you want to take specific actions on matched files (like logging or conditional deletion).

## ✅ Answer  
You can use `-exec rm` with `find` to remove log files older than 30 days:

```bash
sudo find /path/to/folder -type f -name "*.log" -mtime +30 -exec rm -f {} \;
```

### 📘 Detailed Explanation  

#### 🔍 Breakdown of the command:
- `sudo`: Used if the directory (like `/var/log`) requires root access.
- `find`: The base command to search files.
- `/path/to/folder`: Replace with your target directory (e.g., `/var/log`).
- `-type f`: Ensures only files are matched.
- `-name "*.log"`: Filters files ending with `.log`.
- `-mtime +30`: Filters files modified **over 30 days ago**.
- `-exec rm -f {} \;`: Executes the `rm -f` command on each matched file:
  - `{}` gets replaced by the current file path.
  - `\;` indicates the end of the command.

---

#### ✅ Example:
```bash
sudo find /var/log -type f -name "*.log" -mtime +30 -exec rm -f {} \;
```

This command will delete all `.log` files in `/var/log` older than 30 days.

---

#### 🧠 Bonus Tip – Dry run before delete:
You can review the files that would be deleted:
```bash
find /var/log -type f -name "*.log" -mtime +30 -exec ls -lh {} \;
```

---

> Summary:  
> Using `-exec` gives you fine-grained control over file operations. It's especially useful when you want to extend the logic beyond simple deletion, such as archiving or compressing matched files.

---
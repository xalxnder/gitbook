# Searching

**Locate**

If you're going to use this, make sure you have a cron job set up to update the database manually

**Find**

One of the most powerful tools in Linux. You can use the `find` command to search for files and directories based on their permissions, type, date, ownership, size, and more.

```bash
# Search for a file named `document.pdf` in the `/home/linuxize` directory
find /home/linuxize -type f -name document.pdf
```

The `exec` option lets us run commands on whatever file we just found.

```bash
# Search for a file named `document.pdf` in the `/home/linuxize` directory, and then change its permissions. 
find /home/linuxize -type f -name document.pdf -exec chmod 0755 {} \;
```

The `{}` is the results placeholder, and the `;` is the delimiter. The `\` is just used to escape it B

# Rsync

Basic Syntax

```
rsync [options] SOURCE DESTINATION
```

***

### 📁 Local to Local

```
rsync -av /home/user/docs/ /home/user/backup/
```

* `-a`: archive mode (preserves permissions, timestamps, symbolic links, etc.)
* `-v`: verbose

> **Trailing slash `/` matters**\
> `/docs/` → syncs contents of `docs/` into `backup/`\
> `/docs` → syncs `docs` itself into `backup/`

***

### 🌐 Local to Remote

```
rsync -av /home/user/photos/ alice@server.example.com:/home/alice/photos_backup/
```

***

### 🌐 Remote to Local

```
rsync -av bob@remote.example.org:/var/www/ /home/bob/website_backup/
```

***

### ♻️ Common Options

| Option      | Description                                        |
| ----------- | -------------------------------------------------- |
| `-a`        | Archive mode (recursive + preserve everything)     |
| `-v`        | Verbose output                                     |
| `-z`        | Compress file data during the transfer             |
| `-P`        | Show progress and keep partially transferred files |
| `--delete`  | Delete files in destination not in source          |
| `-e ssh`    | Use SSH for data transfer                          |
| `--dry-run` | Show what would be done without making changes     |

***

### 🔒 Using SSH with Custom Port

```
rsync -av -e "ssh -p 2222" /home/user/music/ carol@musicbox.local:/data/music/
```

***

### 🔍 Dry Run (Preview Changes)

```
rsync -av --dry-run /etc/configs/ /tmp/configs_backup/
```

***

### 🧹 Delete Extraneous Files on Destination

```
rsync -av --delete /srv/appdata/ /backup/appdata/
```

> ⚠️ This will **remove files** in `/backup/appdata/` that are not present in `/srv/appdata/`.

***

### 🚫 Exclude Files or Folders

```
rsync -av --exclude 'node_modules' /home/user/project/ /mnt/storage/project_backup/
```

```
rsync -av --exclude-from='exclude.txt' /home/user/project/ /mnt/storage/project_backup/
```

***

### 🧪 Sync Over SSH with Key

```
rsync -av -e "ssh -i ~/.ssh/id_ed25519" /var/logs/ dan@logs.example.net:/home/dan/remote_logs/
```

***

### 📜 Script-Friendly Mode (Quiet)

```
rsync -az --quiet /opt/scripts/ /opt/scripts_backup/
```

***

### 📈 Show Progress

```
rsync -ah --progress /home/user/videos/ /media/usb/videos_backup/
```

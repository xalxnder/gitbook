# Screen Command

### 📦 What is `screen`?

`screen` is a terminal multiplexer that lets you start a terminal session, detach from it, and return to it later — even after disconnecting from SSH.

***

### 🚀 Basic Commands

#### Start a named session

```bash
screen -S mysession
```

#### Detach from a session

```bash
Ctrl + a, then d
```

#### List sessions

```bash
screen -ls
```

#### Reattach to a session

```bash
screen -r             # If only one session
screen -r mysession   # If named
screen -r 1234        # By PID
```

#### Kill a session (from inside)

```bash
exit
```

Or:

```bash
Ctrl + a, then :quit
```

#### Kill a session (from outside)

```bash
screen -X -S mysession quit
```

***

### 📝 Logging Output

#### Start with logging enabled

```bash
screen -L
```

#### Default log file

* Created in the current directory
* Named `screenlog.0`

#### Manually turn on logging in a session

```bash
Ctrl + a, then :log on
```

#### Change log file name (inside screen)

```bash
Ctrl + a, then :logfile /path/to/mylog.txt
Ctrl + a, then :log on
```

***

### 🧙‍♂️ Tips

* Sessions survive SSH disconnects!
* Use `screen -S` to name sessions and avoid confusion.
* Use `Ctrl + a, then ?` to see more shortcuts inside a session.

***

### 🔧 Optional `.screenrc` Settings

```bash
deflog on
logfile $HOME/logs/screenlog.%t
```

This auto-logs every session with a timestamped filename.

***

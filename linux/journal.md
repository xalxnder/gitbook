# Journal

The systemd-journald service stores log messages in the journal, a binary file that is temporarily stored in the file `/run/log/journal`. If you want to see the last messages that have been logged, you can use `journalctl -f`, which shows the last lines of the messages where new log lines are automatically added. You can also type journalctl and use (uppercase) G to go to the end of the journal. Also note that the search options / and ? work in the journalctl output.

| Command                                                              | Description                                                                                                          |
| -------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| `journalctl`                                                         | Displays the entire system journal.                                                                                  |
| `journalctl -f`                                                      | Follows the journal logs in real time (like `tail -f`).                                                              |
| `journalctl -u <unit>`                                               | Shows logs for a specific systemd unit (e.g., `journalctl -u nginx`).                                                |
| `journalctl -b`                                                      | Displays logs from the current boot.                                                                                 |
| `journalctl -b -1`                                                   | Shows logs from the previous boot.                                                                                   |
| `journalctl --since "1 hour ago"`                                    | Shows logs from the last hour.                                                                                       |
| `journalctl --since YYYY-MM-DD HH:MM:SS --until YYYY-MM-DD HH:MM:SS` | Displays logs within a specific time range.                                                                          |
| `journalctl -p <priority>`                                           | Filters logs by priority (e.g., `0`=emerg, `1`=alert, `2`=crit, `3`=err, `4`=warn, `5`=notice, `6`=info, `7`=debug). |
| `journalctl -k`                                                      | Shows only kernel logs.                                                                                              |
| `journalctl --disk-usage`                                            | Displays the amount of disk space used by the journal.                                                               |
| `journalctl --vacuum-size=100M`                                      | Shrinks journal logs to the specified size.                                                                          |
| `journalctl --vacuum-time=2d`                                        | Deletes journal logs older than 2 days.                                                                              |

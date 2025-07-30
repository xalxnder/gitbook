# Grep

### Grep

This is the ultimate utility to use WITH regex

> 💡 When using grep with regular expression, wrap the regex in quotes.

| Option | Use                                                             |
| ------ | --------------------------------------------------------------- |
| -i     | Not case sensitive. Matches upper- and lowercase letters.       |
| -v     | Shows only lines that do not contain the regular expression.    |
| -r     | Searches files in the current directory and all subdirectories. |
| -e     | Searches for lines matching more than one regular expression.   |
| -A     | Shows of lines after the matching regular expression.           |
| -B     | Shows of lines before the matching regular expression.          |
| -l     | Show ONLY matching filenames, and not the contents              |

#### Examples

```
# Display all lines containing the string bash in /etc/passwd
grep bash /etc/passwd

#Display the lines that do NOT contain the string 'nologin'
grep -v nologin /etc/passwd

#Search for the string 'linuxize.com' in all files inside the /etc/directory
grep -r 'linuxize.com' /etc

#Searh for the string linux at the beginning of the line in file.txt
grep '^linux' file.txt

```

## Display Lines AFTER Found String

`grep -A <number_of_lines> "search_string" filename`

[grep.md](grep.md "mention")

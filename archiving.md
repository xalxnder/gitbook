# Archiving

## Archiving with Tar

#### Create

`tar -cf {archive} {what you are archiving}`

#### Extract

Order matters. The -f flag must come last because it is expecting a file `tar -xf {archive} {what you are archiving}`

**Viewing Contents**

`tar -tf filename.tar.gz`

#### Options

| Option | Use                                                                   |
| ------ | --------------------------------------------------------------------- |
| c      | Creates an archive.                                                   |
| v      | Shows verbose output while tar is working.                            |
| t      | Shows the contents of an archive.                                     |
| z      | Compresses/decompresses the archive while creating it, by using gzip. |
| j      | Compresses/decompresses the archive by using bzip2.                   |
| x      | Extracts an archive.                                                  |
| u      | Updates an archive; only newer files will be written to the archive.  |
| C      | Changes the working directory before performing the command.          |
| r      | Appends files to an archive.                                          |

#### Compression

**gzip**

gzip `filename`. To uncompress, use gunzip

**bzip2**

bzip `filename`]\(<## Archiving and Compression

```
ARCHIVING AND COMPRESSING ARE NOT THE SAME THING
```

#### Archiving with Tar

To create an archive, you use `tar -cf flename.tar files-you-want-to-archive` . To see whats happening, use the `-v` option. To use tar, you must at least have read permissions. To add a file to an archive, use the `-r` option. To update an existing archived file, use `-u`. So, use `tar -uvf /root/homes.tar /home` to write newer versions of all files in /home to the archive. To see the contents of an archive, sue `-t`, so `tar -tvf /root/homes.tar` to see the contents of the tar archive. To extract the contents of an archive, use `tar -xvf /archivename.tar`. This extracts the archive in the current directory. This might not be what you want. To get around this, you can :

1. cd to a new directory
2. Use the `-C /targetdir` option.
   1. \`\` tar -xvf homes.tar -C /tmp To extract a single file, use `tar -xvf /archivename.tar file-you-want-to-extract`

| Option | Use                                                                   |
| ------ | --------------------------------------------------------------------- |
| c      | Creates an archive.                                                   |
| v      | Shows verbose output while tar is working.                            |
| t      | Shows the contents of an archive.                                     |
| z      | Compresses/decompresses the archive while creating it, by using gzip. |
| j      | Compresses/decompresses the archive by using bzip2.                   |
| x      | Extracts an archive.                                                  |
| u      | Updates an archive; only newer files will be written to the archive.  |
| C      | Changes the working directory before performing the command.          |
| r      | Appends files to an archive.                                          |


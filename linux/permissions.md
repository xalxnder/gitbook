# Permissions

### Understanding Read, Write, and Execute

| **Permission** | **Applied To Files**      | **Applied to Directories** |
| -------------- | ------------------------- | -------------------------- |
| Read           | Open a file               | List contents of directory |
| Write          | Change contents of a file | Create and delete files    |
| Execute        | Run a program file        | Change to the directory    |

#### Applying The Permissions

To apply the above permissions, use `chmod`. There are two modes for chmod

1. Absolute Mode - Use digits. Not my favorite
2. Relative Mode - Use letters



| **Permission** | **Numeric Representation** |
| -------------- | -------------------------- |
| Read           | 4                          |
| Write          | 2                          |
| Execute        | 1                          |

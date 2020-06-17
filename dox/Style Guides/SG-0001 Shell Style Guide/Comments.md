# Comments {#ref_comments}

## Shebang {#ref_shebang}

### Rule 1.1

Do put **shebang** at the beginning of a script file.

Why? On UNIX-like systems, scripts should always start with a shebang line. The system call "execve" (that is responsible
for starting programs) relies on an executable, having either an executable header or a shebang line.

Why? If the file has executable permissions, but no shebang line and does seem a text file, the behaviour depends on the
shell that you're running in. Since there is no guarantee that the script was actually written for that shell, this can work
or fail spectacularly.

```
#!/bin/bash
```

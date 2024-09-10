**Linux Commands to check**

1. chmod --> Used to change the permissions for the file/directory
2. chown --> Used to change user/group permission to file/directory
3. top   --> Prints all the CPU % info , Memory % info , PIDs (gives a wholistic view of all the process running)
4. nproc --> prints no of CPU cores used by Linux machine
5. df -h   --> prints free disc space present in the system
6. free    --> prints info regarding free memory and swap memory
7. ps -ef  --> Gives details info regarding all the processes running
8. awk  --> used to get particular output 
9. find  --> finds the path of a file
10. if loops and for loops
11. set -x set -e set -o
12. curl
13. wget
14. curl vs wget
15. man --> command to get help on any command
16. symlinks vs hardlinks
17. default permissions of a file when it is created - 666 - rw-rw-rw-
18. head 
19. tail
20. mount (lists all the mounts on the current system)
21. redirection commands(>,<)
22. uname - provides Linux kernel info
23. du --> command to check disk usage directory wise

-------------------------------------------------------------------------------------------------------------------------

### Chmod

`chmod` is a command used in Unix and Unix-like operating systems (such as Linux and macOS) to change the permissions of files and directories. The name stands for "change mode."

Here’s a quick overview of how it works:

### Syntax
```bash
chmod [options] mode file
```

### Modes

1. **Symbolic Mode**: Uses letters to represent permissions.
   - `r` stands for read
   - `w` stands for write
   - `x` stands for execute
   - `+` adds a permission
   - `-` removes a permission
   - `=` sets the permission explicitly

   **Examples:**
   - `chmod u+x file` – Adds execute permission for the user (owner) of the file.
   - `chmod go-r file` – Removes read permission for group and others.
   - `chmod u=rwx,g=rx,o=r file` – Sets specific permissions for user, group, and others.

2. **Numeric Mode**: Uses numbers to represent permissions.
   - `4` stands for read
   - `2` stands for write
   - `1` stands for execute
   - Permissions are set by summing these values. For example, `7` is read (4) + write (2) + execute (1), so `chmod 755 file` sets read, write, and execute for the owner and read and execute for group and others.

   **Examples:**
   - `chmod 755 file` – Sets the permissions to rwxr-xr-x (read, write, execute for owner; read, execute for group and others).
   - `chmod 644 file` – Sets the permissions to rw-r--r-- (read, write for owner; read-only for group and others).

### Options
- `-R` – Applies changes recursively to directories and their contents.

**Example:**
```bash
chmod -R 755 directory
```
This command will set the permissions of the directory and all files and subdirectories within it to `rwxr-xr-x`.

Always use `chmod` carefully, especially with the recursive option, to avoid inadvertently changing permissions in a way that might compromise security or functionality.


--------------------------------------------------------------------------------------------------------------------------------

### Chown

The `chown` command in Unix and Unix-like operating systems (such as Linux and macOS) is used to change the ownership of files and directories. The name stands for "change owner."

### Syntax
```bash
chown [options] new_owner[:new_group] file
```

### Components

- **`new_owner`**: The username or user ID of the new owner.
- **`new_group`** (optional): The group name or group ID of the new group. If specified, the file's group will be changed to this group.
- **`file`**: The file or directory whose ownership you want to change.

### Examples

1. **Change Owner Only:**
   ```bash
   chown alice file.txt
   ```
   Changes the owner of `file.txt` to user `alice`, while keeping the current group unchanged.

2. **Change Owner and Group:**
   ```bash
   chown bob:admins file.txt
   ```
   Changes the owner of `file.txt` to user `bob` and the group to `admins`.

3. **Change Group Only:**
   ```bash
   chown :staff file.txt
   ```
   Changes only the group of `file.txt` to `staff`, leaving the owner unchanged.

4. **Recursive Ownership Change:**
   ```bash
   chown -R alice:admins /home/alice
   ```
   Changes the owner to `alice` and the group to `admins` for `/home/alice` and all its contents, including subdirectories and files.

### Note

- You usually need superuser (root) privileges to change ownership of files you do not own. Use `sudo` with `chown` if you do not have the necessary permissions:

  ```bash
  sudo chown alice:admins file.txt
  ```

Changing ownership can affect file access and permissions, so be careful when making these changes, especially on shared or system files.

-------------------------------------------------------------------------------------------------------------------------------

### TOP

The `top` command is a widely used utility in Unix and Unix-like operating systems for monitoring system performance in real-time. It provides a dynamic, real-time view of the system’s processes and resource usage, making it useful for diagnosing performance issues and understanding system load.

### Basic Usage
```bash
top
```

When you run `top`, it displays an interactive, updating list of processes, along with system information.

### Key Sections

1. **Summary Area** (top of the screen):
   - **System Information**: Includes uptime, load averages, and the number of users.
   - **CPU Usage**: Displays the percentage of CPU usage by user, system, and idle time.
   - **Memory Usage**: Shows total, used, and free memory and swap space.

2. **Process List** (below the summary area):
   - **PID**: Process ID.
   - **USER**: The user who owns the process.
   - **PR**: Process priority.
   - **NI**: Nice value (affects priority).
   - **VIRT**: Virtual memory used by the process.
   - **RES**: Resident memory (physical RAM) used by the process.
   - **SHR**: Shared memory.
   - **S**: Process status (e.g., running, sleeping).
   - **%CPU**: CPU usage percentage.
   - **%MEM**: Memory usage percentage.
   - **TIME+**: Total CPU time used by the process.
   - **COMMAND**: The command or process name.


`top` is a powerful tool for real-time system monitoring and is particularly useful for troubleshooting performance issues and understanding system load.
------------------------------------------------------------------------------------------------------------------------
### ps -ef 

The `ps` command in Unix and Unix-like operating systems is used to display information about active processes. The `-ef` options are commonly used together to provide a comprehensive view of all processes running on the system.

### Syntax
```bash
ps -ef
```

### Options

- **`-e`** or **`-A`**: Show all processes running on the system.
- **`-f`**: Full format listing. This provides a more detailed view compared to the default output, including additional columns.

### Output Columns

When you run `ps -ef`, you'll typically see the following columns:

- **`UID`**: User ID of the process owner.
- **`PID`**: Process ID of the running process.
- **`PPID`**: Parent Process ID. This indicates the PID of the parent process.
- **`C`**: CPU utilization of the process.
- **`STIME`**: Start time of the process.
- **`TTY`**: Terminal associated with the process (if any).
- **`TIME`**: Cumulative CPU time used by the process.
- **`CMD`**: Command that started the process.

### Example Output
Here’s an example of what the output might look like:

```
UID        PID  PPID  C STIME TTY          TIME CMD
root         1     0  0 Sep10 ?        00:00:05 /sbin/init
user       256     1  0 Sep10 pts/0    00:00:00 bash
user       789   256  0 Sep10 pts/0    00:00:00 ps -ef
```

### Example Commands

- **List all processes:**
  ```bash
  ps -ef
  ```

- **Find processes for a specific user (e.g., `username`):**
  ```bash
  ps -ef | grep username
  ```

- **Find a specific process by name (e.g., `apache2`):**
  ```bash
  ps -ef | grep apache2
  ```

- **View processes with more readable start times:**
  ```bash
  ps -ef --sort=start_time
  ```

### Notes

- The `ps` command displays a snapshot of processes at the time it is run. For continuous monitoring, tools like `top` or `htop` might be more appropriate.
- The `ps -ef` output includes processes owned by all users and might require root or superuser privileges to see some processes.

Using `ps -ef` is a great way to get a comprehensive snapshot of the current processes on a system, including details about how processes are related to each other.

----------------------------------------------------------------------------------------------------------------------------------
### awk

`awk` is a powerful programming language and command-line utility used for pattern scanning and processing. It's particularly useful for text processing and data extraction from files or streams of text. Named after its creators—Al Aho, Peter Weinberger, and Brian Kernighan—`awk` is often used in shell scripting and command-line operations.

### Basic Syntax
```bash
awk 'pattern { action }' file
```

- **`pattern`**: A condition or pattern that determines which lines to process.
- **`action`**: The operation to perform on lines that match the pattern.
- **`file`**: The input file to process. If omitted, `awk` reads from standard input.

### Basic Examples

1. **Print Entire File:**
   ```bash
   awk '{ print }' file.txt
   ```
   This prints each line of `file.txt`. The `{ print }` action is the default and can be omitted.

2. **Print Specific Field:**
   ```bash
   awk '{ print $1 }' file.txt
   ```
   This prints the first field of each line, assuming fields are separated by whitespace.

3. **Print Lines Matching a Pattern:**
   ```bash
   awk '/pattern/ { print }' file.txt
   ```
   This prints lines that contain the word "pattern".

4. **Sum of a Column:**
   ```bash
   awk '{ sum += $1 } END { print sum }' file.txt
   ```
   This sums the values in the first column and prints the result after processing all lines.

5. **Print Specific Field with Separator:**
   ```bash
   awk -F, '{ print $2 }' file.csv
   ```
   This prints the second field of a CSV file where fields are separated by commas.

### Built-in Variables

- **`$0`**: Represents the entire current line.
- **`$1`, `$2`, ...**: Represents the fields of the current line (where `$1` is the first field, `$2` is the second field, etc.).
- **`NR`**: The number of records (lines) read so far.
- **`NF`**: The number of fields in the current record.
- **`FS`**: The field separator (default is whitespace). You can set it with `-F` option or inside `awk` script.

### Advanced Usage

1. **Using a Field Separator:**
   ```bash
   awk -F":" '{ print $1, $3 }' /etc/passwd
   ```
   This prints the first and third fields from the `/etc/passwd` file, using a colon as the field separator.

2. **Formatting Output:**
   ```bash
   awk '{ printf "%-10s %-5s\n", $1, $2 }' file.txt
   ```
   This formats the output with columns of fixed width.

3. **Processing Multiple Files:**
   ```bash
   awk '{ print FILENAME ": " NR ": " $0 }' file1.txt file2.txt
   ```
   This prints the filename, line number, and line content for each line in both files.

4. **Conditional Actions:**
   ```bash
   awk '$3 > 50 { print $1, $3 }' file.txt
   ```
   This prints the first and third fields of lines where the third field is greater than 50.

### Summary

`awk` is highly versatile for text processing and data manipulation, making it a valuable tool for tasks ranging from simple field extraction to complex data analysis and reporting. Its power lies in its ability to handle fields and patterns efficiently, allowing for sophisticated text processing directly from the command line or within scripts.

---------------------------------------------------------------------------------------------------------------
### find

The `find` command is a powerful utility in Unix and Unix-like operating systems used to search for files and directories in a directory hierarchy based on various criteria. It's extremely versatile and can perform a wide range of searches and operations on files.

### Basic Syntax
```bash
find [path] [expression]
```
- **`path`**: The directory where the search starts. If omitted, it defaults to the current directory.
- **`expression`**: Specifies search criteria and actions. Expressions can include options, tests, and actions.

### Common Usage

1. **Find Files by Name**
   ```bash
   find /path/to/search -name "filename"
   ```
   Finds files with the exact name `filename` in `/path/to/search` and its subdirectories.

   **Example:**
   ```bash
   find /home/user -name "report.txt"
   ```

2. **Find Files by Extension**
   ```bash
   find /path/to/search -name "*.ext"
   ```
   Finds all files with the `.ext` extension.

   **Example:**
   ```bash
   find /var/log -name "*.log"
   ```

3. **Find Files by Type**
   ```bash
   find /path/to/search -type [f|d|l]
   ```
   - **`-type f`**: Finds regular files.
   - **`-type d`**: Finds directories.
   - **`-type l`**: Finds symbolic links.

   **Example:**
   ```bash
   find /etc -type d
   ```

4. **Find Files by Size**
   ```bash
   find /path/to/search -size [+-]size
   ```
   - **`-size +100M`**: Finds files larger than 100MB.
   - **`-size -10k`**: Finds files smaller than 10KB.

   **Example:**
   ```bash
   find /home/user -size +500M
   ```

5. **Find Files by Modification Time**
   ```bash
   find /path/to/search -mtime [+|-]n
   ```
   - **`-mtime +7`**: Files modified more than 7 days ago.
   - **`-mtime -1`**: Files modified in the last 24 hours.

   **Example:**
   ```bash
   find /var/tmp -mtime -7
   ```

6. **Find Files by Permissions**
   ```bash
   find /path/to/search -perm mode
   ```
   - **`-perm 644`**: Finds files with permissions set to 644.

   **Example:**
   ```bash
   find /home/user -perm 755
   ```

7. **Execute Commands on Found Files**
   ```bash
   find /path/to/search -name "filename" -exec command {} \;
   ```
   - **`{}`**: Placeholder for the current file name.
   - **`\;`**: Indicates the end of the command to be executed.

   **Example:**
   ```bash
   find /home/user -name "*.tmp" -exec rm {} \;
   ```
   This finds all `.tmp` files and removes them.

8. **Find and Print File Information**
   ```bash
   find /path/to/search -name "filename" -print
   ```
   Prints the path of each found file. This is the default action when no other action is specified.

   **Example:**
   ```bash
   find /usr -name "*.conf" -print
   ```

### Combining Expressions

You can combine multiple criteria using logical operators:

- **`-and`**: Default operator, can be omitted.
- **`-or`**: Logical OR.
- **`-not`** or **`!`**: Logical NOT.

**Example:**
```bash
find /path/to/search -type f -and -name "*.txt" -or -name "*.md"
```
Finds files that are either `.txt` or `.md` files.

### Example Use Cases

1. **Find all files with `.log` extension modified in the last 30 days:**
   ```bash
   find /var/log -name "*.log" -mtime -30
   ```

2. **Find and delete all `.bak` files:**
   ```bash
   find /home/user -name "*.bak" -exec rm {} \;
   ```

3. **Find empty directories:**
   ```bash
   find /path/to/search -type d -empty
   ```

### Summary

The `find` command is an essential tool for file system management and scripting. It provides powerful search capabilities and allows for complex querying and operations on files and directories. Understanding and mastering `find` can greatly enhance your efficiency in managing files on Unix-like systems.

---------------------------------------------------------------------------------------------------------------------------------
### curl

`curl` is a command-line tool used for transferring data to or from a server using various network protocols. It is highly versatile and supports a wide range of protocols including HTTP, HTTPS, FTP, FTPS, SCP, SFTP, LDAP, and more. `curl` is commonly used for downloading files, interacting with APIs, and testing server responses.

### Basic Syntax
```bash
curl [options] [URL]
```

### Common Usage

#### Download a File
```bash
curl -O [URL]
```
- **`-O`**: Saves the file with its original name from the URL.

  **Example:**
  ```bash
  curl -O https://example.com/file.zip
  ```

#### Download a File and Save with a Different Name
```bash
curl -o [filename] [URL]
```
- **`-o`**: Saves the file with the specified name.

  **Example:**
  ```bash
  curl -o myfile.zip https://example.com/file.zip
  ```

#### Display Response in Terminal
```bash
curl [URL]
```
This fetches the content of the URL and displays it in the terminal.

  **Example:**
  ```bash
  curl https://api.github.com
  ```

#### Follow Redirects
```bash
curl -L [URL]
```
- **`-L`**: Follow HTTP redirects.

  **Example:**
  ```bash
  curl -L http://example.com/redirect
  ```

#### Send HTTP GET Request
```bash
curl -X GET [URL]
```
- **`-X GET`**: Specifies the HTTP method. GET is the default method, so this is often optional.

  **Example:**
  ```bash
  curl -X GET https://api.example.com/data
  ```

#### Send HTTP POST Request with Data
```bash
curl -X POST -d "param1=value1&param2=value2" [URL]
```
- **`-X POST`**: Specifies the HTTP POST method.
- **`-d`**: Sends the specified data in the POST request.

  **Example:**
  ```bash
  curl -X POST -d "name=John&age=30" https://example.com/api
  ```

#### Send JSON Data in POST Request
```bash
curl -X POST -H "Content-Type: application/json" -d '{"key1":"value1", "key2":"value2"}' [URL]
```
- **`-H`**: Adds an HTTP header.
- **`-d`**: Sends JSON data in the POST request.

  **Example:**
  ```bash
  curl -X POST -H "Content-Type: application/json" -d '{"name":"John","age":30}' https://example.com/api
  ```

#### Include HTTP Headers in Output
```bash
curl -i [URL]
```
- **`-i`**: Includes HTTP headers in the output.

  **Example:**
  ```bash
  curl -i https://example.com
  ```

#### Show Only HTTP Headers
```bash
curl -I [URL]
```
- **`-I`**: Fetches only the HTTP headers.

  **Example:**
  ```bash
  curl -I https://example.com
  ```

#### Basic Authentication
```bash
curl -u username:password [URL]
```
- **`-u`**: Provides the username and password for basic HTTP authentication.

  **Example:**
  ```bash
  curl -u user:pass https://example.com/protected
  ```

#### Download a File with Progress Bar
```bash
curl -O [URL] --progress-bar
```
- **`--progress-bar`**: Shows a progress bar during the download.

  **Example:**
  ```bash
  curl -O https://example.com/largefile.zip --progress-bar
  ```

### Example Use Cases

1. **Download a file and save it with a different name:**
   ```bash
   curl -o newname.zip https://example.com/file.zip
   ```

2. **Submit a form via POST request:**
   ```bash
   curl -X POST -d "name=John&age=30" https://example.com/form
   ```

3. **Fetch JSON data from an API:**
   ```bash
   curl -H "Accept: application/json" https://api.example.com/data
   ```

4. **Authenticate and download a protected resource:**
   ```bash
   curl -u user:pass -O https://example.com/protected/resource.zip
   ```

5. **Check HTTP headers of a URL:**
   ```bash
   curl -I https://example.com
   ```

### Summary

`curl` is a highly flexible and powerful tool for interacting with network resources and APIs. Its broad support for protocols and various options make it an essential tool for web development, debugging, and system administration tasks. Understanding its capabilities can greatly enhance your ability to work with networked resources from the command line.

--------------------------------------------------------------------------------------------------------------------------------------

### curl vs wget

`curl` and `wget` are both popular command-line tools used for downloading files from the web and interacting with web services. Despite their similar purposes, they have different features and use cases. Here’s a detailed comparison of `curl` and `wget`:

### **Overview**

- **`curl`**: Primarily used for transferring data to or from a server. It supports a wide range of protocols and is highly configurable. `curl` is often used in scripting and automation for interacting with APIs and web services.

- **`wget`**: Primificalliy designed for downloading files from the web. It is more oriented towards recursive downloading and handling large numbers of files. It is often used for mirroring websites or downloading large datasets.

### **Features and Usage**

#### **Basic Download**

- **`curl`**:
  ```bash
  curl -O http://example.com/file.zip
  ```
  - **`-O`**: Saves the file with its original name.

- **`wget`**:
  ```bash
  wget http://example.com/file.zip
  ```
  - Downloads the file with its original name.

#### **Recursive Download**

- **`curl`**:
  - `curl` does not natively support recursive downloading. You would need to use additional scripting or tools to achieve this.

- **`wget`**:
  ```bash
  wget -r http://example.com/directory/
  ```
  - **`-r`**: Recursively download files from a directory.

#### **Resume Download**

- **`curl`**:
  ```bash
  curl -C - -O http://example.com/file.zip
  ```
  - **`-C -`**: Resumes a partially downloaded file.

- **`wget`**:
  ```bash
  wget -c http://example.com/file.zip
  ```
  - **`-c`**: Continues a partially downloaded file.

#### **Support for Multiple Protocols**

- **`curl`**:
  - Supports a wide range of protocols including HTTP, HTTPS, FTP, FTPS, SCP, SFTP, LDAP, and more.

  ```bash
  curl -u user:password ftp://example.com/file.zip
  ```

- **`wget`**:
  - Primarily supports HTTP, HTTPS, and FTP. It is not as versatile with protocols as `curl`.

  ```bash
  wget ftp://example.com/file.zip
  ```

#### **Handling HTTP Headers**

- **`curl`**:
  ```bash
  curl -I http://example.com
  ```
  - **`-I`**: Fetches only the HTTP headers.

- **`wget`**:
  ```bash
  wget --server-response http://example.com
  ```
  - **`--server-response`**: Prints server responses and HTTP headers.

#### **Form Submission**

- **`curl`**:
  ```bash
  curl -X POST -d "param1=value1&param2=value2" http://example.com/form
  ```
  - **`-X POST`**: Specifies the POST method.
  - **`-d`**: Sends form data.

- **`wget`**:
  ```bash
  wget --post-data="param1=value1&param2=value2" http://example.com/form
  ```
  - **`--post-data`**: Sends POST data.

#### **Output to a File**

- **`curl`**:
  ```bash
  curl -o newname.zip http://example.com/file.zip
  ```
  - **`-o`**: Saves the file with a specified name.

- **`wget`**:
  ```bash
  wget -O newname.zip http://example.com/file.zip
  ```
  - **`-O`**: Saves the file with a specified name.

#### **Progress and Logging**

- **`curl`**:
  ```bash
  curl -O http://example.com/file.zip --progress-bar
  ```
  - **`--progress-bar`**: Shows a progress bar.

- **`wget`**:
  ```bash
  wget --progress=bar http://example.com/file.zip
  ```
  - **`--progress=bar`**: Shows a progress bar.

### **Summary**

- **`curl`**: 
  - Best for interacting with APIs and performing complex data transfers.
  - Supports a wider range of protocols.
  - More suitable for tasks requiring HTTP headers, form submission, and other advanced features.

- **`wget`**:
  - Best for downloading files and mirroring websites.
  - Built-in support for recursive downloads and resuming interrupted downloads.
  - Better suited for bulk downloading and handling large datasets.

Both tools are highly capable, and the choice between them depends on the specific requirements of the task at hand. For general file downloads and mirroring, `wget` is often preferred, while `curl` shines in scenarios involving advanced interactions with web services and APIs.


---------------------------------------------------------------------------------------------------------------------------------------
### symlinks vs hardlinks

do practical implementation to understand better

### head

The `head` command is a Unix and Unix-like utility used to display the beginning of a file or input from a pipeline. By default, `head` shows the first 10 lines of each file provided as input, but you can customize this behavior with various options.

### Basic Syntax
```bash
head [options] [file...]
```

- **`[options]`**: Optional flags to modify the behavior of `head`.
- **`[file...]`**: The file(s) you want to read. If no file is specified, `head` reads from the standard input.

### Common Options

1. **Display the First 10 Lines (Default Behavior)**
   ```bash
   head filename
   ```
   Displays the first 10 lines of `filename`.

### Examples

1. **View the First 10 Lines of a File:**
   ```bash
   head /var/log/syslog
   ```

2. **View the First 15 Lines of a File:**
   ```bash
   head -n 15 /etc/passwd
   ```

3. **View the First 50 Bytes of a File:**
   ```bash
   head -c 50 /usr/bin/somebinary
   ```

4. **View the First 20 Lines of Multiple Files:**
   ```bash
   head -n 20 file1 file2
   ```

5. **View the First 10 Lines of Output from a Command:**
   ```bash
   dmesg | head
   ```

6. **View the First 100 Bytes of Input from a Pipe:**
   ```bash
   cat somefile | head -c 100
   ```

### Summary

The `head` command is a simple yet powerful utility for viewing the beginning portion of files or output streams. Its ability to customize the number of lines or bytes displayed and handle multiple files makes it versatile for various text processing tasks.

--------------------------------------------------------------------------------------------------------------------------
### tail

The `tail` command in Unix and Unix-like operating systems is used to display the end of a file or input from a pipeline. By default, `tail` shows the last 10 lines of each file, but you can customize this behavior with various options.

### Basic Syntax
```bash
tail [options] [file...]
```

- **`[options]`**: Optional flags to modify the behavior of `tail`.
- **`[file...]`**: The file(s) you want to read. If no file is specified, `tail` reads from the standard input.

### Common Options

1. **Display the Last 10 Lines (Default Behavior)**
   ```bash
   tail filename
   ```
   Displays the last 10 lines of `filename`.

### Examples

1. **View the Last 10 Lines of a File:**
   ```bash
   tail /var/log/syslog
   ```

2. **View the Last 15 Lines of a File:**
   ```bash
   tail -n 15 /etc/passwd
   ```

3. **View the Last 50 Bytes of a File:**
   ```bash
   tail -c 50 /usr/bin/somebinary
   ```

4. **Follow a Log File:**
   ```bash
   tail -f /var/log/apache2/access.log
   ```

5. **Follow a Log File with Initial 100 Lines:**
   ```bash
   tail -n 100 -f /var/log/apache2/error.log
   ```

6. **View Lines from a Specific Position:**
   ```bash
   tail -n +20 /etc/passwd
   ```

### Summary

The `tail` command is a powerful utility for viewing the end of files or streams and monitoring real-time updates. Its ability to follow file changes, specify the number of lines or bytes, and handle multiple files makes it an essential tool for system monitoring, debugging, and log analysis.

---------------------------------------------------------------------------------------------------------------------------

### Redirection Commands(<,>,<<,>>)

Redirection in Unix and Unix-like operating systems allows you to control where the output of commands is sent and where input is read from. This is done using various redirection operators. Here’s a comprehensive overview of the different redirection commands and operators:

### **Standard Streams**

- **Standard Input (stdin)**: Typically, input provided to a command.
- **Standard Output (stdout)**: The output produced by a command.
- **Standard Error (stderr)**: The error messages produced by a command.

### **Redirection Operators**

#### **1. Output Redirection**

- **Redirect stdout to a File (`>`):**
  ```bash
  command > file
  ```
  - Redirects the standard output of `command` to `file`, overwriting the file if it exists.

  **Example:**
  ```bash
  ls > directory_list.txt
  ```
  This saves the output of the `ls` command to `directory_list.txt`, overwriting it if it already exists.

- **Append stdout to a File (`>>`):**
  ```bash
  command >> file
  ```
  - Redirects the standard output of `command` to `file`, appending to the file if it exists.

  **Example:**
  ```bash
  echo "New entry" >> log.txt
  ```
  This appends "New entry" to `log.txt`.

#### **2. Input Redirection**

- **Redirect stdin from a File (`<`):**
  ```bash
  command < file
  ```
  - Redirects the standard input of `command` from `file`.

  **Example:**
  ```bash
  sort < unsorted_list.txt
  ```
  This sorts the contents of `unsorted_list.txt`.

- **Here Document (`<<`):**
  ```bash
  command << EOF
  text
  EOF
  ```
  - Provides a block of text (terminated by `EOF` or any other delimiter) as standard input to `command`.

  **Example:**
  ```bash
  cat << EOF
  This is line 1
  This is line 2
  EOF
  ```
  This outputs the specified text to the terminal.

#### **3. Error Redirection**

- **Redirect stderr to a File (`2>`):**
  ```bash
  command 2> file
  ```
  - Redirects the standard error output of `command` to `file`, overwriting the file if it exists.

  **Example:**
  ```bash
  ls non_existent_file 2> error_log.txt
  ```
  This redirects the error message to `error_log.txt`.

- **Append stderr to a File (`2>>`):**
  ```bash
  command 2>> file
  ```
  - Redirects the standard error output of `command` to `file`, appending to the file if it exists.

  **Example:**
  ```bash
  ls non_existent_file 2>> error_log.txt
  ```

- **Redirect stdout and stderr to the Same File (`&>` or `2>&1`):**
  ```bash
  command &> file
  ```
  - Redirects both stdout and stderr to `file`, overwriting the file if it exists.

  **Example:**
  ```bash
  ls / > all_output.txt
  ```

  ```bash
  command > file 2>&1
  ```
  - Redirects stdout to `file` and then redirects stderr to the same place as stdout.

  **Example:**
  ```bash
  ls /non_existent_dir > all_output.txt 2>&1
  ```

#### **4. Pipelines**

- **Pipe (`|`):**
  ```bash
  command1 | command2
  ```
  - Redirects the standard output of `command1` to the standard input of `command2`.

  **Example:**
  ```bash
  ls | grep "pattern"
  ```
  This lists files and pipes the output to `grep` to search for "pattern".

### **Examples of Combining Redirections**

1. **Redirect stdout and stderr to the Same File:**
   ```bash
   ./run_script.sh > output_and_errors.log 2>&1
   ```

2. **Redirect stdout to a File and stderr to a Different File:**
   ```bash
   ./run_script.sh > output.log 2> errors.log
   ```

3. **Append stdout and stderr to the Same File:**
   ```bash
   ./run_script.sh >> output_and_errors.log 2>&1
   ```

4. **Use Here Document to Provide Input:**
   ```bash
   cat << EOF > newfile.txt
   Line 1
   Line 2
   EOF
   ```

5. **Pipe Output to Another Command:**
   ```bash
   ps aux | grep 'process_name'
   ```

### **Summary**

Redirection is a powerful feature in Unix-like systems that allows you to control the flow of data between commands, files, and the terminal. By understanding and using these redirection operators effectively, you can manage output and input streams to suit your needs, automate tasks, and perform complex data processing operations efficiently.

--------------------------------------------------------------------------------------------------------------------------------
### gzip, gunzip and tar 

The `gzip`, `gunzip`, and `tar` commands are essential tools for file compression, decompression, and archiving in Unix and Unix-like operating systems. They often work together in file management tasks. Here’s an overview of each command:

### **`gzip`**

**Description:**
`gzip` (GNU zip) compresses files to reduce their size using the Lempel-Ziv coding (LZ77) algorithm.

**Basic Syntax:**
```bash
gzip [options] [file...]
```

**Common Options:**
- **`-d`**: Decompress files (equivalent to `gunzip`).
- **`-c`**: Write output to standard output.
- **`-k`**: Keep the original file after compression.
- **`-v`**: Verbose mode; displays compression details.
- **`-1` to `-9`**: Set the compression level (1 is fastest, 9 is highest compression).

**Examples:**
1. **Compress a File:**
   ```bash
   gzip file.txt
   ```
   Creates `file.txt.gz` and removes the original `file.txt`.

2. **Compress and Keep the Original File:**
   ```bash
   gzip -k file.txt
   ```
   Creates `file.txt.gz` and keeps `file.txt`.

3. **Decompress a File:**
   ```bash
   gzip -d file.txt.gz
   ```
   Restores `file.txt` from `file.txt.gz`.

4. **Compress to Standard Output:**
   ```bash
   gzip -c file.txt > file.txt.gz
   ```

### **`gunzip`**

**Description:**
`gunzip` is used to decompress files compressed with `gzip`. It is functionally equivalent to `gzip -d`.

**Basic Syntax:**
```bash
gunzip [options] [file...]
```

**Common Options:**
- **`-c`**: Write output to standard output.
- **`-k`**: Keep the original compressed file.
- **`-v`**: Verbose mode; displays decompression details.

**Examples:**
1. **Decompress a File:**
   ```bash
   gunzip file.txt.gz
   ```
   Restores `file.txt` from `file.txt.gz`.

2. **Decompress and Keep the Original File:**
   ```bash
   gunzip -k file.txt.gz
   ```
   Restores `file.txt` while keeping `file.txt.gz`.

3. **Decompress to Standard Output:**
   ```bash
   gunzip -c file.txt.gz | less
   ```

### **`tar`**

**Description:**
`tar` (tape archive) is used to create and manipulate archive files. It combines multiple files into a single archive file, which can then be compressed with `gzip` or other compression tools.

**Basic Syntax:**
```bash
tar [options] [archive-file] [file...]
```

**Common Options:**
- **`-c`**: Create a new archive.
- **`-x`**: Extract files from an archive.
- **`-t`**: List the contents of an archive.
- **`-f`**: Specify the archive file.
- **`-v`**: Verbose mode; shows the progress.
- **`-z`**: Compress the archive using `gzip`.
- **`-j`**: Compress the archive using `bzip2`.
- **`-J`**: Compress the archive using `xz`.

**Examples:**
1. **Create a Tar Archive:**
   ```bash
   tar -cvf archive.tar file1 file2
   ```
   Creates `archive.tar` containing `file1` and `file2`.

2. **Create a Compressed Tar Archive with gzip:**
   ```bash
   tar -czvf archive.tar.gz file1 file2
   ```
   Creates `archive.tar.gz`, which is `archive.tar` compressed with `gzip`.

3. **Extract a Tar Archive:**
   ```bash
   tar -xvf archive.tar
   ```
   Extracts the contents of `archive.tar`.

4. **Extract a Compressed Tar Archive with gzip:**
   ```bash
   tar -xzvf archive.tar.gz
   ```
   Extracts `archive.tar.gz` and decompresses it.

5. **List the Contents of a Tar Archive:**
   ```bash
   tar -tvf archive.tar
   ```
   Lists the contents of `archive.tar`.

6. **List the Contents of a Compressed Tar Archive with gzip:**
   ```bash
   tar -tzvf archive.tar.gz
   ```
   Lists the contents of `archive.tar.gz`.

### **Combining Commands**

`tar` and `gzip` (or `gunzip`) are often used together. You can use `tar` to create an archive and compress it with `gzip` in one step. Similarly, you can decompress and extract in one step.

**Create and Compress in One Step:**
```bash
tar -czvf archive.tar.gz directory/
```

**Decompress and Extract in One Step:**
```bash
tar -xzvf archive.tar.gz
```

### **Summary**

- **`gzip`**: Compresses individual files.
- **`gunzip`**: Decompresses files compressed with `gzip`.
- **`tar`**: Archives multiple files into a single file and can use various compression methods.

These commands are fundamental for managing file archives and compression in Unix-like systems, often used together for efficient storage and transmission of files.

------------------------------------------------------------------------------------------------------------------------------------
### Networking commands

In Linux, daily networking tasks often involve checking network status, configuring interfaces, troubleshooting connectivity, and monitoring network activity. Here’s a comprehensive list of commonly used networking commands that you might use on a daily basis:

### **1. Basic Network Configuration**

- **`ifconfig`**: Displays or configures network interfaces (deprecated, replaced by `ip`).
  ```bash
  ifconfig
  ```

- **`ip`**: Provides detailed network configuration and control.
  ```bash
  ip addr show        # Display network interfaces and their IP addresses
  ip link show        # Show network interfaces
  ip route show       # Display routing table
  ip a               # Short form for `ip addr show`
  ip l               # Short form for `ip link show`
  ip r               # Short form for `ip route show`
  ```

- **`nmcli`**: Command-line tool for NetworkManager to manage network connections.
  ```bash
  nmcli device status         # Show status of network devices
  nmcli connection show       # List network connections
  nmcli device show           # Show detailed information about network devices
  nmcli networking off        # Turn off networking
  nmcli networking on         # Turn on networking
  ```

### **2. Network Status and Connectivity**

- **`ping`**: Sends ICMP ECHO_REQUEST packets to a network host.
  ```bash
  ping example.com         # Ping a domain name
  ping 192.168.1.1         # Ping an IP address
  ping -c 4 example.com    # Ping with a count of 4 packets
  ```

- **`traceroute`**: Traces the route packets take to a network host.
  ```bash
  traceroute example.com   # Trace the route to a domain
  traceroute 8.8.8.8       # Trace the route to an IP address
  ```

- **`tracepath`**: Traces the path to a network host, similar to `traceroute`.
  ```bash
  tracepath example.com
  ```

- **`mtr`**: Combines `ping` and `traceroute` for real-time network diagnostics.
  ```bash
  mtr example.com
  ```

### **3. Network Interfaces**

- **`netstat`**: Displays network connections, routing tables, and interface statistics (deprecated, replaced by `ss`).
  ```bash
  netstat -tuln          # Show listening ports and associated addresses
  netstat -rn            # Show routing table
  netstat -i             # Show network interfaces and statistics
  ```

- **`ss`**: Utility to investigate sockets (modern replacement for `netstat`).
  ```bash
  ss -tuln               # Show listening TCP and UDP ports
  ss -tul                # Show listening TCP and UDP ports with additional details
  ss -r                  # Show routing information
  ```

### **5. DNS and Host Resolution**

- **`nslookup`**: Queries DNS to obtain domain name or IP address information.
  ```bash
  nslookup example.com   # Lookup the IP address for a domain
  ```

- **`dig`**: Provides detailed DNS query information.
  ```bash
  dig example.com        # Query DNS for a domain
  dig -x 8.8.8.8         # Reverse DNS lookup for an IP address
  ```

- **`host`**: Simple utility to perform DNS lookups.
  ```bash
  host example.com       # Lookup the IP address for a domain
  host 8.8.8.8           # Reverse lookup for an IP address
  ```

### **7. Network Services**

- **`systemctl`**: Manages system services, including network services.
  ```bash
  systemctl status NetworkManager      # Check the status of NetworkManager
  systemctl restart NetworkManager     # Restart NetworkManager
  systemctl enable NetworkManager      # Enable NetworkManager to start at boot
  ```

- **`service`**: Older command for managing services.
  ```bash
  service network status     # Check the status of the network service
  service network restart    # Restart the network service
  ```

### **9. Network File Transfer**

- **`scp`**: Securely copy files between hosts over SSH.
  ```bash
  scp file.txt user@remote:/path/to/destination  # Copy file to remote host
  scp user@remote:/path/to/file.txt .             # Copy file from remote host
  ```

- **`rsync`**: Synchronizes files and directories between locations.
  ```bash
  rsync -avz source/ user@remote:/path/to/destination  # Sync files to remote host
  ```

### **Summary**

These commands are vital for various aspects of network management, including configuration, monitoring, and troubleshooting. Familiarity with these commands can help you effectively manage network interfaces, diagnose connectivity issues, and monitor network performance.

----------------------------------------------------------------------------------------------------------
Here's the corrected version of your script to count occurrences of 's' in the string 'mississippi':

bash
Copy code
#!/bin/bash

count=0
var='mississippi'

for (( i=0; i<${#var}; i++ )); do
    if [ "${var:$i:1}" == 's' ]; then
        ((count++))
    fi
done

echo "Count of 's' in 'mississippi': $count"

#var will provide the length of variable
var:$i:1 --> will get the substring of starting from index 'i' and number of letters after index which in this case is one

--------------------------------------------------------------------------------------------------------------------------------

Crontab

Crontab syntax

cron.allow --> Allows which users are permitted to run crontab command
cron.deny --> Denys  which users are permitted to run crontab command


gzip, unzip, tar ---> commands used for backup

disk usage ----> df , du , 

df --> command to check free disk space
du --> command to check disk usage directory wise
dfspace --> free disk space interms of MB

du -sh /home/Mallikarjun --> Total disck space used by user Mallikarjun

du /tmp --> Total disk space used by /tmp folder

Open readonly file --> vi -R file.txt

--------------------------------------------------------------------
For example, to print the 5th line of file.txt, you would use:

sed -n '5p' file.txt

-------------------------------------------------
save output of a command into a file

command > output.txt (this command will remove any existing content in the file and places the output)

ls -l > file_list.txt

command >> output.txt 

This will append the output of command to output.txt. If output.txt does not exist, it will be created.

-----------------------------------------------
how to mail error log file

To mail an error log file in Linux, you can use the mail command along with redirection to send the contents of the log file via email. Here’s a step-by-step guide on how to do this:

Prerequisites
Before proceeding, ensure that your Linux system has a mail server properly configured to send emails. If you haven't set up a mail server, you can use a service like ssmtp or postfix to configure one. Consult your system administrator or refer to your distribution's documentation for details.

Steps to Mail an Error Log File
Compose the Email Body: You'll need to prepare the content of the email you want to send, including the log file content. You can do this by capturing the output of a command or by directly including the contents of a file.

Use mail Command: The mail command is used to send emails from the command line in Linux. Here's the basic syntax:

mail -s "Subject of the Email" recipient@example.com < logfile.txt

-s: Specifies the subject of the email.
recipient@example.com: Replace this with the recipient's email address.
< logfile.txt: This redirects the contents of logfile.txt as the input for the email body.

------------------------------------------------------------------------------
netcat command widely used for debugging, network exploration.

nc <hostname or IP address> <port>

Netstat (Network Statistics):

netstat -tulpn(displays all tcp,udp services listening on ports)

Function: Netstat is a command-line tool used to display network connections, routing tables, interface statistics, masquerade connections, and multicast memberships.
Features:
Shows active network connections (both incoming and outgoing), listening ports, and related networking statistics.
Provides information about the IP addresses and ports to which the computer is connected.
Can display routing table information, including default gateways and routing paths.
Usage: It is primarily used for network troubleshooting, monitoring network activity, and diagnosing network performance issues.

In summary, netstat is used to inspect existing network connections and diagnose network issues, whereas netcat is used to create connections and transfer data over networks, making it more of a Swiss Army knife for network tasks and security testing.


-------------------------------------------------------------------

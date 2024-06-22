**Linux Commands to check**

1. chmod --> Used to change the permissions for the file/directory
2. chown --> Used to change user/group permission to file/directory
3. top   --> Prints all the CPU % info , Memory % info , PIDs (gives a wholistic view of all the process running)
4. nproc --> prints no of CPU cores used by Linux machine
5. df -h   --> prints free disc space present in the system
6. free    --> prints info regarding free memory and swap memory
7. ps -ef | grep --> Gives details info rgearding all the processes running
8. awk  --> used to get particular output 
9. find
10. if loops and for loops
11. set -x set -e set -o
12. curl
13. wget
14. curl vs wget
15 man --> command to get help on any command
16. symlinks vs hardlinks
17. default permissions of a file when it is created - 666 - rw-rw-rw-
18. head 
19. tail
20. mount (lists all the mounts on the current system)
21. redirection commands(>,<)
22. uname - provides Linux kernel info
23. du --> command to check disk usage directory wise

-------------------------------------------------------------------------------------------------------------------------

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

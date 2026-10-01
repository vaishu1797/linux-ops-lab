

The Linux commands: navigation, files, permissions, processes,disk/memory, logs, system information, and networking.


1. Basic Navigation & User Information

 whoami            = Displays username of currently logged-in user.
 pwd               = Shows current working directory.
 ls                = Lists files and directories in the current directory.
 ls -l filename    = Shows detailed information about a file.(permissions, owner, group, size and modification time)
 ls -ld directory  = Shows detailed information about the directory itself, rather than its contents.


2. System Information

 uname -a            = Displays detailed kernel/system information.
 hostname            = Displays the name of current machine.
 lsb_release -a      = Displays Linux distribution and version information.
 cat /etc/os-release = Displays Linux operating-system release information.
 uptime              = Shows how long system running,logged-in users and load averages.


3. Directories & Files

 mkdir -p ~/linux-ops-lab                         = Creates linux-ops-lab under the home directory.(-p creates missing parent directories)
 cd ~/linux-ops-lab                               = Moves into linux-ops-lab directory.
 mkdir logs configs scripts backup                = Creates four directories at once.
 touch logs/app.log                               = Creates an empty app.log file if it does not already exist.
 touch logs/error.log                             = Creates an empty error.log file.
 touch configs/app.conf                           = Creates an empty configuration file.
 touch scripts/start.sh                           = Creates an empty shell script file.
 find .                                           = Finds files and directories starting from the current directory.
 cp logs/app.log backup/                          = Copies app.log into the backup directory.(the original remains)
 mv backup/app.log backup/application.log         = Renames app.log to application.log in the same directory.
 rm backup/application.log                        = Deletes the specified file.


4. Writing & Reading Logs

 echo "application started" > logs/app.log        = Writes the text into app.log.( > overwrites the file)
 cat logs/app.log                                 = Displays the contents of app.log.
 tail logs/app.log                                = Displays the last 10 lines of the file by default.
 tail -f logs/app.log                             = Continuously follows the file and displays new log entries as they are added.
 echo "application error" >> logs/app.log         = Appends text to the file without overwriting existing content.


5. File Permissions

 chmod 600 logs/app.log                          = Changes permissions so owner has read/write access, while group and others have no access.
                                             600 = rw-------  6 = read (4) + write (2);0 = no permission.

6. Processes

 ps                  = Shows processes of current terminal/session.
 ps aux              = Shows all running processes with user, PID, CPU, memory, status.
 ps aux | head       = Sends the process list through head and displays the first 10 lines by default.
 ps aux | grep bash  = Searches process list for entries containing bash.
 ps aux | grep ssh   = Searches process list for entries containing ssh.
 top                 = Continuously updating, real-time process and CPU/memory monitoring.
 Press q to exit.


7. Disk Space & Memory

 df -h            = Shows filesystem disk usage and available space in human-readable units.
 du -sh ~         = Shows total disk space used by the home directory.
 du -sh /*        = Shows disk usage for each item directly under root directory.
 free -h          = Shows RAM and swap memory usage in human-readable units.


8. Logs & Troubleshooting

 ls /var/log                        = Lists log files and directories under /var/log.
 sudo tail -n 20 /var/log/syslog    = Shows last 20 lines of system log. sudo may be required for access.
 grep -i error /var/log/syslog      = Searches syslog for lines containing error. 


9. Network Troubleshooting

 ping -c 4 google.com           = Tests network reachability using 4 packets and shows response time/packet loss.
 curl -I https://google.com     = Sends HTTP request and displays response headers only.
 curl -IL https://google.com    = Displays headers and follows HTTP redirects. -L follows redirects.
 ss -tuln                       = Shows listening TCP/UDP sockets using ports.
 ss -tulnp                      = Shows listening TCP/UDP sockets plus process using ports.
 sudo ss -tulnp                 = Process  with elevated privileges.
 nslookup google.com            = Queries DNS and shows IP address information of google.com.


10. Quick Troubleshooting Flow


 Who am I / where am I?            = whoami / pwd
 What OS/kernel is this?           = uname -a ,  lsb_release -a  ,  cat /etc/os-release
 Is disk space low?                = df -h ,  du -sh /*
 Is memory high?                   = free -h , top
 Is a process running?             = ps aux | grep
 What ports are listening?         = ss -tulnp
 Can I reach a host?               = ping -c 4
 Is DNS working?                   = nslookup
 Is HTTP/HTTPS responding?         = curl -I https://google.com
 What are the latest system logs?  = sudo tail -n 20 /var/log/syslog
 Find errors in logs               = grep -i "error" /var/log/syslog


Key memory points: 
  
  ps = process snapshot;  top = live process monitoring;   df = filesystem space;  du = directory/file space;  free = RAM/swap; 
  grep = search/filter;  ss = sockets/ports;  nslookup = DNS;  ping = reachability;  curl = HTTP/API response.

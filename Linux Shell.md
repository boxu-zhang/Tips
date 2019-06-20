# Linux Shell Tips
### How to find out cwd(current working directory) a process?
```bash
# correct command
ls -l /proc/$(pid)/cwd 
# wrong command, with a slash '/' in the end of last command
ls -l /proc/$(pid)/cwd/
```
### How to find out which process opens a specific port?
```bash
 netstat -tulpn | grep $(port)
```
### Linux shared library search path
```bash
/etc/ld.so.conf
```
### Vim Jump Forward & Backward
```bash
CTRL + O/I # O for backward and I for forward
```
### Useful shortcuts
```bash
CTRL + U # Clear current command line
CTRL + L # Clear whole screen
```
### Remove all go files's BOM
```bash
find ./ -type f -name "*.go" -exec sed -i -e '1s/^\xEF\xBB\xBF//' {} \;
```
### Remove Carriage Return(^M)
```bash
# (to get ^M type CTRL+V followed by CTRL+M
find ./ -type f -name "*.go" -exec sed -i -e "s/^M//g' {} \;
```
### List umount disk device
```bash
lsblk -io KNAME,TYPE,SIZE,MODEL
```
### Display Process Tre
```bash
ps -aef --forest | more
```
### Count line of file
```bash
wc -l ./file.text
cat ./file.text | grep wc -l
```
### Yum Source for CentOS6/7
```bash
http://www.city-fan.org/ftp/contrib/yum-repo/rhel6/x86_64/
```
### Sed
```bash
# Comment a bash line start with LIBS=
  sed -i '/^LIBS=/s/^/#&/g' Makefile
```
### Set Tab Size
```bash
tabs 4 # set tab size to 4
```
### Show cmdline of process
```bash
xargs -0 < /proc/<pid>/cmdline # native cmdline don't have space
```
### Create netcat interface for any console program
```bash
# On the server:
mkfifo pipe_name
nc -l -p port_number < pipe_name | program_name > pipe_name

# On the client:
nc server_machine_name port_number

# To remove the fifo after program closed, pipe is a file under same folder of the command you run
rm pipe_name
```
### Print total cpu usage of a machine
```bash
grep 'cpu ' /proc/stat | awk '{usage=($2+$4)*100/($2+$4+$5)} END {print usage "%"}'
```
### View markdown in console
```bash
# must install pandoc first
pandoc -t plain README.md | less
```
### Core dump setting
```bash
# Enable core dump in bash
ulimit -c unlimited

# Analyze core dump file
gdb <executable> -c <core-file>

# or
gdb <executable>
(gdb) core <core-file>
```
### Get library information
```bash
# Get dependency
ldd ./<execuable_name>

# Get elf information
readelf -d ./<execu>

# list file used by process
lsof -p <pid>
```

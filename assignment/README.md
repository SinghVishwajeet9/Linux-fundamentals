# Deploying a Cronjob in linux 

### CronJob is meant for performing regular scheduled actions such as backups, updates, and so on. It runs a Job periodically on a given schedule
This is the basic command to deploy a cronjob :
```
crontab -e
```
you can also deploy a cronjob for a particular user by using the following command:
```
sudo crontab -e -u <username>
```
use `sudo` for root access
```
* * * * * command-to-run
| | | | |
| | | | +----- Day of week (0 - 7)
| | | +------- Month (1 - 12)
| | +--------- Day of month (1 - 31)
| +----------- Hour (0 - 23)
+------------- Minute (0 - 59)
```
## Deploy a cronjob to update and upgrade the system everyday
```
sudo crontab -e      

0 0 * * * apt update && sudo apt upgrade -y
```
use `-y` option to auto conifrm updates

## some examples

 Every minute	        --     `* * * * *`	    

Every hour	           --     ` 0 * * * *`	   

Every day at 1 AM	   --        `0 1 * * *	`   

Every reboot --`@reboot` 


# Create a custom Binary
here, i am creating a binary `fib` to show fibonacci series upto `n` terms
```
cat > fib
#!/bin/bash

# Read number of terms
read -p "Enter the number of terms: " n

# Initialize first two terms
a=0
b=1

echo "Fibonacci series up to $n terms:"

for (( i=0; i<n; i++ ))
do
    echo -n "$a "
    fn=$((a + b))
    a=$b
    b=$fn
done

echo
```
make it executable by:
```
chmod +x fib
```

now you can run it by the following command:
``` 
./fib
```
but if you want to run it just by entering `fib` like other commands such as `ls`, you have to copy or move your custom script to path that is stored in environment variables such as `/usr/local/bin`:
run the command: 
```
mv /home/paul/fib /usr/local/bin
```
now you can run only using:
```
fib
Enter number of terms: 7
fibonacci series upto 7 terms:
0112358
```

# Creating a new user and setting its password
To create a new user run the command:
```
sudo useradd [options] <username>
```
to create a new user `Vinix`:
```
sudo useradd -s /bin/bash -d /home/ Vinix
```
To set the password:
```
sudo passwd Vinix 
```
## Enable password authentication for ssh:
go to `root` user and run the command:
```
sudo nano /etc/ssh/sshd_config
```
here, enable password auth in `/etc/ssh/sshd_config` with
```
PasswordAuthentication yes
```
now you have enabled password login for ssh
```
username@your_ip
enter password:
```
Now you can enter your password and connect with server/user/

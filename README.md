# Hack_Away_Walkthrough

# Let's first create a directory on our machine for this challenge
sudo mkdir hack_away
cd hack_away

# Let's start with an nmap scan to find out what ports are running on the machine and output the results in our hack_away directory.
nmap $IP -sC -sV -oN nmap_scan

# Here we see that FTP (21), SSH (22) and HTTP (80) are the only ports open.

# The nmap scan tells us that anonymous login is allowed for the FTP service. Let's start there.
ftp $IP
username = anonymous
password = anonymous

# Logging in to ftp we see a zip file. Let's download it to our machine and play with it.
ls
get hackme.zip
quit

# If we now do an "ls" on our machine we should see the zip file. Let's try and unzip it.
unzip hackme.zip

# The zip file is password protected! We can use a tool called "fcrackzip" to try and crack the password.
sudo apt install fcrackzip -y
fcrackzip -u -D -p /path/to/rockyou.txt hackme.zip

# Fcrackzip was successful in cracking the password. Let's unzip the file using the found password.
fcrackzip hackme.zip
# Enter password

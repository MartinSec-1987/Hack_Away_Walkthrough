# Hack_Away_Walkthrough

# Let's first create a directory on our machine for this challenge
sudo mkdir hack_away
cd hack_away

# Let's start with an nmap scan to find out what ports are running on the machine and output the results in our hack_away directory.
nmap $IP -sC -sV -oN nmap_scan

# Here we see that FTP (21), SSH (22) and HTTP (80) are the only ports open.

# The nmap scan tells us that anonymous login is allowed for the FTP service. Let's start there. Login with both the username and password as "anonymous"
ftp $IP

# Logging in to ftp we see a zip file. Let's download it to our machine and play with it.
ls \n
get hackme.zip \n
quit

# If we now do an "ls" on our machine we should see the zip file. Let's try and unzip it.
unzip hackme.zip

# The zip file is password protected! We can use a tool called "fcrackzip" to try and crack the password.
sudo apt install fcrackzip -y
fcrackzip -u -D -p /path/to/rockyou.txt hackme.zip

# Fcrackzip was successful in cracking the password. Let's unzip the file using the found password.
unzip hackme.zip
enter the password

# Now doing an "ls -l" in our hack_away directory we see the extracted files. We have "steg_clue.txt" and "stego_image.jpg"

# The name of these files hints straight towards some stegonography.

# First let's take a look at "steg_clue.txt"
cat steg_clue.txt

# We have a famous movie quote clue of "Send A Maniac To Catch A ......".

# Google helps us find the missing word at the end of the quote. Must be some sort of password.

# Let's use "steghide" to find out if there is anything hidden in this stego_image.jpg we extracted.
sudo apt install steghide -y
steghide extract -sf stego_image.jpg
enter the movie quote word we found as the password.

# Now doing an "ls -l" in our hack_away directory we see steghide has extracted a file from the image called creds.txt. Let's take a look.
cat creds.txt

# 


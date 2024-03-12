fisier README

	Firstly, I installed the Docker Desktop app and the I uploaded an Ubuntu Image using the command : 
docker pull ubuntu:latest.

	Then, I wanted to start the container using the : 
daria@laptop-daria MINGW64 ~/Desktop
$ winpty docker run -it --name my_linux_container ubuntu,
  
	I had an error that I resolved by firstly removing my_linux_container daria@laptop-daria MINGW64 ~/Desktop
$ docker rm my_linux_container

	and then creating it again.
daria@laptop-daria MINGW64 ~/Desktop
$ docker rm my_linux_container

	Once this was done, I was inside my container, ready to create the user John, using the command : 
root@58ab944edaba:/# adduser john

	I copied the create_large_file.sh script to the container using the cp command and in order to do this I had to get out of the container:
daria@laptop-daria MINGW64 ~/Desktop
$ docker cp C:/Users/daria/Desktop/interviu/create_large_file.sh 

	Now the script is in container, I switched to john again and I executed the script using:
john@58ab944edaba:~$ ./create_large_file.sh

	After that, I encountered a typo in the script ( mv lage_file /home/john
) and I renamed the file from lage_file to large_file.
john@58ab944edaba:~$ sed -i 's/mv lage_file/mv large_file/' create_large_file.sh

	Finally, I ran the script again.


The commands for the following tasks are:

1. Print the home directory
root@58ab944edaba:/# echo $HOME

2. List all usernames from the passwd file
root@58ab944edaba:/# cut -d: -f1 /etc/passwd

3. Count the number of users
root@58ab944edaba:/#$ cut -d: -f1 /etc/passwd | wc -l

4. Find the home directory of a specific user (prompt to enter the username value)
root@58ab944edaba:/# read -p "username" username
username john
root@58ab944edaba:/# grep "^$username:" /etc/passwd | cut -d: -f6
/home/john

5. List users with specific UID range (e.g. 1000-1010)
root@58ab944edaba:/# awk -F: '$3 >= 1000 && $3 <= 1010' /etc/passwd

6. Find users with standard shells like /bin/bash or /bin/sh
root@58ab944edaba:/# grep -E '/bin/(bash|sh)$' /etc/passwd

7. Replace the “/” character with “\” character in the entire /etc/passwd file and redirect the content to a new file
root@58ab944edaba:/# sed 's/\//\\/g' /etc/passwd > modified_passwd_file

8. Print the private IP
root@58ab944edaba:/# hostname -I | cut -d' ' -f1

9. Print the public IP
root@58ab944edaba:/# curl -s ifconfig.me

10. Switch to john user
root@58ab944edaba:/# su john

11. Print the home directory
john@58ab944edaba:~$ echo $HOME
/home/john
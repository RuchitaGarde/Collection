### This file contains some common problems with respect to installation & others I faced while working on development projects. I am noting them down here with solutions that worked for me.
Please note that I use a windows machine, & it is not easy to find solutions for windows, & my solutions will only be for windows users.

#### 1. When trying to install node/npm packages, a common error one might get is something like this:
"Python executable "python" is v3.4.3, which is not supported by gyp"
This problem was fixed in latter versions of gyp. So, if you are using gyp version below 3.0, then you might face this problem.
Solution: Update your gyp. It is not possible to find out the version of gyp your node has since 'npm' bundles its own internal copy of node-gyp. This will not appear in your node_modules either.
To update to latest gyp, follow the step (for windows machine):
- Open cmd with administrator provileges, since your installations will mostly be in program files.
- `where node`
(Used to find where your node is located)
- `cd` into the directory that node.exe is contained in.
- `npm install -g node-gyp@latest`

#### 2. When trying to see which ports are listening on your computer:
- Run cmd as administrator
- `netstat -ano |findstr : yourportnumber` OR just `netstat -ano` will give you a list of all of them. THe last column of the row of your port will have the pid value. Note it.
- `taskkill /PID yourpidhere /F`

#### 3. When trying to SSH into a remote server which is protected by a private key, and you are using Putty:
- If not already done, first convert the filetype of your key into .ppk (the filetype accepted by putty). For eg, you can convert a .pem or a .txt file into .pppk.
To do that, download puttygen from https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html. Open puttygen, *load* an existing key, and then 'save' the key. This will automatically save the key in putty's ppk format.
- Now, open putty, enter the *ip address*, expand *SSH* under *Connection* on the left hand side Categories menu, select *Auth*, and now browse for the new .ppk file you just created. 

#### 4. When trying to SSH into a remote server which is protected by a private key, using command line:
- Type `ssh` into your command-line. If command is not recognized, your cmd should be 'Run as Administrator'.
- If `ssh` command still not recognized, download [OpenSSH for Windows](https://sourceforge.net/projects/sshwindows/?source=typ_redirect).
- Rerun command prompt as administrator, a common ssh command looks like this:
`ssh -i C:\privatekeylocation.ppk -L port:host:hostport username@hostname`
  - Eg: `ssh -i C:\users\user\key.ppk -L 5432:localhost:5432 user@12.234.678.900`
  *For postgres databases, the portname is usually 5432 by default.*
  This is called SSH tunneling.
- If your private key is not protected by a passphrase, you may get an error: 



#### 5. When trying to copy files from a remote server onto your machine or vice versa:
- On windows machines, do not use `scp`, instead, use `pscp` command. To do that, first download *pscp.exe* from https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html. 
- Run the executable. Also, add the location to which this file is stored in the *PATH* in your environment variables.
- Now, whether you want to copy from remote to local or local to remote, ALWAYS use this command on the command prompt of your local machine:
`pscp source destination`
  - EG: From remote to local: 
  `pscp Username@ipaddress:/home/example_file.py C:\Users\localuser\Documents\whatever_I_want_to_name_my_file.py`

- In cases when the remote machine required a cryptographic key to login, that key needs to be sent along with the pscp command in this way using the *-i* flag for the key_file and *-l* for the username:
Eg: From local to remote:
`pscp -i C:\Users\localuser\key_file.ppk -l ec2-user C:\Users\localuser\dump.sql ec2-user@ipaddress:/home/ec2-user/whatever_I_want_to_name_my_file.sql`
Please note that thekey has to be in .ppk format, & if it is not, it can be converted using the steps provided in point #3.

#### 5. Some PostGres things.
- If you had setup your PostGre Server with a password (Note that using a password is not mandatory), then while trying to setup a local copy of a node.js project on your computer might you an error which looks something like: 
*error: password authentication failed for user "username"*, where *username* is the name you used while setting up your server. To solve  this, include this line in your .env file:
`DB_URI=postgresql://username:password@localhost/dbname` instead of 
`DB_URI=postgresql://username@localhost/tmastradetest` if you did not have a password.

- The `\d` command, when used in psql prompt lists all the tables present in your database.

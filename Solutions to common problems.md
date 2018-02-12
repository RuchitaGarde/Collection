This is work in progress

This file contains some common problems with respect to installattion & others I faced while working on development projects. I am noting them down here with solutions that worked for me.
Please note that I use a windows machine, & it is not easy to find solutions for windows, & my solutions will only be for windows users.

1. When trying to install node/npm packages, a common error one might get is something like this:
"Python executable "python" is v3.4.3, which is not supported by gyp"
This problem was fixed in latter versions of gyp. So, if you are using gyp version below 3.0, then you might face this problem.
Solution: Update your gyp. It is not possible to find out the version of gyp your node has since 'npm' bundles its own internal copy of node-gyp. This will not appear in your node_modules either.
To update to latest gyp, follow the step (for windows machine):
- Open cmd with administrator provileges, since your installations will mostly be in program files.
- where node
(Used to find where your node is located)
- cd into the directory that node.exe is contained in.
- npm install -g node-gyp@latest

2. When trying to see which ports are listening on your computer:
- Run cmd as administrator
- 'netstat -ano |findstr : yourportnumber' OR just 'netstat -ano' will give you a list of all of them. THe last column of the row of your port will have the pid value. Note it.
- taskkill /PID yourpidhere /F

3. When trying to SSH into a SSH which is protected by a private key, and you are using Putty:
- If not already done, first convert the filetype of your private into .ppk (the filetype accepted by putty). For eg, you can convert a .pem or a .txt file into .pppk.
To do that, download puttygen from https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html. Open puttygen, 'load' an existing key, and then 'save' the key. This will automatically save the key in putty's ppk format.

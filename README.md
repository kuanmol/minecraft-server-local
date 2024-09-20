This vagrantfile to run minecraft server in your local host first.

Where you saved that vagrantfiel you have to run: 
Vagrant init
Vagrant up
Vagrant ssh

There might chance that java may not install so copy this command to install inside the terminal after running vagrant:
java -version if this not working then follow down steps:

wget https://download.oracle.com/java/23/latest/jdk-23_linux-x64_bin.tar.gz 
tar -xvf jdk-23_linux-x64_bin.tar.gz                                        

After the installtion now you have to make it default for your terminal

sudo mkdir -p /opt/jdk      
sudo mv jdk-23 /opt/jdk/                                                                                                                                                            

set up the enviroment variables
nano ~/.bashrc

after running nano commant a script file will open write this line at the end of file:

export JAVA_HOME=/opt/jdk/jdk-23
export PATH=$JAVA_HOME/bin:$PATH

Save and exit (Ctrl + X, then Y, and press Enter).

source ~/.bashrc

now java is setup for verification

java -version

there might error come that most probably for permission error

sudo chmod -R 755 /home/vagrant/minecraft-server

sudo chown -R vagrant:vagrant /home/vagrant/minecraft-server

After giving the permission to the sever files, use this command to run it:

java -Xmx4096M -Xms4096M -jar minecraft_server.1.21.1.jar nogui

if you have bought mohjang minecraft then u can direct use /op [playr id] if you using tlauncher then:

nano server.properties                                                                                                                                                              
online-mode=false

and for adding new player 
whitelist=true

for admin 
op playername

normal player
whitelist add playername





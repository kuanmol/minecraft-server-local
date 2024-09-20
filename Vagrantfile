Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/jammy64"  # Updated to Ubuntu 22.04 (Jammy Jellyfish)

  config.vm.provider "virtualbox" do |vb|
    vb.name = "minecraft-server"     # Name of the Virtual Machine
    vb.memory = "8192"               # Allocate 8GB of RAM for the VM
    vb.cpus = 2                      # Use 2 CPU cores
  end

  config.vm.network "private_network", ip: "192.168.56.10"
  config.vm.network "forwarded_port", guest: 25565, host: 25565

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get install -y openjdk-23-jre-headless wget screen  # Updated to OpenJDK 23

    # Create Minecraft server directory
    mkdir -p /home/vagrant/minecraft-server
    cd /home/vagrant/minecraft-server
    
    # Download the Minecraft server jar
    wget https://piston-data.mojang.com/v1/objects/59353fb40c36d304f2035d51e7d6e6baa98dc05c/server.jar -O minecraft_server.1.21.1.jar
    
    # Accept the Minecraft EULA
    echo "eula=true" > eula.txt

    # Create the server.properties file
    cat <<EOT > server.properties
# Minecraft server properties
allow-nether=true
level-name=my_custom_world
server-port=25565
max-players=5
view-distance=10
allow-cheats=true
motd=My Vagrant Minecraft Server 1.21.1
difficulty=normal
gamemode=survival
EOT

    # Create a script to start the Minecraft server
    echo '#!/bin/bash' > start_minecraft.sh
    echo 'cd /home/vagrant/minecraft-server' >> start_minecraft.sh
    echo 'screen -dmS minecraft java -Xmx4096M -Xms4096M -jar minecraft_server.1.21.1.jar nogui' >> start_minecraft.sh
    chmod +x start_minecraft.sh

    # Start the Minecraft server if it's not already running
    if ! screen -list | grep -q "minecraft"; then
      ./start_minecraft.sh
    fi
  SHELL
end

A simple Ansible playbook to deploy a Minecraft Modpack onto a Linux (tested with Oracle Linux 9) machine.


Inventory should include authentication, modpack, and optionally port for each host. New hosts will need to be added to the minecraft group in the inventory/hosts.yaml file.

Minecraft role includes the shared config used across modpacks and a set of default_minecraft_settings that takes a lower precedence than modpack or host specific settings.
Additional roles exist for Modpacks in the form of directories with mods, configs, a populated variables.txt, and any other needed files.

The only variables that should need to be changed in the variables.txt is the modloader, modloader_version, minecraft_version, recommended_java_version and java_args. Changing any others may result in the server not installing correctly or not behaving correctly as a daemon.

The server.properties uses a common template from the minecraft role, if any fields are desired to be changed on a per pack or per pack basis, they will need to be added to the minecraft_settings vars for that pack and updated in the server.properties.j2 template to read them.

The Minecraft server is ran in a tmux session named the same as the modpack name.

The Minecraft server uses Jabba to source its Java rather than relying on a system Java.

The Minecraft server will be installed as a systemd daemon and will auto restart in the event of a crash.


When executing the playbook, ensure the whole repository is not world writable else the ansible.cfg file will not be read. (i.e. chmod 770 on the directory)


References:

https://docs.ansible.com/projects/ansible/latest/getting_started/index.html 

https://blog.kywa.io/tag/mineops/ 

https://serverpackcreator.de/#/ 


= Shinken POC=

== prereq ==
    $ vagrant plugin list
    ansible (0.2.2)
    vagrant-share (1.1.5, system)
    $ vagrant ssh-config central
    Host central
      HostName 127.0.0.1
      User vagrant
      Port 2200
      UserKnownHostsFile /dev/null
      StrictHostKeyChecking no
      PasswordAuthentication no
      IdentityFile /home/jack/git/shinken2/.vagrant/machines/central/virtualbox/private_key
      IdentitiesOnly yes
      LogLevel FATAL
      ForwardAgent yes

== Creation du noeud central ==
    # vagrant up central --provision
    # ansible all -i central, -m setup
    central | SUCCESS => {
        "ansible_facts": {
            "ansible_all_ipv4_addresses": [
                "10.0.15.11", 
                "10.0.2.15"
            ], 
            "ansible_all_ipv6_addresses": [
                "fe80::a00:27ff:fec5:9894", 
                "fe80::5054:ff:fe96:1d95"
            ], 
            "ansible_architecture": "x86_64", 
            "ansible_bios_date": "12/01/2006", 
            "ansible_bios_version": "VirtualBox", 
            "ansible_cmdline": {
                "BOOT_IMAGE": "/vmlinuz-3.10.0-327.18.2.el7.x86_64", 
                "LANG": "en_US.UTF-8", 
                "biosdevname": "0", 
                "console": "ttyS0,115200", 
                "crashkernel": "auto", 
                "net.ifnames": "0", 
                "no_timer_check": true, 
                "quiet": true, 
                "rd.lvm.lv": "VolGroup00/LogVol01", 
                "rhgb": true, 
                "ro": true, 
                "root": "/dev/mapper/VolGroup00-LogVol00"
            }, 
            ...
            "ansible_uptime_seconds": 3886, 
            "ansible_user_dir": "/home/vagrant", 
            "ansible_user_gecos": "vagrant", 
            "ansible_user_gid": 1000, 
            "ansible_user_id": "vagrant", 
            "ansible_user_shell": "/bin/bash", 
            "ansible_user_uid": 1000, 
            "ansible_userspace_architecture": "x86_64", 
            "ansible_userspace_bits": "64", 
            "ansible_virtualization_role": "guest", 
            "ansible_virtualization_type": "virtualbox", 
            "module_setup": true
        }, 
        "changed": false
    }

== Connexion ==
    $ vagrant ssh central
    [vagrant@central ~]$ sudo -i

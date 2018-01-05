# Vagrant-Box16

# this project for ubuntu 16.04 vagrant box

# Pre-install setup

1. [virtualbox](https://www.virtualbox.org/wiki/Downloads)

2. [vagrant](https://www.vagrantup.com/downloads.html)

3. [git](https://git-scm.com/downloads) for minGW64(like bash terminal) Or [Mobaxterm](https://mobaxterm.mobatek.net/download.html)

# make working space

```bash
# make default workspace
$ mkdir vagrant-box16
$ cd vagrant-box16

# make basebox
$ vagrant init

# make SSH key
$ ssh-keygen
(public and private key PATH is depending on terminal default PATH)

# launch vagrant via Vagrantfile 
$ vagrant up
```

```
# if you catch below error,
$ vagrant ssh
==> default: The machine you're attempting to SSH into is configured to use
==> default: password-based authentication. Vagrant can't script entering the
==> default: password for you. If you're prompted for a password, please enter
==> default: the same password you have configured in the Vagrantfile.
or
server refuse
or
Permission denied (publickey,password)

# should check 'config.ssh.private_key_path', check source at Vagrantfile 

  config.vm.provision "file",
    source: "~/.ssh/id_rsa", destination: "/home/ubuntu/.ssh/id_rsa"

  config.vm.provision "file",
    source: "~/.ssh/id_rsa.pub", destination: "/home/ubuntu/.ssh/id_rsa.pub"

  config.vm.provision "file",
    source: "~/.ssh/id_rsa.pub", destination: "/home/ubuntu/.ssh/authorized_keys"

  config.vm.provision "shell", privileged: false, inline: <<-SHELL
    chmod 400 ~/.ssh/id_rsa ~/.ssh/id_rsa.pub ~/.ssh/authorized_keys
  SHELL

# then, Do
$ vagrant provision
$ vagrant ssh-config
```

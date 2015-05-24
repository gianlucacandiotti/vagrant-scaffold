# Vagrant Scaffold

This repository contains the main structure to run a vagrant environment provisioned with puppet. It's recommended to use it as a git subtree inside your repository for better management since you'll need to modify some file later on. Also the puppet modules should be added later as submodules inside *vagrant-env/puppet/modules* folder since we aren't touching them most likely.

It's already set up to use ubuntu 14.10 distribution on virtual box although this can be easily changed on the **Vagrantfile**. The sync folder currently points to an */app* folder outside the vagrant environment folder. Your project structure should look like this:

- vagrant-env ( or whatever you want to name this repository inside your project )
	- .vagrant
	- puppet
	- Vagrantfile
- app
	- **Your project files go here**

## Adding this repository as a subtree

1. `git remote add -f vagrant-env git@github.com:GianlucaCandiotti/vagrant-scaffold.git`

2. `git subtree add --prefix vagrant-env vagrant-env master --squash`

3. Don't forget that the Vagrantfile will look for the *./app* folder as the sync folder. If you already have some files, put them in an *./app* folder so that your structure looks like the one described above. If you are starting from scratch or cloning a repository just create the *./app* folder and put your files in there.

4. Currently the Vagrantfile configures the guest machine with a private network **192.168.33.10** that allows host only access. Also the Vagrantfile will forward port **8080** on the guest machine to port **8080** on the host machine.

## Updating the subtree from your repository

1. `git fetch vagrant-env master`

2. `git subtree pull --prefix vagrant-env vagrant-env master --squash`

## Adding puppet modules as submodules

1. From the command line navigate to the vagrant-env folder.

2. To add a puppet submodule type:

		git submodule add [repository-url] puppet/modules/name_of_the_module

For example to add the apt module you would type:

	git submodule add git@github.com:puppetlabs/puppetlabs-apt.git puppet/modules/apt

## Running on Windows

If you are working on a Windows environment, run this command in a command prompt as administrator in order to allow all kinds of symbolic links to be created on the computer:

	fsutil behavior set SymlinkEvaluation L2L:1 R2R:1 L2R:1 R2L:1

After that reboot your computer to apply changes.

### Some already configured environments using this repository

[Node ready environment](https://github.com/GianlucaCandiotti/node-env)

[Node/Mongo ready environment](https://github.com/GianlucaCandiotti/mongo-node-env)
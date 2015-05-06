# Vagrant Scaffold

This repository contains the main structure to run a vagrant environment provisioned with puppet. It's recommended to use it as a git subtree inside your repository for better management since the puppet modules should be added later as submodules inside *vagrant-env/puppet/modules* folder.

It's already set up to use ubuntu 14.10 distribution on virtual box although this can be easily changed on the **Vagrantfile**. The sync folder currently points to an */app* folder outside the vagrant environment folder. So your project structure should look like this:

- vagrant-env ( or what ever you want to name this repository inside your project )
	- .vagrant
	- puppet
	- Vagrantfile
- app
	- **Your project files go here**

## Adding this repository as a subtree

1. `git remote add -f vagrant-env git@github.com:GianlucaCandiotti/vagrant-scaffold.git`
2. `git merge -s ours --no-commit vagrant-env/master`
3. `git read-tree --prefix=vagrant-env/ -u vagrant-env/master`
4. `git commit -m "Added Vagrant environment as a subtree merged in vagrant-env"`

## Adding puppet modules as submodules

1. From the command line navigate to the vagrant-env folder.
2. To add a puppet submodule type: `git submodule add [repository-url] puppet/modules/name_of_the_module`

For example to add the apt module you would type:

	git submodule add git@github.com:puppetlabs/puppetlabs-apt.git puppet/modules/apt
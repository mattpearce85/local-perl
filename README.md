# Get started with local development

### Preliminary setup

- Install VirtualBox: https://www.virtualbox.org/wiki/Downloads
  - **If you're on Windows START VirtualBox AS ADMINISTRATOR**
- Install Vagrant: https://www.vagrantup.com/downloads.html
  - **If you're on Windows START Vagrant AS ADMINISTRATOR** i.e. run `vagrant up` in a shell that was started as administrator
- Create a new directory where you want to handle local development (I'll use the tilde ("~") symbol to represent this directory going forward)
- Open a command line at that new directory (the one we're calling "~").
- Clone the repo using the following command:

```git clone https://github.com/mattpearce85/local-perl.git .``` _you can download Git here if you don't already have it: https://git-scm.com/downloads_

- Now that we have the local environment repository on our machine we can execute the following commands:

```vagrant up``` _this will take a few minutes the first time..._

```vagrant ssh``` _this opens an ssh command line within the virtual machine_

- Once ssh'd into the virtual machine, execute the following commands to install Docker:

```sudo apt update```

```sudo apt install apt-transport-https ca-certificates curl software-properties-common```

```curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -```

```sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"```

```sudo apt update```

```sudo apt install docker-ce```

```docker -v``` _this verifies that Docker is installed properly_

- Now install Docker Compose:

```sudo curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose```

```sudo chmod +x /usr/local/bin/docker-compose```

```docker-compose --version``` _this verifies that Docker Compose is installed properly_

### Starting and stopping the local server resources

- Execute the following commands to start up the local server resources

```cd /vagrant``` _/vagrant is mapped to the directory you ran "vagrant up" in (aka "~"), it also houses your web root and everything else_

```sudo docker-compose up -d``` _this will take a few minutes the first time..._

- If you want to shut down the local server resources, execute the following command

```sudo docker-compose down```

# Working with Perl

### Running Perl in the command line

- Make sure your local server resources are running using the `docker-compose` command above
- If you're not ssh'd into vagrant, open a command line where you cloned the repo and run the following command:

```vagrant ssh```

- Now you're logged into the vagrant virtual machine, but Perl is running within Docker container on our virtual machine, so we need to run another command to get to the command line _inside_ the Perl Docker container. It's like command line Inception!

```sudo docker exec -it perl bash```

- Now we've jumped into the virtual machine, and jumped deeper still into the Perl Docker container. We should be ready to run Perl scripts from the command-line. For example, execute the following command to run our plain Perl file:

```perl perl/index.pl```

- This command runs the Perl compiler on the specified file. In this case, the file just outputs some HTML code. The command line doesn't interpret HTML, so it's just plain text. How about running it in a web browser?

### Running Perl in the web browser

- Make sure your local server resources are running using the docker-compose command above
- Open your web browser to `http://perl.localhost/index.pl`
- Let's edit that Perl code... Open the following file from the cloned repo in your IDE or a text editor. It will be somewhere like: `~/webroot/perl/plain-perl/index.pl` 
- Make some changes, save the file, and then refresh your web browser. Do you see your changes? Good!

### Creating a MySQL database for your Laravel application

- Make sure your servers are running and then open your browser to ```http://pma.localhost```
- Login using the username `root` and the password `mysqltemp`
- If you're not already at the phpMyAdmin dashboard, click the logo
- Click the `User Accounts` tab at the top
- Click the `Add user account` tab midway down the page
- Set `User name` equal to your project name and click the `Generate` button to get a password.
- Copy the password to notepad or something, we'll need it next
- Check the box for `Create database with same name and grant all privileges.`
- Scroll down and click the `Go` button in the bottom-right corner
- The database is now ready

# Other stuff

### Server-related commands you might need

- Reloading nginx (such as after updating a configuration file):

```sudo docker exec -it nginx sh``` _Start a shell prompt in the nginx service (must be ssh'd into vagrant)_

```nginx -s reload``` _reloads nginx_

- Restarting the local server resources (such as after doing a `git pull` on this repo):

```sudo docker-compose down```

```sudo docker-compose up -d```

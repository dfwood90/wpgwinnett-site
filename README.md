# WP Gwinnett - Documentation

## WordPress Login Credentials
- Username:
- Password:

## Using Vagrant

### Prerequisites
- Install [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
- Install [Vagrant](http://www.vagrantup.com/downloads.html)
- Install the [Vagrant Hosts Updater](https://github.com/cogitatio/vagrant-hostsupdater) plugin
- Clone the [repository](https://github.com/wpgwinnett/wpgwinnett-site) project onto your machine

### Getting Started
- In the terminal, run `vagrant up` from the project root
- Visit [http://wpgwinnett.dev/](http://wpgwinnett.dev/) in your browser

## Everyday Usage
- Running a virtual machine does utilize resources on the host machine, which means you will want to 'turn off' the virtual machine when not in use.  You can use the `vagrant suspend` or `vagrant halt` commands for this purpose.
- Turning the virtual machine back on can be done using the same `vagrant up` command you used to create the virtual machine initially. Since the machine already exists in this case, the provisioning step will be skipped.
- Should you ever need to reprovision the virtual machine, you can just run `vagrant provision`.  An example of when you may want to do this: The import.sql file was updated by another dev and you need to pull down the database changes.
- Very rarely you may find you need to trash a virtual machine and start fresh.  Just run `vagrant destroy` to trash the virtual machine and then follow the steps in the 'Getting Started' section to create a new instance.

### Accessing the Virtual Machine via Command Line
- Open your terminal and type `vagrant ssh`

### Accessing MySQL Command Line
- After you ssh into the virtual machine, run `mysql -u root -p`
- Type the password `vagrant` when prompted.

### Exporting the MySQL Database
- After you ssh into the virtual machine run `mysqldump -u root -p db_name > /vagrant/sql/backup.sql`
- Type the password `vagrant` when prompted.
- Your `backup.sql` file will now be inside the project `/sql/` directory on your local machine.
- As a best practice, please use this naming convention for backups: backup-[year][month][day].sql (i.e. backup-20140501.sql).
- The file named import.sql will be imported automatically during provisioning. Updating this file and pushing the changes to the repo will allow other devs to pull down your changes by running `vagrant provision`.

### Importing a MySQL Database
- After you ssh into the virtual machine, run `mysql -u root -p -h localhost db_name < /vagrant/sql/import.sql`
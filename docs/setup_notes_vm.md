# VM Set Up Notes
- After signing into your GCP account, navigate to Compute Engine, select VM Instances and create instance
- Create a name for your instance
- Configure your VM using the following settings:
    - Region: us-central1 (Iowa)
    - Zone (Any)
    - Series: E2
    - Machine Type: e2-small
    - OS and storage: change operating system to Ubuntu
- Keep all other settings the same and hit "Create"
- Once your instance is done loading, copy the external IP address and enter it into your .env code
- Next, navigate to Firewall and select: create firewall rule
- Create a name and description
- Configure your firewall using the following settings:
    - Targets: All instances in the network
    - Source IPv4 ranges: 0.0.0.0/0
    - Check TCP box, enter 3306 in the ports section
    - Keep all other settings as the default and hit "Create"
- Return to your VM and open SSH
- Enter the following SSH commands in order:

```bash
    sudo apt-get update
    ```
```bash
    sudo apt install nano mysql-server mysql-client -y 
    ```
```bash
    sudo mysql 
    ```
```bash
    show databases; # to see current list of databases
    ```
```bash
    create database db; # create example database
    ```
```bash
    show databases; # should show newly created db database
    ```
```bash
    create user 'dba'@'%' identified by 'dba2025'; # create user and password
    ```
```bash
    select user from mysql.user; # to verify user creation 
    ```
```bash
    select * from mysql.user where user like ‘dba’ \G; #
    ```
```bash
    grant all privileges on *.* to 'dba'@'%' with grant option; # command to grant privileges
    ```
```bash
    exit; # close SSH, relaunch SSH and enter: 
    ```
```bash
    sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf # this will show bind address and mysql bind address, change both to 0.0.0.0, hit control O, enter, control X 
    ```
```bash
    sudo systemctl restart mysql # if this does not work, relaunch SSH and reenter command
    ```

# Clound shell environment commands, open cloud shell and enter:

```bash
    sudo apt install mysql-client
    ```
```bash
    mysql -u dba -h *IP address* -p # connects to VM, enter password when prompted to
    ```
```bash
    show databases; # see current list of databases, go to VS code and run vm_demo script
    ```
```bash
    show databases; # VM_DB_NAME=test_db should appear in the list of databases
    ```
```bash
    select * from test_db. visits; # this will show you the first 5 rows of our table
    ```
# Issues: sometimes I'd enter commands and they would not run in SSH, to solve this, I would relaunch SSH, re-enter the command and that seemed to work
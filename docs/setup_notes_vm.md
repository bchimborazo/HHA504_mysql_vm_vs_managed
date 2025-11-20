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
- Once your instance is done loading, copy the external IP address and enter it into your .env code, in the "VM_DB_HOST" section
- Next, navigate to Firewall and select: create firewall rule
- Create a name and description
- Configure your firewall using the following settings:
    - Targets: All instances in the network
    - Source IPv4 ranges: 0.0.0.0/0
    - Check TCP box, enter 3306 in the ports section
    - Keep all other settings as the default and hit "Create"
- Return to your VM and open SSH
- Enter the following SSH commands in order:

### 1. Install MySQL Server
```bash
sudo apt-get update
sudo apt install nano mysql-server mysql-client -y 
```

### 2. Configure MySQL
```bash
sudo mysql
```

Inside MySQL:
```sql
SHOW DATABASES;  # to see current list of databases
CREATE DATABASE db;  # create example database
SHOW DATABASES;  # should show newly created db database
CREATE USER 'dba'@'%' IDENTIFIED BY 'dba2025';  # create user and password
SELECT user FROM mysql.user;  # to verify user creation 
SELECT * FROM mysql.user WHERE user LIKE 'dba' \G;  # check user details
GRANT ALL PRIVILEGES ON *.* TO 'dba'@'%' WITH GRANT OPTION;  # grant privileges
EXIT;
```

### 3. Configure MySQL to Accept External Connections
```bash
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
```

Change both `bind-address` and `mysqlx-bind-address` to:
```
bind-address = 0.0.0.0
mysqlx-bind-address = 0.0.0.0
```

Save with `Ctrl+O`, `Enter`, then exit with `Ctrl+X`

Restart MySQL:
```bash
sudo systemctl restart mysql
```

## Testing from Cloud Shell

Install MySQL client:
```bash
sudo apt install mysql-client
```

Connect to VM:
```bash
mysql -u dba -h YOUR_VM_IP -p
```
Enter password: `xxxx`

Verify setup:
```sql
SHOW DATABASES;
```

Run `vm_demo.py` script in VS Code, then verify:
```sql
SHOW DATABASES;  # test_db should appear
USE test_db;
SELECT * FROM visits;  # shows the 5 rows inserted by script
```

## Issues Encountered
- **Issue:** Commands would not always run in SSH
- **Solution:** Relaunched SSH and re-entered the command, which resolved the issue

## Time Tracking
- Total setup time (including all steps): ~ approximately 20 minutes

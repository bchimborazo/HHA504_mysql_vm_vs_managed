# Managed VM Set up Notes
- After signing into your GCP account, navigate to the menu bar, select "All Products" --> Coud Sql --> create instance 
- Configure your instance with the following settings:
    - Select Enterprise tier
    - Edition: Sandbox
    - Version: MySql 8.4
    - Instance ID: create a name
    - No password (for root)
    - Security: Allow unencrypted network traffic
    - Connections: Public IP
    - New Network: allow-all-traffic
    - IP range: 0.0.0.0/0
    - Acknowledge Risk
    - Create
- Instance will take 5-6 minutes to load/create
- Navigate to Users, select Add User
    - User: create
    - Password: create
    - Host: allow any host
    - Hit "Add"
- Open/Connect to Cloud Shell
- Test connection to CloudSql by entering 
```bash
mysql -h YOUR_CLOUD_SQL_PUBLIC_IP -u dba -p
```
Enter password: `dba2025`

Verify connection:
```sql
SHOW DATABASES; 
```
- In VS code, run the managed_demo script, verify databse and table creation:
```sql
SHOW DATABASES;  -- test_db should appear
USE test_db;
SELECT * FROM visits;  -- shows the 5 rows inserted by script
```
## Issues Encountered
- None - setup was straightforward using GCP Console interface

## Time Tracking
- Instance configuration and creation: ~7 minutes
- Running script and entering cloud shell commands: ~3 minute
- Total setup time: ~ approximately 10 minutes total


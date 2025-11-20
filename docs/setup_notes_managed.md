# Managed VM Set up Notes
- After signing into your GCP account, navigate to the menu bar, select "All Products" --> Coud Sql --> create instance 
- Configure your instance with the following settings:
    - Select Enterprise
    - Edition: Sandbox
    - Version: MySql 8.4
    - Instance ID: create a name
    - No password
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
    - Hit "Add"
- Open/Connect to Cloud Shell
- Test connection to CloudSql by entering this command: 

```bash
    mysql -h *ENTER PUBLIC_IP* -u dba -p
    ```

- Enter user password and run managed_demo script in VS code

```bash
    show databases # should show test_db database
    ```
```bash
    select * from test_db.visits; # this will show you the first 5 rows of our table
    ```



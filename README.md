# HHA504_mysql_vm_vs_managed
- Name: Blanca Chimborazo-Reyes
- Cloud Chosen: GCP
- Region: us-central1 (Iowa)
- Video link (VM and managed in one video): https://drive.google.com/file/d/1II9pLbUSr3uruMDNhqyFfchWhqNIETiu/view?usp=sharing
- VM portion: 0:00:00 - 0:08:01
- Managed Service portion: Begins at 0:08:02 - until end of video

## Documentation 
- [VM Setup Notes](docs/setup_notes_vm.md) - Detailed step-by-step VM configuration
- [Cloud SQL Setup Notes](docs/setup_notes_managed.md) - Detailed Cloud SQL configuration
- [Comparison Analysis](docs/comparison.md) - Use case recommendations and analysis

## Overview
This project compares two approaches to running MySQL databases on GCP:
1. **Self-Managed MySQL** on a Compute Engine VM
2. **Managed MySQL** using Cloud SQL

## Project Structure
```
HHA504_mysql_vm_vs_managed/
├── .env                          # Local secrets (NOT committed)
├── .env.example                  # Template with placeholders
├── .gitignore                    # Excludes .env
├── README.md                     # This file
├── requirements.txt              # Python dependencies
├── scripts/
│   ├── vm_demo.py               # Self-managed VM demo
│   └── managed_demo.py          # Cloud SQL demo
├── docs/
│   ├── setup_notes_vm.md        # Detailed VM setup steps
│   ├── setup_notes_managed.md   # Detailed Cloud SQL setup steps
│   └── comparison.md            # Analysis and recommendations
└── screenshots/
    ├── vm/                       # VM-related screenshots
    ├── managed/                  # Cloud SQL screenshots

```


### Self-Managed VM Setup (for more detailed instructions, view docs/setup_notes_vm.md)
1. Create a Compute Engine VM instance (select E2 series, e2-small, change OS to Ubuntu)
2. Configure GCP firewall rules to allow TCP port 3306
3. SSH into the VM and install MySQL server
4. Configure MySQL user (`dba`) with appropriate privileges
5. Edit `/etc/mysql/mysql.conf.d/mysqld.cnf` to allow external connections (bind-address = 0.0.0.0)
6. Restart MySQL service
7. Update `.env` file with VM's External IP
8. Run `python scripts/vm_demo.py` on VS code
9. Verify database and table creation using Cloud Shell: connect with `mysql -h *IP* -u dba -p` 
10. Enter "show databases;", should show test_db
11. Run `SELECT * FROM test_db.visits;`, to view the first 5 rows of the visits table

### Managed Cloud SQL Setup (for more detailed instructions, view docs/comparison.md)
1. Create a Cloud SQL MySQL instance via GCP Console
2. Configure instance settings (Sandbox tier, MySQL 8.4, allow unencrypted network traffic, etc.)
3. Configure authorized networks (add 0.0.0.0/0 for testing)
4. Add database user (`dba`) through Cloud SQL Users tab
5. Note the Public IP address
6. Update `.env` file with Cloud SQL's Public IP
7. Run `python scripts/managed_demo.py` on VS code
8. Verify database and table creation using Cloud Shell: connect with `mysql -h *IP* -u dba -p`
9. Enter "show databases;", should show test_db
10. Run `SELECT * FROM test_db.visits;`, to view the first 5 rows of the visits table

---

## Connection String Patterns

### Self-Managed VM
- server_url = f"mysql+pymysql://{VM_DB_USER}:{VM_DB_PASS}@{VM_DB_HOST}:{VM_DB_PORT}/"

### Managed Cloud SQL
- server_url = f"mysql+pymysql://{MAN_DB_USER}:{MAN_DB_PASS}@{MAN_DB_HOST}:{MAN_DB_PORT}/"
- mysql+pymysql://USERNAME:PASSWORD@HOST:PORT/DATABASE_NAME

## Secrets Management
- All sensitive credentials are stored locally in a `.env` file that is NOT committed to GitHub. A `.env.example` file with placeholder values is provided in the repository for reference.


## Screenshots

### Self-Managed VM Path

#### 1. VM Instance Creation
![VmConfigurations1](screenshots/vm/VM1.png)
![VmConfigurations2](screenshots/vm/VM2.png)
![VmConfigurations3](screenshots/vm/VM3.png)
![VmConfigurations4](screenshots/vm/vmmade.png)
#### 2. Firewall Rules
![FirewallConfiguration1](screenshots/vm/VM4.png)
![FirewallConfiguration2](screenshots/vm/VM5.png)
![FirewallConfiguration for Port 3306](screenshots/vm/VM6.png)

#### 3. MySQL Installation, Service Status, and Script Run
![MySQLInstallation](screenshots/vm/VM7.png)
![MySQLServiceStatus](screenshots/vm/VM8.png)
![MySQLConfigChanges](screenshots/vm/VM9.png)
![MySQScript](screenshots/vm/VM10.png)

#### 4. Successful Database & Table Verification
![ShowDatabases](screenshots/vm/VM11.png)


### Managed Cloud SQL Path

#### 1. Cloud SQL Instance Creation
![InstanceConfig1](screenshots/managed/managed1.png)
![InstanceConfig2](screenshots/managed/managed2.png)
![InstanceConfig3](screenshots/managed/managed3.png)

#### 2. Adding User
![User](screenshots/managed/managed4.png)

#### 4. Connection, Successful Database & Table Verification
![Final1](screenshots/managed/managed5.png)
![Final2](screenshots/managed/managed6.png)
![Final3](screenshots/managed/managedlast.png)
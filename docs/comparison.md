# MySQL Deployment Comparison: VM vs Cloud SQL

## Setup Experience

### Self-Managed VM (Compute Engine)
The self-managed VM approach required more hands-on configuration. The process involved manually installing MySQL packages, editing configuration files (such as changing `bind-address` to `0.0.0.0`) and creating database users with proper permissions. When commands wouldn't execute properly in SSH, I had to relaunch the session. The entire process took approximately 20 minutes from VM creation to successfully running the demo script and printing the table. 

### Managed Service (Cloud SQL)
In contrast, Cloud SQL provisioning was faster and more straightforward. Creating the instance, adding authorized networks, and setting up database users took approximately 6-7 minutes total. There were no configuration files to edit manually, no services to restart, and no troubleshooting required. 

### Preference
Overall, I would personally go with a managed service. While more costly, I believe that it's extensive configurations and user friendly interface make it ideal in production. 

## Use Case Analysis

### Small Student App
**Recommendation: Self-Managed VM**

For a student application, a self-managed would be the better option. A self managed VM would be more cost effective than a managed service. A small VM instance (e2-micro or e2-small) can run continuously within GCP's free tier limits, while Cloud SQL instances incur ongoing charges even when idle. 

### Departmental Analytics Database
**Recommendation: Cloud SQL**

A departmental analytics database would go best with Cloud SQL's automated backups, point-in-time recovery, and built-in monitoring capabilities. For departments without dedicated database administrators, the managed service eliminates the burden of security patches, version updates, and maintenance windows. The ability to easily scale resources and add read replicas for read-heavy analytical workloads makes Cloud SQL ideal for this use case.

### HIPAA-Aligned Workload
**Recommendation: Cloud SQL (with BAA)**

For HIPAA-compliant workloads, Cloud SQL would be best when a Business Associate Agreement (BAA) is available. GCP's managed service includes compliance certifications, automated security patching, encrypted connections by default, and comprehensive audit logging capabilities. While a self-managed VM may be able to meet HIPAA requirements, maintaining compliance would be far more complex. 


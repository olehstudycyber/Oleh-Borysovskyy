# 🛠️ Troubleshooting GVM Installation on Kali Linux

This guide documents the troubleshooting steps taken to fix Greenbone Vulnerability Manager (GVM) installation issues on Kali Linux after an upgrade.

---

## 📌 Problem Summary

After upgrading GVM, the following error was encountered during the setup check:

Database is wrong version. You have installed a new gvmd version.

yaml
Copy
Edit

This indicated that the PostgreSQL database schema was outdated and incompatible with the new `gvmd` version.

---

## ✅ Resolution Steps

### 1. 🗃️ Database Migration

Run the following command to migrate the existing database schema:

```bash
sudo runuser -u _gvm -- gvmd --migrate
This process updates the PostgreSQL schema and synchronizes SCAP/NVT feeds.

The SCAP sync may take several minutes—be patient.

2. 🔍 Verify Installation
Once the migration is complete, verify the setup:

bash
Copy
Edit
sudo gvm-check-setup 2.3.3
✅ All checks passed successfully after the migration.

3. ⚠️ User Creation Errors
Attempts to create or reset user credentials returned PostgreSQL errors:

pgsql
Copy
Edit
md manage:WARNING: sql_open: PQconnectPoll failed
FATAL:  role "root" does not exist
This indicated that gvmd attempted to connect using the incorrect role (root).

4. 👤 Fixing User Management
Verified the database user configuration in gvmd.conf.

Created users using the correct syntax:

bash
Copy
Edit
sudo runuser -u _gvm -- gvmd --create-user=your_new_username --new-password=your_new_password
Noted the generated password for the Admin user (from earlier setup logs).

5. 🌐 GSA Web Interface Login Troubleshooting
User was unable to log in via the GSA web interface.

Actions Taken:
Checked service status:

bash
Copy
Edit
systemctl status gvmd
systemctl status gsad
Ensured usernames/passwords were case-sensitive.

Attempted login using:

The generated Admin password.

Any known or newly created user accounts.

Reset password for the default admin user:

bash
Copy
Edit
sudo runuser -u _gvm -- gvmd --user=admin --new-password=your_intended_password
Cleared browser cache and cookies.

Tried alternative browsers.

Checked GSA logs for relevant error messages.

🎉 Final Result
successfully accessed the GSA web interface. Resolution was achieved by:



Resetting the admin user password properly.

🗂️ Notes
GVM version: 2.3.3

OS: Kali Linux (latest rolling release as of April 2025)

PostgreSQL and SCAP databases updated using GVM's built-in migration tools

🧠 Lessons Learned
Always migrate the database after a GVM upgrade.

Use runuser -u _gvm for GVM-related operations.

Watch for misleading errors like database connection attempts as root.

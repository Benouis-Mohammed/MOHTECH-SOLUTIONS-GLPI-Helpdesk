
# GLPI Helpdesk & IT Asset Management
### MOHTECH Solutions — IT Support Infrastructure Lab

![GLPI](https://img.shields.io/badge/GLPI-12.0.2-blue)
![Ubuntu](https://img.shields.io/badge/Ubuntu-24.04.5-E95420)
![Apache](https://img.shields.io/badge/Web_Server-Apache2-red)
![MariaDB](https://img.shields.io/badge/Database-MariaDB-003545)
![PHP](https://img.shields.io/badge/PHP-8.3-777BB4)
![Status](https://img.shields.io/badge/Status-Completed-success)

---

## 1. Project Overview

This project demonstrates the deployment, configuration, and practical use of **GLPI (Gestionnaire Libre de Parc Informatique)** as a centralized IT Service Management (ITSM), helpdesk, and IT asset management solution.

The lab was developed around an internal IT support scenario for **MOHTECH Solutions**. Its purpose was to simulate the core responsibilities of an organization's IT department, from deploying a Linux-hosted helpdesk server to managing employee accounts, registering IT equipment, and handling support incidents.

The project combines Linux server administration with practical helpdesk operations.

### Project Objectives

- Deploy GLPI on an Ubuntu Linux virtual machine.
- Install and configure Apache2 as the web server.
- Install and configure MariaDB as the database server.
- Install PHP and the extensions required by GLPI.
- Create and configure the GLPI application database.
- Configure application directory ownership and permissions.
- Create an organizational structure with locations and departments.
- Create employee and IT technician accounts.
- Configure user profiles and authorizations.
- Register computers and printers in the asset inventory.
- Create ITIL ticket categories.
- Demonstrate a complete support ticket lifecycle, from employee submission to technician resolution and closure.

---

## 2. Lab Environment

The environment was deployed using VMware Workstation with an Ubuntu virtual machine.

| Component | Configuration |
|---|---|
| Virtualization Platform | VMware Workstation |
| Operating System | Ubuntu Desktop 24.04.5 LTS |
| Helpdesk Application | GLPI 12.0.2 |
| Web Server | Apache2 |
| Database Server | MariaDB 10.11.14 |
| PHP Version | 8.3.6 |
| Network Configuration | Bridged Networking |
| Deployment Type | Virtual Machine |

### Infrastructure Architecture

The deployment uses a web application architecture consisting of the GLPI application, Apache2, PHP, and MariaDB.

```text
                 MOHTECH SOLUTIONS
                  EMPLOYEES / IT
                        |
                        |
                   Web Browser
                        |
                        |
                Ubuntu Linux VM
                   GLPI 12.0.2
                        |
                    Apache2
                        |
                       PHP
                        |
                     MariaDB
                   GLPI Database
```

| Component | Responsibility |
|---|---|
| Ubuntu Linux | Hosts the application and supporting services |
| Apache2 | Handles HTTP requests and serves the GLPI web interface |
| PHP | Executes the GLPI application |
| MariaDB | Stores GLPI application data |
| GLPI | Provides helpdesk, ITSM, and asset management functionality |

---

# 3. Infrastructure Deployment

## 3.1 Ubuntu Virtual Machine

Created an Ubuntu Desktop 24.04.5 LTS virtual machine using VMware Workstation.

The virtual machine was configured with bridged networking to allow communication with other devices on the local network.

### Configuration

- Created and installed the Ubuntu virtual machine.
- Configured the network adapter using bridged networking.
- Updated the operating system.
- Prepared the Linux environment for the GLPI deployment.

### Evidence

![GLPI Initial Dashboard](screenshots/Glpi-initial-dashboard.png)

---

## 3.2 Apache2 Web Server

Installed Apache2 to host the GLPI web application.

Apache2 was configured to serve GLPI through its `public` directory.

### Configuration tasks

- Installed Apache2.
- Started and enabled the Apache service using `systemctl`.
- Verified the default Apache web page.
- Configured an Apache VirtualHost for GLPI.
- Set the document root to `/var/www/glpi/public`.
- Enabled the Apache rewrite module.
- Verified that the GLPI web interface was accessible locally.

**VirtualHost configuration file:**

```text
/etc/apache2/sites-available/glpi.conf
```

**Document root:**

```text
/var/www/glpi/public
```

### Apache2 Default Page

Verified that Apache2 was installed and serving its default web page.

![Apache2 Default Page](screenshots/Apache2-DefaultPage.png)

### Apache2 and MariaDB Services

Verified that both services were running.

![Apache2 and MariaDB Running](screenshots/mariadb-apache2-running.png)

---

## 3.3 MariaDB Database Server

Installed MariaDB to provide the relational database required by GLPI.

A dedicated database and database user were created for the application.

### Database configuration

| Setting | Value |
|---|---|
| Database Server | MariaDB |
| Database Name | `glpi` |
| Database User | `glpi_user` |
| Purpose | GLPI application data |

The database was verified through the MariaDB command-line interface using:

```sql
SHOW DATABASES;
```

The database credentials were entered during the GLPI web installation.

> Database passwords and other private credentials are intentionally excluded from this repository.

### Database Verification

![GLPI Database Created](screenshots/Show_databases-glpiCreated.png)

---

## 3.4 PHP Installation

Installed PHP 8.3 and the required PHP extensions for GLPI.

PHP provides the runtime environment used by the application.

The installed version was verified using:

```bash
php -v
```

**Installed PHP version:** `8.3.6`

![PHP Version Verification](screenshots/PHP-version.png)

---

## 3.5 GLPI Application Deployment

Downloaded and extracted the GLPI installation package.

The application files were deployed under:

```text
/var/www/glpi
```

Apache was configured to use the application's public directory:

```text
/var/www/glpi/public
```

This configuration exposes the public application directory rather than the entire GLPI installation directory.

### Deployment steps

1. Extracted the GLPI installation package.
2. Placed the application files under `/var/www/glpi`.
3. Configured the Apache VirtualHost.
4. Set the document root to `/var/www/glpi/public`.
5. Enabled Apache rewrite functionality.
6. Configured the required ownership and permissions.
7. Accessed the GLPI installation interface through the browser.
8. Completed the environment compatibility checks.
9. Connected GLPI to the MariaDB database.
10. Completed the installation and accessed the GLPI login page.

### Application Permissions

The GLPI configuration and storage directories were assigned to the Apache service account, `www-data`.

The following commands were used to configure ownership and permissions:

```bash
sudo chown -R www-data /var/www/glpi/files /var/www/glpi/config

sudo find /var/www/glpi/files /var/www/glpi/config -type d -exec chmod 775 {} \;

sudo find /var/www/glpi/files /var/www/glpi/config -type f -exec chmod 664 {} \;
```

These permissions allow the web server to access the required application data without granting unrestricted permissions to the entire installation.

### Extracted Application Files

![GLPI Extracted](screenshots/Glpi-Extracted.png)

### Directory Permissions and Ownership

![GLPI Permissions](screenshots/gave_gpiperms-2apache.png)

### GLPI Localhost Access

![GLPI Localhost](screenshots/GLPI-inLocalHost-done.png)

### Installation Compatibility Checks

![GLPI Initial Installation Test](screenshots/Glpi-passed-initialTest.png)

### Installation Completed

![GLPI Installation Finished](screenshots/glpi-install-finished.png)

### GLPI Login Page

![GLPI Login Page](screenshots/glpi-login-page.png)

---

# 4. GLPI Configuration

After completing the installation, GLPI was configured to represent the organizational structure and IT support operations of MOHTECH Solutions.

## 4.1 Organizational Structure and Locations

Created a location hierarchy under GLPI to organize employees and assets by department.

### Configured structure

```text
Main Office
|
|-- HR Department
|
|-- IT Department
|
|-- Sales Department
```

This structure allows users and equipment to be associated with their respective departments and locations.

### Evidence

![Created Locations and Departments](screenshots/Created-locations-departments.png)

---

## 4.2 User and Access Management

Created three user accounts representing employees from different departments and an IT technician responsible for handling support requests.

### User accounts

| Full Name | Username | Department | Access Configuration |
|---|---|---|---|
| Benouis Youcef | `youcef.hr` | HR | Self-Service |
| Mansour Youness | `youness.sales` | Sales | Self-Service |
| Khalil Ahmed | `ahmed.it` | IT | Technician authorization |

### Configuration tasks

- Created employee and technician accounts.
- Assigned users to their respective department locations.
- Configured Self-Service access for employees.
- Configured the IT support account.
- Added the Technician authorization for the IT technician.
- Verified access through the employee self-service interface.

Employees can use the Self-Service interface to submit and track support requests, while IT personnel manage and resolve tickets through the standard GLPI interface.

### Created Users

![GLPI Users Created](screenshots/Users-created.png)

### HR Employee Login

Verified access through the HR employee account.

![Logged In as HR](screenshots/LoggedIn-as-hr.png)

---

## 4.3 IT Asset Management

Configured the GLPI asset inventory to represent the equipment used by the company.

Registered three computers and one printer.

### Registered assets

| Asset Name | Department / Location | Assigned User | Asset Identifier |
|---|---|---|---|
| `HR-LAPTOP-01` | HR Department | Benouis Youcef | `MOH-LAP-001` |
| `SALES-PC-01` | Sales Department | Mansour Youness | `MOH-PC-001` |
| `IT-PC-01` | IT Department | Khalil Ahmed | `MOH-PC-002` |
| `MAIN-OFFICE-PRINTER-01` | Main Office | Khalil Ahmed | `MOH-PRN-001` |

### Inventory Summary

| Asset Type | Quantity |
|---|---:|
| Computers | 3 |
| Printers | 1 |
| **Total Assets** | **4** |

Each asset was registered and associated with its respective user and organizational location.

This provides a centralized inventory that can help IT personnel identify equipment associated with an employee or support request.

### Computers Added

![Computers Added to GLPI](screenshots/Added-Computers.png)

### Complete Inventory

![GLPI Inventory - Three Computers and One Printer](screenshots/Inventory-3c1p.png)

---

## 4.4 IT Ticket Categories

Created ITIL ticket categories to classify incoming support requests.

### Categories configured

| Category | Code | Purpose |
|---|---|---|
| Hardware | HW | Computer and hardware-related incidents |
| Software | SW | Operating system and application problems |
| Network | NET | Network connectivity and communication issues |
| Accounts & Access | ACC | User accounts and access-related problems |
| Printers | PRN | Printer and printing-related incidents |

These categories help organize support requests and make it easier for the IT department to identify the type of assistance required.

### Evidence

![GLPI IT Ticket Categories](screenshots/ITtickets-categories-created.png)

---

# 5. Helpdesk Workflow — Ticket Lifecycle

The final stage of the project was to demonstrate a complete support incident lifecycle in GLPI.

An employee submitted a network connectivity incident through the Self-Service portal. The IT technician then investigated the issue, documented the troubleshooting activity, and recorded a solution.

## 5.1 Ticket Submission

Benouis Youcef (`youcef.hr`), an HR employee, submitted a network incident through the GLPI Self-Service interface.

### Ticket details

| Field | Value |
|---|---|
| Ticket ID | `1` |
| Requester | Benouis Youcef (`youcef.hr`) |
| Ticket Type | Incident |
| Category | Network |
| Priority | High |
| Initial Status | New |
| Associated Asset | `HR-LAPTOP-01` |
| Assigned Technician | Khalil Ahmed (`ahmed.it`) |
| Title | Unable to connect to Wi-Fi |

### Reported issue

> My HR laptop cannot connect to the office Wi-Fi. Other employees appear to be connected normally. Please investigate.

The incident was categorized as a Network issue and associated with the employee's laptop.

### Evidence — First Ticket

![First GLPI Ticket](screenshots/First-ticket.png)

---

## 5.2 Ticket Assignment and Investigation

The incident was assigned to IT technician Khalil Ahmed (`ahmed.it`) for investigation.

A task was added to document the initial troubleshooting activity directly within the ticket.

### Troubleshooting task

> Investigated the Wi-Fi issue. Checked the network adapter settings and confirmed further troubleshooting is required.

This demonstrates how an IT technician can document investigation activities and maintain a record of work performed on a support request.

### Evidence — Administrator Ticket View

![Ticket Solved - Administrator View](screenshots/Ticket-solved-admin.png)

---

## 5.3 Solution and Ticket Closure

After troubleshooting the wireless connectivity issue, a solution was added to the ticket.

### Documented solution

> Wi-Fi connectivity was restored. The employee can now connect to the office network.

The employee reviewed and approved the proposed solution.

**Solution approval:** Accepted on 2026-11-25 at 13:49 by Benouis Youcef.

The ticket subsequently reached **Closed** status.

### Ticket lifecycle

```text
Employee submits incident
          |
          v
Ticket created in GLPI (#1)
          |
          v
Ticket assigned to IT
          |
          v
Technician investigates
          |
          v
Troubleshooting documented
          |
          v
Solution added
          |
          v
Employee approves solution
          |
          v
Ticket closed
```

### Evidence — Ticket Resolution

![Ticket Solved](screenshots/Ticket-solved.png)

![Ticket Closed - Administrator View](screenshots/Ticket-solved-admin.png)

---

# 6. Skills and Technical Knowledge Demonstrated

This project combines Linux administration, web server deployment, database configuration, and practical IT support workflows.

### Linux Administration

- Ubuntu Linux installation and configuration.
- Linux command-line administration.
- Service management using `systemctl`.
- Application directory management.
- File ownership using `chown`.
- File and directory permissions using `chmod`.
- Installing and managing software packages.

### Web Server Administration

- Apache2 installation and configuration.
- Apache VirtualHost configuration.
- DocumentRoot configuration.
- Enabling Apache modules.
- Hosting a PHP-based web application.

### Database Administration

- MariaDB installation and service verification.
- Database creation.
- Dedicated application database user configuration.
- Database verification through the command line.
- Configuring a web application to use a database.

### IT Support and Helpdesk

- GLPI deployment and configuration.
- Organizational location and department management.
- User account and access profile configuration.
- IT asset inventory management.
- ITIL ticket categorization.
- Incident assignment.
- Troubleshooting documentation.
- Solution submission and ticket closure.

### IT Infrastructure

- VMware Workstation virtual machine deployment.
- Bridged networking configuration.
- Linux server environment preparation.
- Web application architecture.
- Integration of Apache2, PHP, and MariaDB.

---

# 7. Future Improvements

The current implementation provides a functional foundation for a small company helpdesk environment.

Potential improvements include:

- **Active Directory / LDAP Integration:** Connect GLPI to the existing MOHTECH Active Directory lab to centralize user authentication and directory synchronization.
- **Expanded Asset Inventory:** Register additional workstations, network switches, access points, and peripherals.
- **Additional Ticket Scenarios:** Simulate hardware failures, software issues, account lockouts, and printer incidents.
- **Automated Inventory:** Explore GLPI Agent deployment to collect hardware and software information from client machines.
- **Network Monitoring Integration:** Explore connecting infrastructure monitoring alerts with helpdesk workflows using tools such as PRTG.

These are potential extensions and are not part of the current completed implementation.

---

# 8. Project Outcome

Successfully deployed and configured GLPI 12.0.2 on Ubuntu Desktop 24.04.5 LTS using Apache2, PHP 8.3.6, and MariaDB 10.11.14.

The completed lab demonstrates:

- A functioning GLPI helpdesk and ITSM environment.
- A structured company location hierarchy.
- Employee Self-Service accounts and IT technician access.
- A registered inventory of three computers and one printer.
- Five configured IT ticket categories.
- A complete support incident lifecycle, from employee submission to technician investigation, solution approval, and ticket closure.

This project provided practical experience with Linux-hosted application deployment, web server configuration, database administration, IT asset management, and helpdesk operations.

---

# 9. Repository Structure

```text
MOHTECH-GLPI-Helpdesk/
|
|-- README.md
|
|-- screenshots/
    |
    |-- Added-Computers.png
    |-- Apache2-DefaultPage.png
    |-- Created-locations-departments.png
    |-- First-ticket.png
    |-- gave_gpiperms-2apache.png
    |-- Glpi-Extracted.png
    |-- Glpi-initial-dashboard.png
    |-- GLPI-inLocalHost-done.png
    |-- glpi-install-finished.png
    |-- glpi-login-page.png
    |-- Glpi-passed-initialTest.png
    |-- Inventory-3c1p.png
    |-- ITtickets-categories-created.png
    |-- LoggedIn-as-hr.png
    |-- mariadb-apache2-running.png
    |-- PHP-version.png
    |-- Show_databases-glpiCreated.png
    |-- Ticket-solved.png
    |-- Ticket-solved-admin.png
    |-- Users-created.png
```

---

## Disclaimer

This project is a practical virtual lab developed for educational and portfolio purposes using an internal company IT support scenario.

It is not a production deployment. It demonstrates the deployment and administration of a helpdesk and asset management solution in a controlled virtual environment.

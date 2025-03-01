# GCP VM Migration: USA to Australia Region

## Migration of Intercontinental VM (USA Region > Australia Region) using Storage Snapshot through Google Cloud Internal Private Network in less than 30 minutes

<p align="center">
<img src="https://i.imgur.com/DlnlVs5.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

## Project Description
The project involves migrating virtual machine (VM) instances from the United States (Oregon region) to Australia (Sydney region) using Google Cloud Platform's (GCP) snapshot capabilities over the internal private network. The objective is to perform this migration within a time frame of less than 30 minutes, ensuring minimal downtime and continuity of service. The application stack includes a Node.js application and a MySQL database, both hosted on Debian GNU/Linux instances.

## Project Objectives
1. VM Creation: Set up two GCP instances (one for the application and one for the database) in the us-west1 (Oregon) region.
2. Database Setup: Install and configure MySQL on the database instance.
3. Application Deployment: Install the necessary dependencies for the Node.js application and configure it to connect to the database.
4. Snapshot Creation: Create snapshots of both VM instances to facilitate migration.
5. Disk Creation in New Region: Utilize the snapshots to create new disks in the australia-southeast1 (Sydney) region.
6. Instance Creation: Deploy new VM instances in the Sydney region using the newly created disks.
7. Application Configuration: Update application configurations to point to the new database instance.
8. Testing: Ensure that the application is accessible and functioning correctly post-migration.

## Project Solution
1. VM Instances Creation:
   - Two instances were created in the us-west1 region:
     - Application instance (usa-app01) with an e2-micro size.
     - Database instance (usa-db01) with an e2-micro size.
2. Database Installation and Setup:
   - MySQL server was installed and configured with secure settings.
   - A database and necessary user privileges were established.
3. Application Deployment:
   - The application files were downloaded and unzipped.
   - Application settings were modified to connect to the MySQL database.
   - Required npm packages were installed, and the application was started.
4. Firewall Rule Creation:
   - A firewall rule was established to allow TCP access on port 3000 for the application.
5. Migration Process:
   - Snapshots of the VM disks were created using the gcloud compute disks snapshot command.
   - New disks were created in the australia-southeast1 region from the snapshots.
   - New VM instances (aus-app01 and aus-db01) were created in the Sydney region using the newly created disks.
6. Post-Migration Configuration:
   - The application was accessed via SSH, and the necessary configuration updates were made.
   - The application was started, and functionality was verified by accessing it via the browser.

## Tools and Technologies
- Google Cloud Platform (GCP): The cloud provider used for hosting and migrating VMs.
- Compute Engine: For creating and managing virtual machine instances.
- MySQL: The database management system used for data storage.
- Node.js: The runtime environment for executing the application code.
- Debian GNU/Linux: The operating system used for the VM instances.
- gcloud CLI: Command-line tool for managing resources on GCP.

## Project Solution Part 1: Setting Up Google Cloud Compute Instances and MySQL Database

### Step 1: Creating Compute Engine Instances

1. Create Application Instance:
   - Navigate to the Google Cloud Platform (GCP) console.
   - Click on Compute Engine and then VM Instances.
   - Click on Create Instance.
     - Instance Name: USA-app-01
<p align="center">
<img src="https://i.imgur.com/GXgXrzT.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - Region: us-west1 (Oregon)
<p align="center">
<img src="https://i.imgur.com/fdBpC6l.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - Zone: us-west1-b
<p align="center">
<img src="https://i.imgur.com/0sVKu7l.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - Machine Type: E2 Micro
<p align="center">
<img src="https://i.imgur.com/QfuY6ed.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - Operating System: Debian 11
<p align="center">
<img src="https://i.imgur.com/Ds6rOGm.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - After configuring the settings, click Create to provision the instance.
<p align="center">
<img src="https://i.imgur.com/M5OdINk.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

2. Create Database Instance:
   - Follow the same steps to create another instance.
     - Instance Name: USA-DB-01
<p align="center">
<img src="https://i.imgur.com/9TwmeA7.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - Region: us-west1
<p align="center">
<img src="https://i.imgur.com/wfI0y1T.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - Zone: us-west1-b
<p align="center">
<img src="https://i.imgur.com/0sVKu7l.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - Machine Type: E2 Micro
<p align="center">
<img src="https://i.imgur.com/QfuY6ed.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - Operating System: Debian 11
<p align="center">
<img src="https://i.imgur.com/Ds6rOGm.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - Click Create to provision the database instance.
<p align="center">
<img src="https://i.imgur.com/zrh3H32.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

3. Accessing Instances:
   - Once both instances are running, establish an SSH connection to the application instance (USA-app-01) by clicking the SSH button.
<p align="center">
<img src="https://i.imgur.com/k1vjKpv.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

<p align="center">
<img src="https://i.imgur.com/oxYPYuy.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - Open another SSH connection to the database instance (USA-DB-01).
<p align="center">
<img src="https://i.imgur.com/4IVaBD2.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

### Step 2: Installing MySQL on the Database Instance

1. Update the Operating System:
   - On the database instance, run:
<p align="center">
<img src="https://i.imgur.com/SNiVUQ8.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

2. Install wget:
   - Install wget to download files:
<p align="center">
<img src="https://i.imgur.com/nzMMk7a.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

3. Download and Install MySQL:
   - Use wget to download the MySQL installer:
<p align="center">
<img src="https://i.imgur.com/0yUoARV.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - Install MySQL using the downloaded package:
<p align="center">
<img src="https://i.imgur.com/hu5OSKh.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

<p align="center">
<img src="https://i.imgur.com/pKegFFo.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

4. Configure MySQL Installation:
   - During installation, select the default options and set the root password as welcome1.
   - Choose the legacy authentication method when prompted.

5. Install MySQL Server:
   - Update package lists again:
<p align="center">
<img src="https://i.imgur.com/rFHbzOX.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - Install MySQL 8 Server
<p align="center">
<img src="https://i.imgur.com/R56ZI8Y.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - Once the installation completes, you can verify the installation and check MySQL's status with:
<p align="center">
<img src="https://i.imgur.com/St6ecS1.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

6. Secure MySQL Installation:
   - Restart the MySQL service 
   - Run the secure installation command
<p align="center">
<img src="https://i.imgur.com/nSCEv0q.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - When prompted for the root password, enter welcome1.
   - Answer 'no' to all security questions for now.

### Step 3: Setting Up the Database

1. Download SQL File:
   - Use wget to download a SQL file containing the necessary table creation commands:
<p align="center">
<img src="https://i.imgur.com/Bxe4LQu.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

2. Connect to MySQL:
   - Access MySQL using the root user:
<p align="center">
<img src="https://i.imgur.com/vpXicRQ.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - Enter the password (welcome1).

3. Run SQL Commands:
   - Source the downloaded SQL file to create the database and tables:
<p align="center">
<img src="https://i.imgur.com/3Zl73jc.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

4. Create Application User:
   - Create a new user for the application to access the database:
<p align="center">
<img src="https://i.imgur.com/03hxyrR.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

5. Exit MySQL:
   - Type exit to leave the MySQL prompt.
<p align="center">
<img src="https://i.imgur.com/tAqdMov.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

### Step 4: Preparing the Application Instance

1. Update the Application Instance:
   - On the application instance (USA-app-01), run
<p align="center">
<img src="https://i.imgur.com/jnYccGp.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

2. Install Node.js and NPM:
   - Install Node.js and NPM (Node Package Manager)
<p align="center">
<img src="https://i.imgur.com/xR5QC25.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

3. Install Additional Packages:
   - Install zip and wget
<p align="center">
<img src="https://i.imgur.com/oKnDRdV.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

<p align="center">
<img src="https://i.imgur.com/zZ4YfIR.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

4. Download and Unzip Application Files:
   - Download the application files using wget
<p align="center">
<img src="https://i.imgur.com/e0LEhph.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - Unzip the downloaded files
<p align="center">
<img src="https://i.imgur.com/4z0M7h2.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

5. Navigate to Application Directory:
   - Change to the directory containing the application files
<p align="center">
<img src="https://i.imgur.com/KeUHfxa.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

6. Locate index.js and Configure Database Connection:
   - Inside the application directory, navigate to the src folder
<p align="center">
<img src="https://i.imgur.com/JFdSULY.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - Open the index.js file with vi to configure the database connection.
<p align="center">
<img src="https://i.imgur.com/eOFQZPP.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - In index.js, locate the line with the host configuration. Update it with the private IP of the MySQL instance from usa-db01.
   - Update the following configurations:
     - Host: Set to the private IP of your MySQL server.
     - User: Replace with app.
     - Password: Set to welcome1.
     - Database: Set to clinic.
   - Save and close the file.
<p align="center">
<img src="https://i.imgur.com/a5yC2Ec.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

7. Install Application Dependencies:
   - Move up one directory level where the package.json and package-lock.json files are located
<p align="center">
<img src="https://i.imgur.com/TiszUuY.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - Run npm install to install required dependencies for the application.
<p align="center">
<img src="https://i.imgur.com/foWwvM4.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

8. Start the Application:
   - Start the application using Node.js.
<p align="center">
<img src="https://i.imgur.com/ajPFEj8.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - The application will launch and listen on port 3000.

9. Configure Firewall to Allow Traffic on Port 3000:
   - Go to the VPC section in your console to create a new firewall rule.
   - Create Firewall Rule:
<p align="center">
<img src="https://i.imgur.com/NIY8mPI.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - Name: allow-app-port-3000
<p align="center">
<img src="https://i.imgur.com/67lgESk.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - Network: Use the VPC associated with your virtual machine.
<p align="center">
<img src="https://i.imgur.com/1veYiyh.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - Direction: Ingress
<p align="center">
<img src="https://i.imgur.com/Sdtc54z.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - Action: Allow
<p align="center">
<img src="https://i.imgur.com/RwT78q0.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - Source Filter: IP ranges with 0.0.0.0/0 (to allow connections from any IP).
<p align="center">
<img src="https://i.imgur.com/wTRIl2E.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - Port: 3000 (TCP)
<p align="center">
<img src="https://i.imgur.com/OcV0Ey5.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - Target: All instances in the network
<p align="center">
<img src="https://i.imgur.com/gYsP6pv.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - Click Create to apply the rule.
<p align="center">
<img src="https://i.imgur.com/ZwrwUrJ.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

10. Access the Application:
    - Copy the external IP of the usa-app01 instance.
    - Open a browser and enter http://<external-ip>:3000 to access the application UI.

11. Verify Database Connectivity:
    - In the application UI, add a new patient record to verify the database connection.
    - Patient Name: e.g., David Blue
    - Address: e.g., 998 South Road
    - Phone Number: e.g., 777-888-2222
    - Click Save Patient to confirm that the entry is saved to the database. This ensures that the application server and database server are correctly configured and communicating.
<p align="center">
<img src="https://i.imgur.com/vwttnc8.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

## Project Solution Part 2: Migration of Virtual Machines to Australia

### Overview
In this part of the project, we will migrate our application and database virtual machines (VMs) from the US West region to the Australia region. This migration involves creating snapshots of the current disks, transferring these snapshots to the new region, and launching new VMs in Australia using these snapshots. The goal is to ensure minimal downtime and data consistency during the migration process.

### Steps for Migration

1. Stop the Virtual Machines
   - To prevent any changes to the application data during the migration, we first stop both the database and application VMs. This ensures data consistency.
   - In the Google Cloud Console, navigate to the VM instances, select the instances, and choose Stop from menu.
<p align="center">
<img src="https://i.imgur.com/w7R5Cbn.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

2. Create Snapshots of Persistent Disks
   - We need to create snapshots of the persistent disks attached to the VMs. This is crucial for transferring the data to the new region.
   - Instead of using the console, we will utilize the Google Cloud SDK (gcloud) for a more professional approach.
   - Open the Cloud Shell and execute the following command to create a snapshot of the database VM disk:
<p align="center">
<img src="https://i.imgur.com/0marwUv.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - Replace <db-disk-name>, <us-zone>, and <snapshot-name> with the appropriate values for your setup.
   - Authorize the command when prompted, and the snapshot will be created in the US region.
   - Next, create a snapshot for the application VM disk:
<p align="center">
<img src="https://i.imgur.com/15yhMOo.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - Monitor the snapshot creation process to ensure both snapshots are available.

3. Create New Disks in Australia from Snapshots
   - After the snapshots are ready, we will create new disks in the Australia region using these snapshots.
   - For the database disk, execute the following command
<p align="center">
<img src="https://i.imgur.com/L7wi12M.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - For the application disk, run:
<p align="center">
<img src="https://i.imgur.com/hcTafXz.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - This process utilizes Google Cloud's high-performance internal backbone to transfer the necessary data blocks from the US region to Australia.

4. Create New Virtual Machines in Australia
   - With the new disks created, we can now set up the new VMs in Australia.
   - Use the following command to create the application VM:
<p align="center">
<img src="https://i.imgur.com/kkztBD6.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - For the database VM, use
<p align="center">
<img src="https://i.imgur.com/lWprUye.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - Ensure that the machine type and zone are the same as the original VMs to maintain performance characteristics.

5. Verify VM Status
   - After running the commands, check the Google Cloud Console to ensure that both new VMs are running in the Australia region and that the original VMs in the US are stopped.
<p align="center">
<img src="https://i.imgur.com/1XEJxy2.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

<p align="center">
<img src="https://i.imgur.com/dB2KB3x.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

6. Update Application Configuration
   - We need to update the application configuration to connect to the new database VM.
   - SSH into the new application VM using the Cloud Console or gcloud
<p align="center">
<img src="https://i.imgur.com/w1YdKkY.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - Navigate to the application files, typically located in the /bootcamp/src/ directory, and edit the index.js file to update the database IP address
<p align="center">
<img src="https://i.imgur.com/KUafAwq.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

   - Replace the old database IP with the new internal IP of the database VM in Australia.
<p align="center">
<img src="https://i.imgur.com/ULNqOxH.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

<p align="center">
<img src="https://i.imgur.com/IqMvZrD.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

7. Restart the Application
   - After saving the changes to the index.js file, restart the application to apply the new configuration.
<p align="center">
<img src="https://i.imgur.com/pKUjwRV.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

8. Access the Application:
   - Copy the external IP of the aus-app01 instance.
   - Open a browser and enter http://<external-ip>:3000 to access the application UI.
<p align="center">
<img src="https://i.imgur.com/QPzaxzz.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

<p align="center">
<img src="https://i.imgur.com/1s1yEWI.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

## Project Conclusion
The migration of VM instances from the USA to Australia was successfully completed within the targeted time frame of 30 minutes. The process involved creating and configuring instances, setting up a MySQL database, and ensuring application functionality after migration. The project demonstrated the effectiveness of using GCP's snapshot capabilities for intercontinental VM migration with minimal downtime.

### Challenges Encountered
- Network Configuration: Ensuring that the application could access the database over the private network after migration required careful configuration of the firewall and internal IP settings.
- Data Integrity: Maintaining data integrity during the snapshot and migration process was crucial. It required thorough testing post-migration to ensure all data was intact and accessible.

### Lessons Learned
- Snapshot Management: Understanding the nuances of snapshot management in GCP is vital for effective migration strategies. This includes knowing the best practices for snapshot creation and restoration.
- Configuration Consistency: Consistency in configuration across environments (development, testing, production) is essential to prevent issues during migration.

### Future Improvements
- Automation: Implementing scripts to automate the snapshot creation and instance provisioning processes could further reduce migration time and effort.
- Monitoring Tools: Integrating monitoring tools to keep track of application performance during and after the migration would help in identifying and addressing potential issues more proactively.
- Documentation: Enhancing documentation of the migration process for future reference can help streamline similar projects.

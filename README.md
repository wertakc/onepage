# Automated Web Infrastructure and Deployment on AWS

This repository contains a lightweight, custom-built Continuous Deployment (CD) pipeline designed to host and automatically update a web application on an AWS EC2 instance. The project focuses on automating server management tasks, reducing manual intervention, and ensuring consistent delivery of updates.

## Project Overview

The goal of this project was to move away from manual file transfers and establish a self-sustaining deployment lifecycle. By utilizing Bash scripting and Linux system utilities, I created an environment where code changes pushed to GitHub are automatically reflected on a live production server within minutes.

## Core Features and Workflow

The deployment process is governed by a central automation script that performs the following operations:

* **Intelligent Environment Setup:** The script monitors the server’s temporary directory. If the environment is cleared (e.g., after a system reboot), it automatically re-initializes by cloning the repository.
* **Continuous Updates:** For existing installations, the script performs a `git pull` to fetch the latest revisions from the remote repository.
* **Dynamic Content Injection:** Using the `sed` stream editor, the script identifies placeholders within the source code and replaces them with environment-specific information (such as personal contact details), allowing for a single codebase to be used across different deployment scenarios.
* **Atomic Deployment:** Once the files are processed, they are force-copied to the web server’s root directory (`/var/www/html`), ensuring the live site is updated instantly without downtime.
* **Scheduled Execution:** The entire process is managed by a Linux Cron job, which triggers the deployment script every 10 minutes to maintain synchronization between the repository and the server.

## Technical Stack

* **Cloud Provider:** AWS (EC2 Instance running Amazon Linux)
* **Web Server:** Apache (httpd)
* **Scripting:** Bash Shell
* **Version Control:** Git
* **Scheduling:** Linux Crontab

## How to Run

To implement this deployment system on your own instance, follow these steps:

1. Ensure that Git and Apache are installed and the web server is running:
```bash
sudo dnf install httpd git -y
sudo systemctl start httpd

```


2. Clone this repository or copy the deployment script to your project directory.
3. Grant execution permissions to the script:
```bash
chmod +x script.sh

```


4. Run the script manually to verify the initial deployment:
```bash
./script.sh

```


5. To automate the process, add the script to your crontab (e.g., every 10 minutes):
```bash
(crontab -l 2>/dev/null; echo "*/10 * * * * /home/ec2-user/proje/script.sh") | crontab -

```



## Key Achievements

Through this project, I demonstrated the ability to:

* Configure and secure cloud infrastructure on AWS.
* Manage Linux system administration tasks, including user permissions and service management.
* Implement automation logic to solve real-world deployment challenges.
* Establish a basic but effective DevOps culture of continuous delivery.

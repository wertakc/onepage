# Automated Web Deployment Pipeline

This project features a custom-built Continuous Deployment (CD) solution designed to synchronize a web application with a remote Git repository. By automating the fetching, processing, and deployment stages, it eliminates manual intervention and ensures that the production environment always reflects the latest codebase.

## Project Overview

The core of this repository is a Bash-based automation engine that manages the lifecycle of a static web application. It is designed for developers who want a lightweight alternative to heavy CI/CD tools, providing a reliable way to deploy updates to a web server automatically.

## Technical Workflow

The deployment logic within `script.sh` follows a structured sequence:

* **Environment Initialization:** The script checks for the existence of the project directory in the system's temporary storage. If the directory is missing (e.g., after a system cleanup or reboot), it automatically re-initializes by cloning the repository.
* **Synchronized Updates:** If the project already exists locally, the script performs a `git pull` to fetch the latest changes from the remote main branch.
* **Dynamic Content Processing:** Utilizing the `sed` stream editor, the script identifies specific placeholders within the HTML files and replaces them with environment-specific information. This allows for seamless personalization without modifying the source code manually.
* **Production Deployment:** Once the processing is complete, the finalized files are synchronized with the web server’s root directory, ensuring the live application is updated atomically.
* **Scheduled Automation:** The pipeline is designed to be triggered via system-level scheduling (such as Cron), allowing for consistent, hands-off updates.

## Technical Stack

* **Operating System:** Linux
* **Scripting Language:** Bash
* **Version Control:** Git
* **Web Server Support:** Compatible with Apache, Nginx, or any standard web server.
* **Task Scheduling:** Linux Crontab

## Installation and Usage

To implement this pipeline in your own environment, follow these steps:

1. **Prepare the Web Server:** Ensure your web server (e.g., Apache or Nginx) is installed and active. Ensure the destination directory is accessible.
2. **Configure the Script:** Open `script.sh` and update the variables (such as repository URL and destination paths) to match your local environment.
3. **Set Permissions:** Grant execution rights to the script:
```bash
chmod +x script.sh

```


4. **Manual Trigger:** Run the script once to verify the initial deployment:
```bash
./script.sh

```


5. **Automate:** Add the script to your system's crontab for continuous updates.
Open the crontab editor:
```bash
crontab -e

```


Add a line to define the execution frequency (e.g., every 10 minutes):
```bash
*/10 * * * * /path/to/your/script.sh

```



## Key Achievements

This project demonstrates proficiency in:

* Developing robust automation logic using Bash.
* Managing Linux system environments and file structures.
* Implementing stream editing for dynamic content management.
* Establishing basic DevOps principles through automated delivery pipelines.
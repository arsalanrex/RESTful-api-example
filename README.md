
# Deploy a Simple RESTful API Across the VMs

This guide walks you through deploying a simple Python Flask-based RESTful API across two virtual machines (VMs). VM1 will run the API server, while VM2 will be the client to communicate with the API on VM1.

## Prerequisites

- Two virtual machines (VM1 and VM2) with Ubuntu-based operating systems.
- Network connectivity between VM1 and VM2.
- Basic understanding of Python, Flask, and networking.

## Step 1: Install Python and Flask on VM1

First, we'll install Python, pip, and Flask on VM1.

### 1.1 Update the Package List and Install Python

On **VM1**, run the following commands to update the system and install Python and pip:

```bash
sudo apt update
sudo apt install -y python3 python3-pip
sudo apt install python3-venv
```

### 1.2 Create a Project Directory on VM1 and activate venv

```bash
mkdir flask_api && cd flask_api
python3 -m venv venv
source venv/bin/activate
```

### 1.3 Install Flask

Next, install Flask using `pip`:

```bash
pip install flask
```

## Step 2: Create the Simple Flask API on VM1

### 2.1 Create API File

On **VM1**, navigate to the project directory:

```bash
mkdir ~/flask_api && cd ~/flask_api
```

Create a new file called `app.py`:

```bash
nano app.py
```

Paste the Python code into `app.py`:

Save and exit the file (`CTRL + X`, then `Y` to confirm, and `Enter` to save).

### 2.3 Allow External Access to the Flask API

Allow external access to the Flask API by opening port 5000 on **VM1**'s firewall:

```bash
sudo ufw allow 5000/tcp
```

### 2.4 Start the Flask Server

Start the Flask server by running the following command:

```bash
python3 app.py
```

This will run the API server on `http://0.0.0.0:5000`, making it accessible from other machines in the network.

## Step 3: Test the API from VM2

### 3.1 Install `curl` on VM2

On **VM2**, ensure that `curl` is installed to test the API request:

```bash
sudo apt install -y curl
```

### 3.2 Test the API

Use `curl` to test the API by sending a GET request to VM1's API server. Replace `192.168.xx.xxx` with the actual IP address of VM1:

```bash
curl http://192.168.xx.xxx:5000/api/hello
```

Use ifconfig command to get the IP address of VM1.

### Expected Output

You should receive the following JSON response from the API:

```json
{"message": "Hello from VM1!"}
```

This confirms that the API is up and running and VM2 is able to successfully communicate with VM1.


## Troubleshooting

- If VM2 cannot access the API, verify the firewall rules on **VM1** and ensure that port 5000 is open.
- Make sure the IP address of VM1 is correct and reachable from VM2.
- Check if the Flask application is running properly on VM1.

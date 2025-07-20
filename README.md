# N8N Docker & NGROK Public Setup - Free Production Solution

## Introduction
This repository provides a step-by-step guide to expose your self-hosted N8N server to the internet using Docker and NGROK. With this setup, you can run and access N8N workflows securely from anywhere, without the need for cloud hosting or domains.

n8n-docker-ngrok-public-setup/
│
├── README.md
├── docker-compose.yml (Optional)
├── ngrok_config.md (Optional)
├── docker_setup.md (Optional)
└── LICENSE (Optional)


### Key Benefits:
- **Remote Access**: Run your N8N workflows from any device.
- **Zero Cloud Fees**: No cloud hosting or domain registration needed.
- **Security**: NGROK provides an HTTPS tunnel for secure access.
- **Cost-Free**: Avoid the costs of cloud-based solutions for production-grade automation.

## Prerequisites
- **Docker**: A platform for running N8N in containers. Download it from [Docker's official site](https://www.docker.com/products/docker-desktop).
- **NGROK**: A tunneling service to expose local servers to the internet securely. Download it from [NGROK's official site](https://ngrok.com/).
- **N8N**: Workflow automation tool, downloaded via Docker.

## Installation

### Step 1: Install Docker
1. Download and install Docker from [Docker's download page](https://www.docker.com/products/docker-desktop).
2. Follow the installation instructions based on your operating system.

### Step 2: Install NGROK
1. Create a free account at [NGROK](https://ngrok.com/).
2. Install NGROK via CLI by following the instructions on [this page](https://ngrok.com/download).
3. Authenticate NGROK by running the following command in the terminal:
    ```bash
    ngrok authtoken <your_token>
    ```

### Step 3: Install N8N
1. Pull the latest N8N Docker image:
    ```bash
    docker pull n8nio/n8n
    ```

2. Run the N8N container:
    ```bash
    docker run -d -p 5678:5678 --name n8n --volume n8n-data:/root/.n8n n8nio/n8n
    ```

---

## Setup Instructions

### Step 1: Install and Configure NGROK
1. **Sign Up**: Create a free NGROK account.
2. **Download NGROK**: Install NGROK by following the [installation guide](https://ngrok.com/download).
3. **Start Tunnel**: Run NGROK in your terminal to expose your local N8N:
    ```bash
    ngrok http 5678
    ```

### Step 2: Update N8N Docker Configuration
1. **Stop Existing Container**: 
    ```bash
    docker stop n8n
    docker rm n8n
    ```

2. **Run New N8N Container with Environment Variables**:
    ```bash
    docker run -d -p 5678:5678 --name n8n \
      --env N8N_EDITOR_BASE_URL="https://<your-ngrok-url>.ngrok.io" \
      --env N8N_WEBHOOK_URL="https://<your-ngrok-url>.ngrok.io" \
      --env N8N_DEFAULT_BINARY_DATA_MODE="filesystem" \
      --volume n8n-data:/root/.n8n n8nio/n8n
    ```

---

### Step 3: Enable Public Access
1. **Run NGROK** to expose the N8N editor to the web:
    ```bash
    ngrok http 5678
    ```
2. You will receive a public URL (e.g., `https://<your-ngrok-url>.ngrok.io`), which will be used to access the N8N instance remotely.

---

## Security & Best Practices
- **Use Environment Variables**: Always configure sensitive variables (like webhook URLs) using Docker environment variables.
- **NGROK Authentication**: Make sure NGROK is linked with your account to ensure a stable connection.

## Contributing
We welcome contributions to improve the setup! Feel free to open issues for bug reports or submit pull requests for improvements.

---

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.


# Mockoon and Ngrok Docker Setup

This repository contains the configuration to set up Mockoon and Ngrok using Docker. The setup allows you to run a mock API using Mockoon and expose it to the internet using Ngrok.

## Prerequisites

- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)

## Setup Instructions

### Step 1: Ngrok Configuration

1. **Register for an Ngrok Account**:
   - If you don't have an Ngrok account, sign up for a free account at [ngrok.com](https://ngrok.com/).
   
2. **Set Ngrok Authentication Token**:
   - Update the `config/ngrok.yaml` file with your Ngrok authentication token.

#### `config/ngrok.yaml`

```yaml
version: "2"
authtoken: "<YOUR_NGROK_AUTH_TOKEN>"
tunnels:
  mockoon:
    proto: http
    addr: mockoon:3000
```

Replace `<YOUR_NGROK_AUTH_TOKEN>` with your actual Ngrok authentication token.

### Step 2: Mockoon Configuration

1. **Update `mockoon.json`**:
   - If you have custom Mockoon configurations, update the `config/mockoon.json` file accordingly. You can also generate this JSON file using the [Mockoon Desktop](https://mockoon.com/download/).

### Step 3: Entrypoint Script

1. **Ensure Execution Permissions**:
   - Make sure the `entrypoint.sh` script has execution permissions.

```sh
chmod +x entrypoint.sh
```

### Step 4: Start the Services

1. **Run Docker Compose**:
   - Start the services using Docker Compose. You may need to use `sudo` depending on your Docker setup.

```sh
docker-compose down
docker-compose up -d
```

### Step 5: Verify the Setup

1. **Ngrok URL**:
   - Access the Ngrok web interface:
     ```sh
     open http://localhost:4040
     ```
   - Alternatively, you can check the logs of the Ngrok container to find the public URL:
     ```sh
     docker logs ngrok
     ```

2. **Mockoon Logs**:
   - Navigate to the logs directory on your host machine:
     ```sh
     cd ./logs
     ```
   - Check the contents of `mockoon.log`:
     ```sh
     cat mockoon.log
     ```

## Conclusion

By following these steps, you will have a Mockoon service running alongside an Ngrok service, providing a public URL to access your Mockoon API. This setup is useful for testing and developing mock APIs that need to be publicly accessible.

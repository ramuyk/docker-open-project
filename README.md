# Introduction

This repository provides a `docker-compose.yml` ready-to-use Docker configuration to simplify the deployment of the official OpenProject Docker container. For comprehensive details about extra configurations, please refer to the [OpenProject official Docker installation guide](https://www.openproject.org/docs/installation-and-operations/installation/docker/).

## Repository Contents

This repository includes:

- **Docker Compose File**: A `docker-compose.yml` file that configures the OpenProject Docker container. Highlights of this setup include:
  - **Persistent Data Storage**: Configures two volumes:
    - `openproject_pgdata` at `/var/openproject/pgdata` for storing OpenProject's PostgreSQL data.
    - `openproject_assets` at `/var/openproject/assets` for storing OpenProject's static assets and uploaded files.
    
    This setup ensures that your OpenProject configurations and data are preserved when the container is restarted.

## Getting Started

### Important Preliminary Steps

Before starting the quick setup, please note the following adjustments:

1. **Configure Network Access**:
   The `docker-compose.yml` file initially binds to `127.0.0.1:10090:80`, restricting access to the localhost only. To make the service accessible from other machines or publicly, it's crucial to change the IP address in the port mapping before starting the container for the first time. Use `0.0.0.0` to bind to all network interfaces, updating the ports line to `- "0.0.0.0:10090:80"`. This change should be made prior to creating volumes to avoid having to delete and recreate them if the IP address needs to be changed later.

2. **Environment Configuration**:
   While this setup is ready to use, it is essential to change the `OPENPROJECT_SECRET_KEY_BASE` in the Docker Compose file to a new secure key before launching your OpenProject instance. This ensures that your installation is secured from the outset.

### Volume Configuration

When setting up OpenProject for the first time, ensure that the volume configuration matches your network and security settings as outlined above. If changes to network settings are made after volumes are created, you may need to delete and recreate the volumes to apply these changes properly.

### Quick Setup

1. **Clone the Repository**:
   Clone this repository to your local machine using the following Git command:
   ```bash
   git clone https://github.com/ramuyk/docker-open-project.git
   cd docker-open-project
   ```

2. **Start OpenProject**:
   Navigate to the directory containing your `docker-compose.yml` and run:
   ```bash
   docker-compose up -d
   ```

3. **Access OpenProject**:
   Open a web browser and navigate to `http://localhost:10090` to access the OpenProject web interface. The pre-configured admin credentials are:

   - **Username**: admin
   - **Password**: admin

   Upon first login with these credentials, the OpenProject frontend will prompt you to change them for security reasons.


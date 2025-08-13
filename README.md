# Directus Self-Hosted Template

A simple, ready-to-use template for self-hosting [Directus](https://directus.io/), an open-source headless CMS and API platform.

## What is Directus?

Directus is a powerful open-source data platform that provides an instant RESTful API and an intuitive admin app for managing database content. It offers a flexible and scalable solution for managing content with a focus on data integrity and ease of use.

## Services Included

This template includes a single Directus service with:

- Directus Docker image
- SQLite database for storage
- Volume mappings for data persistence
- Environment configuration

## Prerequisites

- Docker or Podman
- Docker Compose or Podman Compose

Installing Podman for example would be: sudo pacman -S podman podman-compose

## Setup Instructions

1. **Generate a secret key:**
   ```bash
   openssl rand -base64 32
   ```

2. **Configure environment variables:**

   Edit the `compose.yml` file and set the following environment variables:
   - `SECRET`: Use the generated secret key from step 1
   - `ADMIN_EMAIL`: Your admin email address
   - `ADMIN_PASSWORD`: Your admin password

3. **Set folder permissions (if needed):**

   If you encounter permission issues with SQLite or the mounted volumes:
   ```bash
   chmod -R 777 database
   chmod -R 777 uploads
   chmod -R 777 extensions
   ```

4. **Start the services:**
   ```bash
   # With Docker
   docker-compose up -d

   # With Podman
   podman-compose up -d
   ```

   The `-d` flag runs the services in the background (detached mode).

5. **Access Directus:**

   Once the services are running, you can access the Directus admin panel at:
   ```
   http://localhost:8055
   ```

## Project Structure

```
.
├── compose.yml          # Docker Compose configuration
├── database/            # SQLite database storage
├── uploads/             # Media and file uploads
└── extensions/          # Directus extensions
```

## Configuration Options

The template includes several environment variables that can be customized:

- `SECRET`: Security key for encryption and token generation
- `ADMIN_EMAIL`: Email for the default admin user
- `ADMIN_PASSWORD`: Password for the default admin user
- `DB_CLIENT`: Database client (sqlite3 by default)
- `DB_FILENAME`: Path to the SQLite database file
- `WEBSOCKETS_ENABLED`: Enable/disable websockets (disabled by default)

Additional configuration options can be added by uncommenting or adding environment variables as needed:
- `CORS_ENABLED`: Enable CORS support
- `CORS_ORIGIN`: Specify allowed origins for CORS

## Data Persistence

This template ensures data persistence through volume mappings:

- `./database`: Contains the SQLite database file
- `./uploads`: Stores media and file uploads
- `./extensions`: Houses custom extensions

## Troubleshooting

If you encounter permission issues with the SQLite database or mounted volumes:

1. Ensure the mapped directories have appropriate write permissions:
   ```bash
   chmod -R 777 database uploads extensions
   ```

2. Check that the `DB_FILENAME` path matches the mounted volume path.

## Additional Resources

- [Directus Official Website](https://directus.io/)
- [Directus Documentation](https://docs.directus.io/)
- [Directus GitHub Repository](https://github.com/directus/directus)

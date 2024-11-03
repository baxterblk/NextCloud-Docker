# NextCloud Docker Deployment

This repository contains a Docker-based deployment configuration for NextCloud with PostgreSQL and Redis. The setup includes optimized configurations for handling large files and improved performance.

## Features

- NextCloud with Apache
- PostgreSQL database backend
- Redis for caching and session management
- Optimized PHP settings for large file handling
- Automatic HTTPS support
- Memory-optimized Redis configuration

## Prerequisites

- Docker
- Docker Compose
- Git

## Quick Start

1. Clone the repository:
```bash
git clone https://github.com/yourusername/nextcloud-docker.git
cd nextcloud-docker
```

2. Copy the example environment file and customize it:
```bash
cp .env.example .env
```

3. Edit the `.env` file and set your desired values:
```bash
# Required changes
POSTGRES_PASSWORD=your_secure_password_here
NEXTCLOUD_ADMIN_PASSWORD=your_secure_admin_password
NEXTCLOUD_TRUSTED_DOMAINS=your.domain.com your.ip.address
```

4. Create required directories:
```bash
mkdir -p nextcloud_data nextcloud_db redis_data
```

5. Start the containers:
```bash
docker-compose up -d
```

6. Access NextCloud at `http://localhost:8080` (or your configured domain)

## Configuration

### Environment Variables

Key configuration options in `.env`:

- `POSTGRES_PASSWORD`: PostgreSQL database password
- `NEXTCLOUD_ADMIN_USER`: NextCloud admin username
- `NEXTCLOUD_ADMIN_PASSWORD`: NextCloud admin password
- `NEXTCLOUD_TRUSTED_DOMAINS`: Space-separated list of trusted domains
- `PHP_MEMORY_LIMIT`: PHP memory limit (default: 4096M)
- `PHP_UPLOAD_LIMIT`: Maximum upload file size (default: 16G)
- `NEXTCLOUD_PORT`: Port to expose NextCloud on (default: 8080)

### Performance Optimizations

The deployment includes several performance optimizations:

- Redis caching for improved performance
- Optimized PostgreSQL settings
- Configured PHP memory limits for large file handling
- Apache body size limits adjusted for large uploads

### Directory Structure

```
.
├── docker-compose.yml    # Docker Compose configuration
├── .env                 # Environment configuration
├── nextcloud_data/      # NextCloud data directory
├── nextcloud_db/        # PostgreSQL data directory
└── redis_data/         # Redis data directory
```

## Maintenance

### Backup

To backup your NextCloud installation:

1. Database backup:
```bash
docker-compose exec db pg_dump -U nextcloud nextcloud > backup.sql
```

2. Data backup:
```bash
tar -czf nextcloud_data_backup.tar.gz nextcloud_data/
```

### Updates

To update the containers:

```bash
docker-compose pull
docker-compose down
docker-compose up -d
```

## Security Considerations

- Always change default passwords in the `.env` file
- Use strong passwords for database and admin accounts
- Configure trusted domains appropriately
- Keep your Docker images updated
- Enable HTTPS in production environments

## Troubleshooting

### Common Issues

1. Permission errors:
   - Ensure proper ownership of data directories
   - Check container logs: `docker-compose logs app`

2. Database connection issues:
   - Verify database credentials in `.env`
   - Check if database container is running

3. Redis connection errors:
   - Verify Redis container is running
   - Check Redis logs: `docker-compose logs redis`

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

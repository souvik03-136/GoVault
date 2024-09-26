 Distributed File Storage System

## Overview

**FileSphere** is a distributed file storage system that enables users to store, share, and retrieve files over a decentralized network of nodes. Inspired by technologies like IPFS (InterPlanetary File System) and Dropbox, this system provides secure, scalable, and fault-tolerant file storage, utilizing Go’s concurrency model for efficient communication and data management.

## Features

- **Node Communication:** Peer-to-peer (P2P) protocol for nodes to efficiently communicate and share files.
- **File Sharding and Replication:** Splits files into smaller chunks and distributes them across multiple nodes, ensuring redundancy for fault tolerance.
- **Decentralized Hash Table (DHT):** Efficient file lookup by querying the distributed network using unique file hashes.
- **File Integrity & Security:** Utilizes SHA256 for file integrity checks and encryption for secure file storage and transmission.
- **Metadata & File Tracking:** Maintains metadata for file management and tracks shard locations across the network.
- **Fault Tolerance & Availability:** Automatically reallocates shards when nodes join or leave the network.
- **Versioning and Collaboration:** Supports file versioning for collaborative editing and retrieval of older versions.
- **User Authentication & Access Control:** Implements OAuth for secure user login and defines access control rules.

## Architecture

The architecture of the FileSphere system is designed for scalability and modularity, leveraging several key components:

```
project-root/
├── cmd/
│   └── api/
│       └── main.go              # Entry point of the application
├── config/
│   └── config.go                # Configuration and environment management
├── internal/
│   ├── auth/                     # Authentication and authorization
│   │   ├── auth.go
│   │   └── middleware.go
│   ├── communication/            # P2P communication handling
│   │   ├── p2p.go
│   │   ├── grpc/
│   │   │   └── grpc_handler.go
│   │   └── websocket/
│   │       └── websocket_handler.go
│   ├── controllers/              # Request handlers for various operations
│   │   ├── file_controller.go
│   │   ├── shard_controller.go
│   │   └── version_controller.go
│   ├── database/                 # Database management
│   │   ├── migrations/
│   │   │   └── 001_create_tables.sql
│   │   └── queries/
│   │       ├── sqlc.go
│   │       └── files_queries.sql
│   ├── dht/                      # Decentralized Hash Table implementation
│   │   ├── dht.go
│   │   └── node.go
│   ├── encryption/               # Encryption utilities for secure handling
│   │   └── encryptor.go
│   ├── models/                   # Data models for application
│   │   ├── file.go
│   │   └── shard.go
│   ├── replication/              # Shard replication management
│   │   └── replicator.go
│   ├── server/                   # Server setup and handling logic
│   │   └── server.go
│   └── services/                 # Business logic and services
│       ├── metadata/
│       │   └── metadata_service.go
│       └── storage/
│           ├── storage_service.go
│           └── cache_service.go
├── migrations/                   # Database schema setup scripts
│   └── initial_schema.sql
├── pkg/                          # Reusable components
│   ├── cache/
│   │   └── cache.go
│   ├── logger/
│   │   └── logger.go
│   └── task/
│       └── task.go
├── scripts/                      # Utility scripts
│   └── setup.sh
├── schema.sql                    # SQL schema for database
├── sqlc.yaml                     # Configuration for sqlc
├── .env                          # Environment variables
├── .gitignore                    # Git ignore file
├── docker-compose.yml            # Docker Compose configuration
├── Dockerfile                    # Dockerfile for containerization
├── go.mod                        # Go module dependencies
├── go.sum                        # Go module checksums
└── README.md                     # Project documentation
```

### **Component Descriptions**

- **cmd/api:** Entry point of the application.
- **config:** Configuration files and environment variable management.
- **internal/auth:** Handles user authentication and authorization.
- **internal/communication:** Manages P2P communications and WebSocket connections.
- **internal/controllers:** Contains logic for handling file uploads, shard distribution, and version control.
- **internal/database:** Manages database migrations and SQL queries.
- **internal/dht:** Implements the Decentralized Hash Table for file location management.
- **internal/encryption:** Provides encryption and decryption utilities for secure file handling.
- **internal/models:** Data models for files and shards.
- **internal/replication:** Responsible for replicating file shards across nodes.
- **internal/server:** Contains the server setup and request handling logic.
- **internal/services:** Business logic for metadata management and storage services.
- **pkg:** Reusable components, including caching and logging utilities.
- **migrations:** SQL files for database schema setup.
- **scripts:** Utility scripts for setup and deployment.

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/filesphere.git
   cd filesphere
   ```

2. Set up your environment:
   - Copy the `.env.example` to `.env` and configure your environment variables.
   - Ensure you have Go installed (version 1.18 or later).
   - Install dependencies:
   ```bash
   go mod tidy
   ```

3. Run database migrations using `sqlc`:
   ```bash
   sqlc generate
   ```

4. Start the application:
   ```bash
   go run cmd/api/main.go
   ```

## Usage

- **Uploading a file:**
   Use the API endpoint `POST /files/upload` with the file data.
  
- **Retrieving a file:**
   Use the API endpoint `GET /files/{file_id}` to download the file.

- **View file metadata:**
   Use the API endpoint `GET /files/metadata/{file_id}`.

- **Collaborate on files:**
   Implement version control and user access through the respective endpoints.

## Advanced Features

### Smart Caching
Enhance performance by implementing a caching mechanism for frequently accessed files.

### Load Balancing
Implement load balancing strategies to distribute traffic evenly across nodes.

### CLI and Web Interface
Develop a CLI tool and a web interface for easy user interaction with the system.

## Contributing

We welcome contributions to the FileSphere project! If you'd like to contribute, please fork the repository, make your changes, and submit a pull request.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Acknowledgments

- [Golang](https://golang.org/) for its concurrency support and ease of use.
- [sqlc](https://sqlc.dev/) for generating type-safe code from SQL.
- [gRPC](https://grpc.io/) for efficient communication between nodes.
```

### License File

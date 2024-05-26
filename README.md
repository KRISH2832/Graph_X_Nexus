


# Polygon Network Subgraph Query Tool

## Overview

This tool allows users to query subgraph activity on the Polygon Network, providing up-to-date information on Matic, the native token of Polygon. The subgraph data helps to monitor and analyze various activities, transactions, and states related to Matic, offering a comprehensive view of its ecosystem.

## Features

- **Real-time Data**: Fetches the latest subgraph data for Matic on the Polygon Network.
- **Transaction Monitoring**: Tracks transactions involving Matic, including transfers, staking, and other relevant activities.
- **State Analysis**: Analyzes the current state of Matic, including total supply, circulating supply, and key holder addresses.
- **User-Friendly Interface**: Simple and intuitive interface for querying and visualizing the subgraph data.
- **Custom Queries**: Allows custom GraphQL queries to fetch specific data from the subgraph.

## Prerequisites

- Node.js (v14.x or higher)
- npm (v6.x or higher)
- GraphQL client (e.g., Apollo Client)

## Installation

1. **Clone the Repository**

    ```bash
    git clone https://github.com/KRISH2832/Graph_X_Nexus
    cd Graph_X_Nexus
    ```

2. **Install Dependencies**

    ```bash
    npm install
    ```

3. **Set Up Environment Variables**

    Create a `.env` file in the root directory and add your GraphQL endpoint URL for the Polygon subgraph:

    ```env
    GRAPHQL_ENDPOINT=https://api.thegraph.com/subgraphs/name/your-subgraph
    ```

## Running with Docker

### Docker Setup

1. **Install Docker**

   Ensure Docker is installed on your machine. You can download and install Docker from [here](https://docs.docker.com/get-docker/).

2. **Set Up Docker Compose File**

   Create a `docker-compose.yml` file in your project directory with the following content:

   ```yaml
   version: '3'
   services:
     graph-node:
       image: graphprotocol/graph-node
       ports:
         - '8000:8000'
         - '8020:8020'
         - '8030:8030'
         - '8040:8040'
         - '8050:8050'
         - '8060:8060'
       environment:
         postgres_host: postgres
         postgres_user: graph-node
         postgres_password: let-me-in
         postgres_db: graph-node
         ipfs: 'http://ipfs:5001'
         ethereum: 'mainnet:http://host.docker.internal:8545'
     ipfs:
       image: ipfs/go-ipfs:v0.4.23
       ports:
         - '5001:5001'
     postgres:
       image: postgres
       ports:
         - '5432:5432'
       environment:
         POSTGRES_USER: graph-node
         POSTGRES_PASSWORD: let-me-in
         POSTGRES_DB: graph-node
   ```

3. **Start the Services**

   Run the following command in the directory where your `docker-compose.yml` file is located:

   ```bash
   docker-compose up
   ```

   This command will start the local Graph node, IPFS, and PostgreSQL services.

### Deploying the Subgraph with Docker

After setting up the Docker environment, follow these steps:

1. **Create the Subgraph**

   ```bash
   npm run create-local
   ```

2. **Deploy the Subgraph**

   ```bash
   npm run deploy-local
   ```

## Running without Docker

### Manual Setup

1. **Install PostgreSQL**

   Install PostgreSQL and set it up. On Ubuntu, you can install it using:

   ```bash
   sudo apt update
   sudo apt install postgresql postgresql-contrib
   ```

   After installation, you need to set up a user and a database for the Graph Node:

   ```bash
   sudo -u postgres psql
   CREATE USER graph_node WITH PASSWORD 'let-me-in';
   CREATE DATABASE graph_node OWNER graph_node;
   ```

2. **Install IPFS**

   You can install IPFS by downloading it from the official IPFS website:

   ```bash
   wget https://dist.ipfs.io/go-ipfs/v0.10.0/go-ipfs_v0.10.0_linux-amd64.tar.gz
   tar xvfz go-ipfs_v0.10.0_linux-amd64.tar.gz
   cd go-ipfs
   sudo bash install.sh
   ```

   Initialize and start the IPFS daemon:

   ```bash
   ipfs init
   ipfs daemon
   ```

3. **Install The Graph Node**

   Install Rust and Cargo if they are not already installed:

   ```bash
   curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
   source $HOME/.cargo/env
   ```

   Then, install The Graph Node:

   ```bash
   git clone https://github.com/graphprotocol/graph-node.git
   cd graph-node
   cargo build --release
   ```

### Running the Graph Node

After setting up PostgreSQL, IPFS, and The Graph Node, you can start the Graph Node with the appropriate configuration.

Create a configuration file `docker-compose.yml` equivalent but for manual setup:

```yaml
# .env file
postgres_host=localhost
postgres_user=graph_node
postgres_password=let-me-in
postgres_db=graph_node
ipfs=http://127.0.0.1:5001
ethereum=mainnet:http://localhost:8545
```

Run the Graph Node:

```bash
cargo run -p graph-node --release -- \
  --postgres-url postgresql://graph_node:let-me-in@localhost:5432/graph_node \
  --ipfs $IPFS \
  --ethereum-rpc $ethereum \
  --http-port 8000 \
  --ws-port 8001 \
  --admin-port 8020 \
  --index-node-port 8030
```

### Create and Deploy the Subgraph

Once all services are running, create and deploy your subgraph locally:

1. **Create the Subgraph**

   ```bash
   npm run create-local
   ```

2. **Deploy the Subgraph**

   ```bash
   npm run deploy-local
   ```

## Usage

1. **Generate Code**

    Generate the necessary code from the GraphQL schema:

    ```bash
    npm run codegen
    ```

2. **Build the Project**

    Build the project:

    ```bash
    npm run build
    ```

3. **Deploy the Subgraph**

    - **Deploy to The Graph Studio**

        If you are deploying to The Graph Studio, use:

        ```bash
        npm run deploy
        ```

    - **Deploy to Local Environment**

        If you prefer to deploy to a local environment, ensure your local Graph node and IPFS are running, then use:

        ```bash
        npm run create-local
        npm run deploy-local
        ```

4. **Access the Interface**

    Open your web browser and navigate to `http://localhost:3000`. You will see the main dashboard where you can query and visualize the Matic-related data.

5. **Custom Queries**

    To perform custom queries, navigate to the 'Custom Query' section in the interface. You can write and execute GraphQL queries to fetch specific data.

    Example query to get the latest Matic transactions:

    ```graphql
    {
      transactions(first: 10, orderBy: timestamp, orderDirection: desc) {
        id
        from
        to
        value
        timestamp
      }
    }
    ```

## Development

### Folder Structure

- `src/`: Contains the source code.
  - `components/`: React components for the UI.
  - `graphql/`: Contains GraphQL queries and mutations.
  - `utils/`: Utility functions.
- `public/`: Public assets and the main HTML file.
- `.env`: Environment variables.



### Summary of Commands

Here is a summary of the commands based on the provided `package.json`:

- Install dependencies: `npm install`
- Generate code: `npm run codegen`
- Build the project: `npm run build`
- Deploy to The Graph Studio: `npm run deploy`
- Create local subgraph: `npm run create-local`
- Deploy locally: `npm run deploy-local`
- Run tests: `npm test`

## Contributing

Contributions are welcome! Please fork the repository and submit a pull request with your changes. Ensure that your code adheres to the project's coding standards and includes appropriate tests.

## License

This project is licensed under the MIT License. See the `LICENSE` file for more information.

---

Thank you for using the Polygon Network Subgraph Query Tool! If you have any further questions or need assistance, feel free to reach out.

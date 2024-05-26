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
    git clone https://github.com/yourusername/polygon-subgraph-query-tool.git
    cd polygon-subgraph-query-tool
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

    Depending on your deployment target, you can deploy either to a local environment or to The Graph's hosted service.

    - **Deploy to The Graph Studio**

        If you are deploying to The Graph Studio, use:

        ```bash
        npm run deploy
        ```

    - **Deploy to Local Environment**

        If you prefer to deploy to a local environment, you'll need to set up a local Graph node and IPFS node. Once those are running, use the following commands:

        - Create the subgraph:

            ```bash
            npm run create-local
            ```

        - Deploy the subgraph locally:

            ```bash
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

### Scripts

- **Start Development Server**

    ```bash
    npm start
    ```

- **Build for Production**

    ```bash
    npm run build
    ```

- **Run Tests**

    ```bash
    npm test
    ```

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

Thank you for using the Polygon Network Subgraph Query Tool! Your feedback is appreciated to help improve this tool.

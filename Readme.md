
## WebUI Vault Secrets Display

THis is a Node.js web application that serves a web page displaying values from a configuration file. It's set up to run in a Docker container and follows a modular design pattern. The application is designed to showcase how Vault Agent or Sidecar Injector can retrieve data from a Vault server and populate the `appconfigs.json` file.

This project is intended to be used in conjunction with the following repositories:

- [vault_agent_write_operation](https://github.com/Juandi-M/vault_agent_write_operation): Demonstrates how Vault Agent can write secrets to a file, which can be read by the WebUI Vault Secrets Display application.

- [vaultSideCar_k8s_expressJs](https://github.com/Juandi-M/vaultSideCar_k8s_expressJs): Illustrates how the Vault Sidecar Injector can be used in a Kubernetes environment with Express.js to retrieve secrets from a Vault server and make them available to the application.

Together, these repositories provide a comprehensive example of how to integrate HashiCorp Vault with a Node.js application to securely manage and display secrets. The WebUI Vault Secrets Display application dynamically loads the secrets from the `appconfigs.json` file, which is populated by the Vault Agent or Sidecar Injector based on the configuration and policies defined in Vault.

## Table of Contents

- [WebUI Vault Secrets Display](#webui-vault-secrets-display)
- [Table of Contents](#table-of-contents)
- [Project Map](#project-map)
- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
- [Code Explanation](#code-explanation)
- [Dependencies & packages](#dependencies--packages)
- [Contributing](#contributing)
- [License](#license)

## Project Map:
``` 
WebUI_vaultsecretsDisplay/
│
├── Dockerfile
├── docker-compose.yaml
│
└── web/
    ├── configs/
    │   └── appconfigs.json
    │
    └── js/
        ├── app.js
        ├── package.json
        │
        ├── routes/
        │   └── index.js
        │
        ├── utils/
        │   ├── configLoader.js
        │   └── htmlRenderer.js
        │
        └── webTemplates/
            └── template.html
```
## Features

- **Express.js Backend**: Utilizes Express.js to handle HTTP requests and routing.
- **Docker Integration**: Easily build and run the application using Docker.
- **Dynamic Configuration Loading**: Watches for changes in the configuration file and reloads them dynamically.
- **HTML Rendering**: Renders HTML templates with dynamic content.

## Requirements

- Node.js (v20.5.1 or higher)
- Docker (if using the Docker container)

## Installation

Clone the repository:

```bash
git clone https://github.com/Juandi-M/WebUI_vaultsecretsDisplay.git
cd WebUI_vaultsecretsDisplay
```

Install dependencies:

```bash
npm install
```

Build the Docker image (optional):

```bash
docker-compose build
```

## Usage

To run the application locally:

```bash
npm start
```

To run the application using Docker:

```bash
docker-compose up
```

Visit `http://localhost:3001` in your browser to view the application.

Certainly! Below is a detailed explanation of the code structure and functionality, organized by key components. You can include this section in the README.md or any other documentation.

## Code Explanation

### `Dockerfile` and `docker-compose.yaml`

These files define the Docker configuration for the application. The `Dockerfile` specifies the base image, working directory, user, dependencies, and startup command. The `docker-compose.yaml` file sets up the service, including port mapping, volumes, and environment variables.

### `web/configs/appconfigs.json`

This JSON file contains various hardcoded values and configurations used within the application. It can be modified to change the behavior of the application.

### `web/js/app.js`

The main entry point for the Express.js application. It sets up the following:

- **Logging Middleware**: Logs each incoming request with a timestamp.
- **Example Routes**: Defines example routes to demonstrate dynamic configuration loading.
- **Server Initialization**: Starts the server on port 3001 with a delay to allow for configuration loading.

### `web/js/package.json`

Defines the metadata for the Node.js project, including the name, version, description, main file, start script, and dependencies.

### `web/js/routes/index.js`

Handles the routing logic for the application, including:

- **Test Route**: A simple test route that returns a static response.
- **Root Route**: Renders HTML based on the current configuration using the `htmlRenderer` utility.

### `web/js/utils/configLoader.js`

A utility module responsible for:

- **Loading Configuration**: Reads the `appconfigs.json` file and parses it into a JavaScript object.
- **Watching for Changes**: Sets up a watcher to reload the configuration if the file changes.
- **Error Handling**: Falls back to a default configuration if an error occurs while loading the file.

### `web/js/utils/htmlRenderer.js`

A utility module for rendering HTML templates:

- **Reading Templates**: Reads the HTML template file from the filesystem.
- **Generating Dynamic Content**: Maps the configuration values into HTML elements.
- **Replacing Placeholders**: Replaces placeholders in the template with actual content, including a warning message if using the default configuration.

### `web/js/webTemplates/template.html`

An HTML template file that defines the structure and styling for the web page. It includes placeholders for dynamic content, which are replaced by the `htmlRenderer` utility.

## Dependencies & packages:

--
### Node.js Dependencies

- **express**: A web application framework for Node.js, used to handle HTTP requests and routing. Version `^4.17.1`.
- **chokidar**: A file watcher, used to watch for changes in the configuration file and reload it dynamically. Version `^3.5.2`.
- **fs**: A built-in Node.js module for working with the file system, used to read files such as the configuration and HTML template.
- **http**: A built-in Node.js module for HTTP functionality, used implicitly by Express.js.
- **path**: A built-in Node.js module for working with file and directory paths, used in the HTML rendering utility.

### Docker Dependencies

- **Node.js Base Image**: The Dockerfile uses `node:20.5.1-alpine` as the base image, providing a minimal environment with Node.js installed.

### Development Environment

- **Docker**: Used to containerize the application, making it easy to build, ship, and run.
- **Node.js**: The runtime environment for executing JavaScript code on the server.

## Contributing

Contributions are welcome! Please read the [contributing guidelines](CONTRIBUTING.md) to get started.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
# Desiderati JS Libs

A collection of JavaScript/TypeScript libraries for Angular applications.

## Overview

JS-Libs is a monorepo containing reusable Angular libraries developed by Felipe Desiderati. These libraries provide
various functionalities to enhance Angular applications.

## Prerequisites and Repoflow.io Registration

1. Install Node and NPM. Ensure Node.js and `npm` are installed on your machine.
   If not, download and install them from [Node.js official website](https://nodejs.org/).

2. Configuring `npm` for the private repository. Execute this login command:

    ```bash
    npm login --registry https://api.repoflow.io/npm/desiderati/js-libs --auth-type legacy
    ```

3. Publishing artifacts. Navigate to your package directory in the terminal and execute:

    ```bash
    npm publish --registry https://api.repoflow.io/npm/desiderati/js-libs
    ```
    > This prepares npm to publish packages to your specified private repository.

## Libraries

### Atmosphere

An Angular service wrapper for the [atmosphere.js](https://github.com/Atmosphere/atmosphere-javascript) library,
providing WebSocket and long-polling communication capabilities for Angular applications.

#### Key Features

- WebSocket communication with automatic fallback to long-polling
- Reconnection handling
- Observable-based API for reactive programming
- Simple message sending interface

#### Installation

```bash
npm install @desiderati/atmosphere@1.0.0
```

#### Usage

```typescript
import {AtmosphereService} from '@desiderati/atmosphere';
import {Notification} from '@desiderati/atmosphere';

@Component({
    // ...
})
export class YourComponent {
    constructor(private atmosphereService: AtmosphereService) {
    }

    connect() {
        this.atmosphereService.connect('https://your-server.com/endpoint')
            .subscribe({
                next: (msg: string) => {
                    console.log('Received message:', msg);
                    // Handle the message
                },
                error: (err: any) => {
                    console.error('Connection error:', err);
                    // Handle the error
                }
            });
    }

    sendMessage() {
        const notification = new Notification('Your client (user) identification', 'Your message');
        this.atmosphereService.sendNotification(notification);
    }
}
```

For more details, see the [Atmosphere Library](./libs/atmosphere/README.md).

## Development

### Building All Libraries

To build all libraries in the monorepo:

```bash
ng build
```

### Building a Specific Library

To build a specific library (e.g., atmosphere):

```bash
ng build atmosphere
```

### Running Tests

To run tests for all libraries:

```bash
ng test
```

To run tests for a specific library:

```bash
ng test atmosphere
```

## Publishing

After building a library, you can publish it to npm:

```bash
cd dist/atmosphere
npm publish
```

## Author

Felipe Desiderati <felipedesiderati@springbloom.dev> (https://github.com/desiderati)

## [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.


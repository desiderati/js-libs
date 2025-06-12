# Atmosphere Service Library

An Angular service wrapper for the [atmosphere.js](https://github.com/Atmosphere/atmosphere-javascript) library,
providing WebSocket and long-polling communication capabilities for Angular applications.

## Overview

The Atmosphere service provides a simple way to establish real-time, bidirectional communication between your Angular
application and a server using WebSockets, with automatic fallback to long-polling when WebSockets are not available.

Key features:

- WebSocket communication with automatic fallback to long-polling
- Reconnection handling
- Observable-based API for reactive programming
- Simple message sending interface

## Installation

In the root of your Angular project, create or edit the `.npmrc` file:

```.npmrc
# Registry Default
registry=https://registry.npmjs.org/

# Private Repoflow Registry for @desiderati
@desiderati:registry=https://api.repoflow.io/npm/desiderati/js-libs/
```

```bash
npm install @desiderati/atmosphere@1.0.0
```

## Usage

### Import the Module

Add the AtmosphereService to your Angular module or component:

```typescript
import {AtmosphereService} from '@desiderati/atmosphere';

@Component({
    // ...
})
export class YourComponent {
    constructor(private atmosphereService: AtmosphereService) {
    }
}
```

### Establish a Connection

```typescript
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
```

### Send Notifications

```typescript
import {Notification} from '@desiderati/atmosphere';

const notification = new Notification('Your client (user) identification', 'Your message');
this.atmosphereService.sendNotification(notification);
```

## API Reference

### AtmosphereService

#### Methods

- **connect(url: string, customAtmosphereRequest?: CustomAtmosphereRequest): Observable<string>**

  Establishes a connection to the specified URL using WebSocket (with fallback to long-polling).

  Parameters:
    - `url`: The URL to connect to
    - `customAtmosphereRequest`: Optional custom configuration for the Atmosphere connection

  Returns:
    - An Observable that emits messages received from the server

- **sendNotification(notification: Notification): void**

  Sends a notification to the connected server.

  Parameters:
    - `notification`: The notification object to send

- **isInitialized(): boolean**

  Checks if the Atmosphere connection is initialized.

  Returns:
    - `true` if the connection is initialized, `false` otherwise

#### Connection Configuration

The service uses the following default configuration:

- Content Type: application/json
- Reconnect Interval: 5000 ms
- Max Reconnect Attempts: 7
- Primary Transport: WebSocket
- Fallback Transport: Long-polling
- Debug Level: info

### Types

#### Notification

A class representing a notification to be sent to the server.

```typescript
import {Notification} from '@desiderati/atmosphere';

// Create a notification with a payload.
const notification = new Notification('Your client (user) identification', 'Your message');
```

#### CustomAtmosphereRequest

An interface that extends the Atmosphere.js Request interface with additional options:

```typescript
interface CustomAtmosphereRequest extends AtmosphereRequest {
    logFunction?: ((msg: string) => void) | undefined;
}
```

- `logFunction`: Optional custom logging function for debug messages

## Development

This project was generated using [Angular CLI](https://github.com/angular/angular-cli) version 19.2.0.

### Building

To build the library, run:

```bash
ng build atmosphere
```

This command will compile your project, and the build artifacts will be placed in the `dist/` directory.

### Publishing the Library

Once the project is built, you can publish your library by following these steps:

1. Navigate to the `dist` directory:

   ```bash
   cd dist/atmosphere
   ```

2. Run the `npm publish` command to publish your library to the npm registry:

   ```bash
   npm publish
   ```

### Running unit tests

To execute unit tests with the [Karma](https://karma-runner.github.io) test runner, use the following command:

```bash
ng test
```

## Additional Resources

- [Atmosphere.js Documentation](https://github.com/Atmosphere/atmosphere-javascript)
- [Angular Documentation](https://angular.dev)
- [RxJS Documentation](https://rxjs.dev)

## Author

Felipe Desiderati <felipedesiderati@springbloom.dev> (https://github.com/desiderati)

## [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

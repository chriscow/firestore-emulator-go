# Firestore Emulator Go

Go code to start and stop the Firestore emulator for tests.

## Overview

This code provides utilities to programmatically start, stop, and interact with the Firebase Firestore emulator in Go testing environments. It handles all the boilerplate of:

- Starting the Firestore emulator with dynamic port allocation
- Automatically configuring environment variables
- Creating test clients that connect to the emulator
- Cleaning up resources when tests complete

## Requirements

- Go 1.13 or higher
- Google Cloud SDK (with `gcloud` CLI tool)
- Firestore emulator component (`gcloud components install cloud-firestore-emulator`)

## Installation

Just copy the file(s) to your project. 

## Usage

```go
package main

// In your TestMain function
func TestMain(m *testing.M) {
    // Start emulator
    if err := internal.StartEmulator(); err != nil {
        log.Fatalf("Failed to start emulator: %v", err)
    }
    
    // Stop emulator when tests finish
    defer internal.StopEmulator()
    
    // Run tests
    os.Exit(m.Run())
}

// In your test function
func TestMyFirestoreCode(t *testing.T) {
    ctx := context.Background()
    client, err := internal.NewTestFirestoreClient(ctx)
    if err != nil {
        t.Fatalf("Failed to create client: %v", err)
    }
    defer client.Close()
    
    // Now use the client to test your code
    // ...
}
```

## Features

- Dynamically allocates ports to avoid conflicts between test runs
- Parses emulator output to configure environment variables automatically
- Ensures proper cleanup of resources after tests finish
- Minimizes test setup boilerplate

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the LICENSE file for details.
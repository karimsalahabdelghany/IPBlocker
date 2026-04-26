 IP Blocker Service

A robust, high-performance IP blocking service designed to secure .NET applications. This project implements a clean architecture approach to identify, track, and block unauthorized IP addresses in real-time.

## Features
- **Custom Middleware**: Intercepts incoming requests to perform real-time access control.
- **Geolocation API Integration**: Utilizes a third-party service via `HttpClient` to map IP addresses to country codes for region-based blocking.
- **Background Worker Service**: Efficiently manages temporary blocks and automatically clears expired entries.
- **Thread-Safe Storage**: Uses `ConcurrentDictionary` for high-concurrency performance and memory safety.
- **Clean Architecture**: Decoupled design separating the filtering logic, background management, and data contracts.

## Architecture
- **Middleware Layer**: Handles request validation before they reach the controller.
- **Service Layer**: Manages the core logic of blocking and IP validation.
- **Background Worker**: Handles the cleanup of expired blocks.
- **DTOs**: Ensures data integrity for all blocking and validation operations.

## Technologies Used
- **Framework**: .NET (Core/8/9)
- **Concurrency**: `ConcurrentDictionary`, `Task`-based asynchronous patterns
- **Networking**: `HttpClient` (for Geo-IP services)
- **Logging**: Integrated standard .NET logging for auditing blocked attempts

## How it Works
1. When a request arrives, the **Middleware** captures the IP.
2. The middleware checks the **ConcurrentDictionary** for existing blocks.
3. If not found, it queries the **Geolocation API** (optional/configurable).
4. If the IP violates rules, it is added to the block list.
5. A **Background Worker** monitors this list and releases the block after the configured duration.

## Getting Started
1. Clone the repository.
2. Configure the `appsettings.json` with your Geo-IP API key.
3. Register the IP Blocker middleware in your `Program.cs` / `Startup.cs`.

# Redis and Redis Stack Installation Guide

Welcome to the Redis and Redis Stack Installation Guide! This README provides step-by-step instructions to install Redis (an open-source, in-memory data structure store) and Redis Stack (an enhanced version of Redis with additional modules like JSON, Search, and Time Series) on various operating systems. Whether you're setting up Redis for development or production, this guide has you covered.

## Table of Contents
1. [Overview](#overview)
2. [Prerequisites](#prerequisites)
3. [Installing Redis](#installing-redis)
   - [Linux (Ubuntu/Debian)](#linux-ubuntudebian)
   - [macOS](#macos)
   - [Windows](#windows)
4. [Installing Redis Stack](#installing-redis-stack)
   - [Using Docker](#using-docker)
   - [Linux (Ubuntu/Debian)](#linux-ubuntudebian-1)
   - [macOS](#macos-1)
   - [Windows](#windows-1)


---

## Overview

- **Redis**: A high-performance, in-memory key-value store used as a database, cache, and message broker.
- **Redis Stack**: Extends Redis with additional capabilities such as JSON support, full-text search, time series data, and more through integrated modules.

This guide covers installation methods for both Redis and Redis Stack across popular platforms.

---

## Prerequisites

Before you begin, ensure you have:
- A supported operating system (Linux, macOS, or Windows).
- Administrative or sudo privileges (for Linux/macOS).
- An internet connection to download packages.
- Optional: Docker installed (for containerized installation).

---

## Installing Redis

### Linux (Ubuntu/Debian)

1. **Update Package Index**:
   ```bash
   sudo apt-get update
2. **Install Redis:**:
   ```bash
   sudo apt-get install redis-server
3. **Start Redis Service:**:
   ```bash
   sudo systemctl start redis-server
   ```
4. **Enable Redis on Boot:**:
   ```bash
   sudo systemctl enable redis-server
   ```
### macOS
1. **Install Homebrew (if not already installed):**:
   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```
2. **Install Redis:**:
   ```bash
   brew install redis
   ```


3. **Start Redis**:

    Foreground: 
    ```bash
    redis-server 
    ```

    Background: 
    ```bash
    brew services start redis
    ```




##  Windows
Redis does not officially support Windows, but you can use Windows Subsystem for Linux (WSL):

1.**Install WSL:**

Open PowerShell as Administrator and run:

wsl --install
Install a Linux distribution (e.g., Ubuntu) from the Microsoft Store.
Follow Linux Instructions:
Open your WSL terminal and follow the steps.
# Installing Redis Stack
Redis Stack bundles Redis with additional modules. Below are installation methods:

## Using Docker
1.**Install Docker:**

- Download and install Docker from [docker.com](https://hub.docker.com/_/redis/)

2.**Pull Redis Stack Image:**
```bash
docker pull redis/redis-stack:latest
```
3.**Run Redis Stack:**
```bash
docker run -d --name redis-stack -p 6379:6379 -p 8001:8001 redis/redis-stack:latest
```
- Port 6379: Redis server.
- Port 8001: RedisInsight (GUI tool).

## Linux (Ubuntu/Debian)


1. **Add Redis Repository:**
```bash
sudo apt-get install -y lsb-release curl gpg
curl -fsSL https://packages.redis.io/gpg | sudo gpg --dearmor -o /usr/share/keyrings/redis-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/redis-archive-keyring.gpg] https://packages.redis.io/deb $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/redis.list
```
2. **Update and Install Redis Stack:**
```bash
sudo apt-get update
sudo apt-get install redis-stack-server
```
3. **Start Redis Stack:**
```bash
sudo systemctl start redis-stack-server
sudo systemctl enable redis-stack-server
```
## macOS
1. **Install Redis Stack with Homebrew:**
```bash
brew install redis-stack
```
3. **Start Redis Stack**:

    Foreground: 
    ```bash
    redis-stack-server 
    ```

    Background: 
    ```bash
    brew services start redis-stack
    ```

## Windows
- To install Redis Stack on Windows, you will need to have Docker installed. When Docker is up and running, open Windows PowerShell and follow the instructions described in [Run Redis Stack on Docker](#linux-ubuntudebian-1). Then, use Docker to connect with redis-cli as explained in that topic.



# Closing Note

Congratulations on setting up Redis and Redis Stack! Whether you're caching data, building real-time applications, or exploring advanced features like full-text search and time series, you're now equipped to leverage the power of Redis. If you run into any issues or have suggestions to improve this guide, feel free to open an issue or submit a pull request. Happy coding, and may your Redis adventures be fast and efficient!
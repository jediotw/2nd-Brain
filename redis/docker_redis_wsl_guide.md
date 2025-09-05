# 🚀 Running Docker & Redis Stack inside WSL with systemd

This guide explains how to run **Docker natively inside WSL (Ubuntu)**
and use **Redis Stack** without Docker Desktop.

------------------------------------------------------------------------

## 1️⃣ Update system packages

``` bash
sudo apt update
```

------------------------------------------------------------------------

## 2️⃣ Verify Docker engine

``` bash
docker info
```

-   If it shows engine info → Docker is active.\
-   If not, install it (next step).

------------------------------------------------------------------------

## 3️⃣ Install Docker & Compose

``` bash
sudo apt install -y docker.io docker-compose
```

------------------------------------------------------------------------

## 4️⃣ Enable Docker with systemd

Since `systemd=true` is set in `/etc/wsl.conf`:

``` bash
sudo systemctl enable --now docker
systemctl status docker
systemctl --failed
```

------------------------------------------------------------------------

## 5️⃣ (Optional) Run Docker without `sudo`

``` bash
sudo usermod -aG docker $USER
```

➡️ Restart WSL to apply changes:

``` powershell
wsl --shutdown
```

------------------------------------------------------------------------

## 6️⃣ Manage Containers

-   Stop Redis Stack:

    ``` bash
    docker stop redis-stack
    ```

-   Remove container:

    ``` bash
    docker rm redis-stack
    ```

------------------------------------------------------------------------

## 7️⃣ Manage systemd services

-   List running services:

    ``` bash
    systemctl list-units --type=service
    ```

-   Disable & mask a service:

    ``` bash
    sudo systemctl disable <service-name>
    sudo systemctl mask <service-name>
    ```

-   Remove a service completely:

    ``` bash
    sudo apt remove --purge <service-name>* -y
    sudo apt autoremove -y
    ```

    -   `--purge` → deletes config files\
    -   `autoremove` → cleans unused dependencies

-   Clear ghost services:

    ``` bash
    sudo systemctl daemon-reload
    sudo systemctl reset-failed
    ```

-   Check logs of a service:

    ``` bash
    journalctl -u <service-name>
    ```

------------------------------------------------------------------------

## 8️⃣ Test Docker installation

``` bash
docker --version
sudo docker run hello-world
```

------------------------------------------------------------------------

## 9️⃣ Install & Run Redis Stack

Pull the image:

``` bash
sudo docker pull redis/redis-stack:latest
```

Run container:

``` bash
sudo docker run -d --name redis-stack -p 6379:6379 -p 8001:8001 redis/redis-stack:latest
```

------------------------------------------------------------------------

## 🔟 Use Redis

-   Redis CLI inside container:

    ``` bash
    docker exec -it redis-stack redis-cli
    ```

-   Redis Insight (GUI):\
    👉 http://localhost:8001

------------------------------------------------------------------------

## 1️⃣1️⃣ Shutdown WSL cleanly

From PowerShell:

``` powershell
wsl --shutdown
```

------------------------------------------------------------------------

✅ With this setup, Docker runs **natively inside WSL**, and Redis Stack
is always available at `127.0.0.1:6379` for apps (e.g., Node.js).

# Factorio Docker Image for Private Game Hosting

Utilises [this](https://hub.docker.com/r/dtandersen/factorio/) docker image, which is suitable to run on a Nano
Linode instance.

## Setting Up

### 1. Install Docker CE

[Instructions](https://docs.docker.com/install/linux/docker-ce/debian/#install-using-the-repository) for your
choice of distribution.

### 2. Install Docker Compose

```bash
$ sudo curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
$ sudo chmod +x /usr/local/bin/docker-compose
```

### 2. Setup the Factorio Container User

```bash
sudo mkdir /opt/factorio
sudo chown 845:845 /opt/factorio
```

### 3. Setup Factorio Server

Git Checkout this repo to /opt/factorio:

```bash
git checkout repo path /opt/factorio
```

Edit [docker-compose](./docker-compose.yml) and specify the stable factorio image. At time of writing this is `0.16.51`:

```yml
version: '2'
services:
  factorio:
    image: dtandersen/factorio:0.16.51 <---- set the version here
    ports:
     - "34197:34197/udp"
    volumes:
     - ./factorio:/factorio
    restart: always
```

### 4. Start Factorio Server

Copy the game save to `/opt/factorio/factorio/saves`. Make sure it is the only file in the folder.

```bash
cd /opt/factorio
docker-compose start

```

To view factorio server logs:

```
docker-compose log -f
```


 

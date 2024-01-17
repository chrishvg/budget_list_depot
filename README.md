# Budget Meterials

## Install git sftware

[Git Windows instalation](https://git-scm.com/download/win/)

### Install docker software
[Docker Windows instalation](https://docs.docker.com/desktop/install/windows-install/)

## Follow the commands

### Open terminal and execute the command
```
git clone https://github.com/chrishkv/budget_list_depot.git
```

### Enter to the folder "budget_list_depot" using the command
```
cd budget_list_depot
```

### Create the Docker image with the command
```
docker build -t "budge-depot" .
```

### Execute the software with the command
```
docker compose up -d --build
```

### Now you can see the software in the url
[http://localhost](http://localhost)
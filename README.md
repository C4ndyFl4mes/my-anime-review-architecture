# My Anime Review Architecture

This repo will be the one to compose the Docker environment with a PostgreSQL DBMS, WebAPI (ASP.NET), React frontend, and Caddy.

## Local Deployment Guide (Windows)
Prerequisite for windows: Docker Desktop.

1. `git clone https://github.com/C4ndyFl4mes/my-anime-review-architecture.git`
2. `git clone https://github.com/C4ndyFl4mes/my-anime-review-application.git`
3. In the my-anime-review-application, do the following:
    1. Comment out StrictMode in src/main.tsx (certain features can't handle instant double calls)
    2. Change the relative paths of the baseURL in each service class under src/services/ to begin with https://localhost:443/. Example: https://localhost:443/api/user (I was lazy of not using envs here.)
    3. To run: `npm run dev` (`npm run preview` doesn't work because of me not setting the cors origin for that.)
4. In the my-anime-review-architecture, do the following:
    1. `mkdir .secrets`
    2. `cd .secrets`
    3. `copy absolute-path/my-anime-review-architecture/.example.secrets/* .`
    4. Change the single values of each file to preferred values and correct format to pass validation. The application will crash if validation fails.
    5. To run: `docker compose up`
5. Enter the website: http://localhost:5173/

## VPS Deployment Guide (Linux Ubuntu)
1. `sudo apt update`
2. `sudo apt upgrade -y`
3. Make sure that these exists: `sudo apt install -y ca-certificates curl gnupg git ufw`
4. `sudo install -m 0755 -d /etc/apt/keyrings`
5. `curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg`
6. `sudo chmod a+r /etc/apt/keyrings/docker.gpg`
7. `echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(. /etc/os-release && echo $VERSION_CODENAME) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null`
8. `sudo apt update`
9. `sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin`
10. `sudo usermod -aG docker $USER`
11. You may need to log out and back in for your user to get access to the Docker group.
12. Make sure the firewall have this (check `sudo ufw status`):
    1. `sudo ufw allow OpenSSH`
    2. `sudo ufw allow 80/tcp`
    3. `sudo ufw allow 443/tcp`
    4. `sudo ufw enable`
13. Make a fork of this repo https://github.com/C4ndyFl4mes/my-anime-review-architecture
14. On your own computer do the following:
    1. `git clone https://github.com/yourname/my-anime-review-architecture.git`
    2. `cd my-anime-review-architecture`
    3. On the first line, change the domain to your VPS' domain.
    4. Make a push to your fork.
15. Back to the VPS.
16. `git clone https://github.com/yourname/my-anime-review-architecture.git`
17. `cd my-anime-review-architecture`
18. `mkdir .secrets`
19. `cd .secrets`
20. `cp absolute-path/my-anime-review-architecture/.example.secrets/* absolute-path/my-anime-review-architecture/.secrets/`
21. Change the single values of each file to preferred values and correct format to pass validation. In .secrets/ `nano admin_email.txt`
22. Start:
    1. `docker compose pull`
    2. `docker compose up`
23. It should be running enter the website or test it by `curl -I https://example.com`
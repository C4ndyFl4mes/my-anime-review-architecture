# My Anime Review Architecture

This repo will be the one to compose the Docker environment with a PostgreSQL DBMS, WebAPI (ASP.NET), React frontend, and Caddy.

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
13. `git clone https://github.com/C4ndyFl4mes/my-anime-review-architecture`
14. `cd my-anime-review-architecture`
15. `mkdir .secrets`
16. `cd .secrets`
17. `cp absolute-path/my-anime-review-architecture/.example.secrets/* absolute-path/my-anime-review-architecture/.secrets/`
18. Change the single values of each file to preferred values and correct format to pass validation. In .secrets/ `nano admin_email.txt`
19. In Caddyfile, you may need to change the domain name to your VPS' domain name. In root directory: `nano Caddyfile`
20. Start:
    1. `docker compose pull`
    2. `docker compose up`
21. It should be running enter the website or test it by `curl -I https://example.com`
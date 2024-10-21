# Overleaf Documentation

1. Ssh into machine with overleaf key
2. Make sure instance is put up correctly

   ```
   1. cd /var/logcat 
   2. user-data.log
   ```

   Make sure last line of user-data is server is running. If not then go to terraform-aws-overleaf -> user-data.sh -> manually install packages that failed to install.
3. Check for ebs volume attachment

   ```
   1. lsblk
   2. EBS should be mounted on /data
   ```
4. Go to overleaf directory

   ```
   1. cd /data/home/ubuntu/overleaf-toolkit
   2. bin/doctor
   ```

   Make sure everything is all good
5. Skip steps 6-9 since it is already setup (Meant for initial setup)
6. Setup pass for server pro credential security
   prerequsite:

   ```
   1. sudo apt install pass
   2. sudo apt-get install golang-docker-credential-helpers

   ```

   **Should already be installed**
7. Setup gpg key

   ```
   1. gpg --full-generate-key
   ```

   Follow prompts to setup key
8. Init keys

   ```
   pass init quay.io
   ```
9. Login to server pro with username and password (will be stored in pass)

   **Contact baig@kairospower.com for username and password.**
10. Before starting server type command below to be able to download Tex-live resources

    ```
    pass docker-credential-helpers/cXVheS5pbw==/sharelatex+kairospower
    ```

    **Contact baig@kairospower.com for password**
11. Run command below to start server

    ```
    bin/up -d
    ```
12. Server should be up and running
13. Make sure to be on vpn
14. Go to [Overleaf](overleaf.kairospower.com)
15. Sign in
16. If account is required **contact baig@kairospower.com**


### Troubleshooting

If you see issues below:

1. Error response from daemon: unauthorized: access to the requested resource is not authorized, run command below

   ```
   pass docker-credential-helpers/cXVheS5pbw==/sharelatex+kairospower
   ```
2. Error response from daemon: driver failed programming external connectivity on endpoint sharelatex (4aa1b720e3c3c4375111bbe703f982332481791fff7edd836eb9dcca66c85df6): failed to bind port 127.0.0.1:80/tcp: Error starting userland proxy: listen tcp4 127.0.0.1:80: bind: address already in use

   ```
   1. sudo lsof -i :80
   2. sudo systemctl stop nginx
   3. bin/up -d
   ```
3. permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get "http://%2Fvar%2Frun%2Fdocker.sock/v1.47/containers/json?all=1&filters=%7B%22label%22%3A%7B%22com.docker.compose.config-hash%22%3Atrue%2C%22com.docker.compose.project%3Doverleaf%22%3Atrue%7D%7D": dial unix /var/run/docker.sock: connect: permission denied

   ```
   Type command below and ensure docker is within groups
   1. groups $(whoami)
   ```

   If not do these commands:

   ```
   1. sudo usermod -aG docker $USER
   2. sudo usermod -aG docker $(whoami)
   ```

   Then log out and log back in. Docker should be up and running. Type command below to test

   ```
   docker ps
   ```


### Contact

If any issues arise contact individual below

Name: Aiman Baig

Team: ModSim

Email: baig@kairospower.com

Slack: Aiman Baig

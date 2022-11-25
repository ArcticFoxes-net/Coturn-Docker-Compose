# Coturn-Docker-Compose
Coturn Docker-Compose for Matrix Synapse

1. Start the ACME daemon: `docker-compose up -d acme`.
2. Register an account ZeroSSL: `docker exec acme --register-account -m email@domain.tld`.
3. Generate the certificate: `docker exec acme --issue -d turn.yourdomain.tld  --standalone`.
4. Copy the certificates to the correct location: `docker  exec  acme --install-cert -d turn.yourdomain.tld --fullchain-file /ssl/fullchain.pem --key-file /ssl/privkey.pem`.
5. Set `65534:65534` to own the certificates: `chown -R 65534:65534 ./ssl`
6. Edit `coturn/turnserver.conf` approprieately. At minimum, you should change `realm` to your TURN server's hostname and set your own `static-auth-secret`.
7. Run `docker-compose up` and make sure nothing errors out. You can use `docker-compose up -d` to start it in the background if you want.
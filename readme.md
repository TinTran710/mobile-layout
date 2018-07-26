# Mkcert installation

### Golang
Golang1.10+ is needed when we build mkcert
- Download the Go language binary archive file:
```
wget https://dl.google.com/go/go1.10.linux-amd64.tar.gz
```
- Extract the file:
```
sudo tar -xvf go1.10.linux-amd64.tar.gz
```
- Move the go folder the specified destination:
```
sudo mv go /usr/local
```
- Setup Go enviroment: put this in `~/.profile`:
```
export GOROOT=/usr/local/go
export GOPATH=$HOME/Projects/ADMFactory/Golang
export PATH=$GOPATH/bin:$GOROOT/bin:$PATH
```

### Certutil
Certutil is a simple command-line utility that can create/modify certificate and their key databases.
```
sudo apt install libnss3-tools
```

### Mkcert
```
wget https://github.com/FiloSottile/mkcert/archive/v1.0.0.tar.gz
sudo tar -xvf v1.0.0.tar.gz
cd mkcert-1.0.0/
make
```
- Copy mkcert binary from installation folder to `/usr/bin` folder to use it server-wide:
```
cd mkcert-1.0.0/bin/
cp mkcert /usr/bin/
```

### Generate local CA
```
mkcert -install
```

### Generate local development certificate
```
mkcert localhost
```

### Move the created certificates to /etc/ssl
- Mime was initially created at `/root` so I use the following commands:
```
sudo cp /root/localhost.pem /etc/ssl/certs/
sudo cp /root/localhost-key.pem /etc/ssl/private/
```

### Edit the default SSL file at `/etc/apache2/sites-available/default-ssl.conf` with our locally generated SSL certificate and key details as below
```
SSLCertificateFile /etc/ssl/certs/localhost.pem
SSLCertificateKeyFile /etc/ssl/private/localhost-key.pem
```

### Restart Apache2
```
sudo service apache2 restart
```

### Hit `https://localhost`

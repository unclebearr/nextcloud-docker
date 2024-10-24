#### Generate the private key
sudo openssl genrsa -out nc.local.example.ca.key 2048

#### Generate the certificate signing request (CSR)
sudo openssl req -new -key nc.local.example.ca.key -out nc.local.example.ca.csr

#### Generate a certificate valid for 10 years
sudo openssl x509 -req -days 3650 -in nc.local.example.ca.csr -signkey nc.local.example.ca.key -out nc.local.example.ca.crt
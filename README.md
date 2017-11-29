# easy-rsa-vagrant

This vagrant machine completly installs easy-rsa and creates all certificates

1. clone this project
2. copy ansible/vars.yml.example to ansible/vars.yml and customize to your needs
3. vagrant up

The created certificate can be found inside ca/easy-rsa/keys.

Keep this CA in a secure place. Creation of further client certificates or revocation of certificates will be done by updating ansible/vars.yml and running "vagrant provision".

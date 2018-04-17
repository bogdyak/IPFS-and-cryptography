### instal GNU Privacy Guard
```
sudo apt-get install gnupg
```

### Generate key
```
gpg --gen-key
```
Generate key on second computer

### Export key on the second machine
```
gpg --export --armor exmaple@email.com > pubkey.asc
```
put pubkey.asc in the working directory on the first machine

### Import key on the first machine
```
gpg --import pubkey.asc

// Make sure it imported correctly

gpg --list-keys

// you should see 2 records or more
```

### Install ipfs from https://ipfs.io/docs/install/
```
ipfs init

ipfs daemon
```
Repeat this at the second machine


### Encrypt file and add it to IPFS
```
// encrypting file with public key of recipient
gpg --encrypt --recipient "Full Name of recipient" exmaple_file.pdf

// make sure that file example_file.pdf.pgp appeard at your working dirrectory

// adding file to IPFS
ipfs add example_file.pdf.pgp

// you must see output like 
added QmUAPHhxcTcQKiAFSRjcUbpge9UDyiL5NVyrKFJaXgATKv example_file.pdf.gpg

```

### Dowload and decrypt file from ipfs on second computer
```
ipfs get QmUAPHhxcTcQKiAFSRjcUbpge9UDyiL5NVyrKFJaXgATKv

// make sure file QmUAPHhxcTcQKiAFSRjcUbpge9UDyiL5NVyrKFJaXgATKv appeared in working directory

gpg --decrypt QmUAPHhxcTcQKiAFSRjcUbpge9UDyiL5NVyrKFJaXgATKv > example_file.pdf

// you will see output like
You need a passphrase to unlock the secret key for
user: "Bogdan (IPFS key) <sizov.workingbox@gmail.com>"
2048-bit RSA key, ID 97F5155F, created 2018-04-17 (main key ID 06E5DB59)

Enter passphrase:
// enter password which you used when creating key file

```
Well done, you have encrypted, uploaded, downloaded and decrypted file with IPFS and Cryptography
# SSH Remote Port Forwarding

Melakukan Port Forwarding dari device jaringan lokal agar dapat bisa diakses dari server Remote

## Topologi

![App Topologi](https://media.geeksforgeeks.org/wp-content/uploads/20191031165048/ssh_remote_port3.jpg)


### Penjelasan Topologi

Server Local `example.com` melakukan Remote Port Forwarding pada port local `80` menuju server dengan port `9090`.  
Sehingga `example.com:80` dapat diakses dengan `server:9090`.






## Requierement

Pertama-tama ubah opsi  
```bash 
GatewayPorts no
``` 
pada `sshd_config` menjadi `GatewayPorts clientspecified`
```bash 
GatewayPorts clientspecified
```  
Kemudian ``reload`` service `ssh`.
```bash
sudo service ssh reload
```
    
## Penggunaan

Bash syntax

```bash
ssh -g -R [remote-addr]:[remote-port]:[local-addr]:[local-port] -N [user]@[server.host]
```
Contoh berdasarkan topologi diatas. Syntax berikut dieksekusi dari sisi Local Network `example.com`  
```bash
ssh -g -R 0.0.0.0:9090:localhost:80 -N root@server
```

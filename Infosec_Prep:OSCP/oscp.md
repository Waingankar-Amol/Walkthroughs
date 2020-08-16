# Infosec Prep: OSCP
#### Once we start OS in VM we get the IP address by DHCP.
![1](OSCP/1.png)
#### Now we start Recon by scanning with nmap 
![2](OSCP/2.png)
`nmap -A 192.168.28.129`
 ## Information Gathering: 
 ##### Nmap scan output says that, `22/tcp ssh` is opened and `80/tcp http` is opened. In `robots.txt`, secret.txt is disallowd entry
![3](OSCP/3.png)
##### We opened `http://192.168.28.129/secret.txt/`
On that page we get encrypted msg. so we try to decrypt it with **base64**
![4](OSCP/4.png)

Here we get that openssh private key.
so now try to login with ssh + ssh key.
given key save with a any file name.
![5](OSCP/5.png)

`ssh -i key.txt oscp@192.168.28.129`

![6](OSCP/7.png)


`/bin/bash -p`

this will give root previledges. so **flag** is here

![7](OSCP/8.png)

Now try to gain **root** password
![8](OSCP/9.png)

`openssl passwd admin@123`
 
below generated output copy and paste to `/etc/passwd` file

![9](OSCP/10.png)

copied string replace with `x` 

![10](OSCP/11.png)

[Click here for more Privilege Escalations about this box](https://medium.com/@falconspy/infosec-prep-oscp-vulnhubwalkthrough-a09519236025)
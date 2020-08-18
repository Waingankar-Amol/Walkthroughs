# Traceback
## Recon:
`sudo nmap -T4 -O -A -sV -p- -sS -Pn -n -vvv -oA scan1 10.10.10.181`
![nmap](1.png)

According to Nmap scan results, Port no `22 tcp/ssh` , `80 tcp/http`

## Enumeration
Open 80 port in browser
![](2.png)
 *Some of the best web shells that you might need ;)*

 we google the above hint and get the github link. https://github.com/TheBinitGhimire/Web-Shells
 
 github link displays a php web shells as follow
 
 ![](3.png)
 
 Collect all these names and try to directory search with it. Finally get `smevk.php`
 ![](4.png)
 
 using console we moved to the `/home/webadmin/.ssh/`
 and remove the `authorized_key` file

 **on kali:**
 `ssh-keygen` > generated ssh keys.
`mv id.rsa.pub authorized_keys `
`cp authorized_keys ../Downloads`

we done password less authentication between webadmin user and kali user by uploading `authorized_keys`.

![](5.png)
ssh authentication successfull..

### Previledge Escalation
`sudo -l`
![](6.png)
logged in user have the permission to `/home/sysadmin/luvit`

we use a *lua binary* for previledge escalation.
![](7.png)
![](8.png)
Here we get the user flag

`python3 -m http.server` - setup the webserver on kali machine to wget the file
![](9.png)

![](10.png)
Run the linpeas.sh script

here we got some interesting..!!!
![](11.png)
![](12.png)
![](13.png)
![](14.png)
flag is here..!!
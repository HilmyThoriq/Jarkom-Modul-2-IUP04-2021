# IUP 04
Salsabila Irbah 05111942000007 <br />
Muh Hilmy Thoriq YR 05111942000012 <br />
Nadhif Bhagawanta Hadiprayitno 05111942000029 <br />

# Problem 1
**EniesLobby will be used as DNS Master, Water7 will be used as DNS Slave, and Skypie will be used as Web Server. There are 2 clients, namely Loguetown and Alabasta. All nodes are connected to the Foosha router, so they can access the internet**

First we need to make topologies like this
![1 1](https://user-images.githubusercontent.com/81411468/139196460-379995f5-1166-4b95-b23e-3f7f65407154.PNG)

Then we can run command `iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.210.0.0/16` in foosha console, and run command `echo nameserver 192.168.122.1 > /etc/resolv.conf` in other nodes so we can connect to internet

**Difficulties:**
- No difficulties

# Problem 2
**Luffy wants to contact Franky who is in EniesLobby with denden mushi. You are asked by Luffy to create the main website by accessing `franky.iup04.com` with the alias `www.franky.iup04.com` in the kaizoku folder.**

first we need to run `apt-get update` and `apt-get install bind9 -y` in enieslobby console and edit `/etc/bind/named.conf.local` file like this<br>
![2 1](https://user-images.githubusercontent.com/81411468/139197209-f19cc042-41e1-4fa6-a210-513ba42bf72c.PNG)

next we need to edit `/etc/bind/kaizoku/franky.iup04.com` like this<br>
![2 2](https://user-images.githubusercontent.com/81411468/139197545-5ae33fc9-0368-47bb-9a75-3a0b40447862.PNG)

so when we ping `franky.iup04.com` and `www.franky.iup04.com` to check if its direct to skypie ip
![2 3](https://user-images.githubusercontent.com/81411468/139197807-f4246148-9756-459f-b7c5-3de27323f445.PNG)

**Difficulties:**
- No difficulties

# Problem 3
**After that create a subdomain `super.franky.iup04.com` with the alias `www.super.franky.iup04.com` whose DNS is set at EniesLobby and points to Skypie(3). Also create a reverse domain for the main domain**

first we need to edit `/etc/bind/kaizoku/franky.iup04.com` like this
![3 1](https://user-images.githubusercontent.com/81411468/139198117-1f61348f-ec07-4b29-b87d-988b64c3cb35.PNG)

so when we ping with `super.franky.iup04.com` and `www.super.franky.iup04.com` it will direct to skypie ip like this
![3 2](https://user-images.githubusercontent.com/81411468/139198283-cb8e6035-4cf5-4c91-928f-39c8a9ddcc48.PNG)

**Difficulties:**
- wrong approach at first time

# Problem 4
**Also create a reverse domain for the main domain**

First we need to edit `/etc/bind/named.conf.local` like this </br>
![4 1](https://user-images.githubusercontent.com/81411468/139198576-3be1cfcf-1ecc-494a-b74d-6dcbab8b6682.PNG)

then we edit `/etc/bind/kaizoku/2.210.192.in-addr.arpa` files </br>
![4 2](https://user-images.githubusercontent.com/81411468/139198904-0fcce820-3e1e-4db7-8d45-bbf6529085e0.PNG)

so when we check the reverse of our ip `192.210.2.2` it will direct to `franky.iup04.com` </br>
![4 3](https://user-images.githubusercontent.com/81411468/139199022-49dfed10-e6b1-44b2-a5af-d6be5188264d.PNG)

**Difficulties:**
- No difficulties

# Problem 5
**In order to still be able to contact Franky if the EniesLobby server is damaged, then make Water7 the DNS Slave for the main domain**

**enieslobby**
first we need to edit `/etc/bind/named.conf.local` files </br>
![5 1](https://user-images.githubusercontent.com/81411468/139199600-f72b812d-730b-4fca-9e42-4b42f63d0c01.PNG)

**water7**
run `apt-get update` and `apt-get install bind9 -y` then edit `/etc/bind/named.conf.local` file </br>
![5 2](https://user-images.githubusercontent.com/81411468/139199629-f76ba8a5-0805-4198-9dfe-3fdffe9c959e.PNG)

to check if it works, we need to run `service bind9 stop` then ping `franky.iup04.com` </br>
![5 3](https://user-images.githubusercontent.com/81411468/139199701-4d0aae08-9b99-4de2-b58d-a17dc6f106ec.PNG)

**Difficulties:**
- No difficulties

# Problem 6
**After that there is a subdomain `mecha.franky.yyy.com` with the alias `www.mecha.franky.yyy.com` which was delegated from EniesLobby to Water7 with the IP going to Skypie in the sunnygo folder**

**enieslobby**
edit `/etc/bind/kaizoku/franky.iup04.com` file like this </br>
![6 1](https://user-images.githubusercontent.com/81411468/139200473-77330c6d-6b82-41ce-a4aa-0053ad63efcc.PNG)

edit `/etc/bind/named.conf.options` file like this </br>
![6 2](https://user-images.githubusercontent.com/81411468/139200477-ae764add-626d-4d4e-8b57-53441c438388.PNG)

**water7**
edit `/etc/bind/named.conf.options` file like this </br>
![6 2](https://user-images.githubusercontent.com/81411468/139200491-73f40170-027c-44a4-afbe-bd8b79d249b0.PNG)

edit `/etc/bind/named.conf.local` file like this </br>
![6 3](https://user-images.githubusercontent.com/81411468/139200503-6cb6ad39-0e5d-4b7e-b38c-5e3f15bcf236.PNG)

edit `/etc/bind/sunnygo/mecha.franky.iup04.com` like this </br>
![6 4](https://user-images.githubusercontent.com/81411468/139200517-4207e257-48f1-40da-896c-54276feb1667.PNG)

test ping should be like this </br>
![6 5](https://user-images.githubusercontent.com/81411468/139200553-39b02a7b-25d9-467d-8fbd-2fa84978b2c9.PNG)

**Difficulties:**
- No difficulties

# Problem 7
**To facilitate communication between Luffy and his colleagues, a subdomain was created through Water7 with the name `general.mecha.franky.iup04.com` with the alias `www.general.mecha.franky.iup04.com` which points to Skypie**

**water7**
edit `/etc/bind/sunnygo/mecha.franky.iup04.com` </br>
![7 1](https://user-images.githubusercontent.com/81411468/139201022-fd364aad-a12a-4ebf-a17b-e64a22b79162.PNG)

test ping should be like this </br>
![7 2](https://user-images.githubusercontent.com/81411468/139201041-6289b268-4ece-49f9-b835-c465d9233ba1.PNG)

**Difficulties:**
- wrong approach at the first time

# Problem 8
**After configuring the server, then the Webserver configuration is done. First with the webserver `www.franky.iup04.com`. First, luffy needs a webserver with DocumentRoot on `/var/www/franky.iup04.com.`**

**skypie**

install `apachew`, `wget`, `php`, `unzip`, `libapache2-mod-php7.0`</br>

download all files required with `wget` command and edit `/etc/apache2/sites-available/franky.iup04.com.conf`</br>
![8 1](https://user-images.githubusercontent.com/81411468/139202809-c858331c-fb1b-4b36-8cac-c39a2fdf4178.PNG)

make directory `/var/www/franky.iup04.com` and extract `franky` the required files in here </br>
![8 2](https://user-images.githubusercontent.com/81411468/139202779-e98a09e2-47cc-4afa-acf0-156a27be0eaf.PNG)

**Difficulties:**
- Wrong `wget` link so can't unzip, must using raw data link

# Problem 9
**After that, Luffy also needs that the url `www.franky.iup04.com/index.php/home` can be `www.franky.iup04.com/home.`**

run `a2enmod rewrite` and `service apache2 restart` </br>
Edit file `/var/www/franky.iup04.com/.htaccess` like this </br>
![9 1](https://user-images.githubusercontent.com/81411468/139203696-4aaa0f18-40a4-40a4-be4e-a28afe493eb0.PNG)

Edit file `/etc/apache2/sites-available/franky.iup04.com.conf` like this </br>
![9 2](https://user-images.githubusercontent.com/81411468/139203710-3676b058-8b48-4fd8-ad86-acbba042f527.PNG)

**Difficulties:**
- No difficulties

# Problem 10
**After that, on the subdomain `www.super.franky.iup04.com`, Luffy needs an asset store that has DocumentRoot on `/var/www/super.franky.iup04.com`**

Edit `/etc/apache2/sites-available/super.franky.iup04.com.conf` like this </br>
![10 1](https://user-images.githubusercontent.com/81411468/139204253-163e79dc-0320-4cba-af81-f9e66ee72671.PNG)

Make directory `/var/www/super.franky.iup04.com` and put the downloaded files in there </br>

**Difficulties:**
- No difficulties

# Problem 11
**However, in the /public folder, Luffy wants to only be able to do directory listings**

Edit `/etc/apache2/sites-available/super.franky.iup04.com.conf` like this </br>
![11 1](https://user-images.githubusercontent.com/81411468/139204613-b5036a8a-2edc-4bda-b38a-0e1298117534.PNG)

**Difficulties:**
- No difficulties

# Problem 12
**Not only that, Luffy also prepared an error file 404.html in the /error folder to replace the error code in apache**

Edit `/etc/apache2/sites-available/super.franky.iup04.com.conf` like this
![12 1](https://user-images.githubusercontent.com/81411468/139204629-62e9e3a8-ff4e-45b4-a193-e8bf2b4966bf.PNG)

**Difficulties:**
- No difficulties

# Problem 13
**Luffy also asked Nami to make a virtual host configuration. This virtual host aims to be able to access the asset file `www.super.franky.iup04.com/public/js` to `www.super.franky.iup04.com/js`.**

Edit `/etc/apache2/sites-available/super.franky.iup04.com.conf` </br>
![13 1](https://user-images.githubusercontent.com/81411468/139204881-d6f717e9-4240-49ea-87ef-a81d0de2848e.PNG)

**Difficulties:**
- No difficulties

# Problem 14
**And Luffy asked for the web `www.general.mecha.franky.yyy.com` it can only be accessed with port 15000 and port 15500**

Edit `/etc/apache2/sites-available/general.mecha.franky.iup04.com.conf` file like this </br>
![14 1](https://user-images.githubusercontent.com/81411468/139205857-7cc84cd2-7b41-48ac-a3ed-283d6b5d71f7.PNG)

Edit `/e![14 2](https://user-images.githubusercontent.com/81411468/139205867-96f768d7-27e8-45b8-bab5-6a78609940c3.PNG)
tc/apache2/ports.conf` file like this </br>

make directory `/var/www/general.mecha.franky.iup04.com` and put the downloaded file in there </br>
![14 3](https://user-images.githubusercontent.com/81411468/139205873-5103b1d9-ba74-4f5a-b186-c5819c497c0b.PNG)

**Difficulties:**
- No difficulties

# Problem 15
**with authentication `username luffy` and `password onepiece` and file at `/var/www/general.mecha.franky.iup04.com`**

Run `htpasswd -c /etc/apache2/.htpasswd luffy` </br>

Edit `/etc/apache2/sites-available/general.mecha.franky.iup04.com.conf` like this </br> 
![15 1](https://user-images.githubusercontent.com/81411468/139206538-0a279540-646d-486c-a594-2dce0dcf1c7b.PNG)

Edit `/var/www/general.mecha.franky.iup04.com/.htaccess` like this </br>
![15 2](https://user-images.githubusercontent.com/81411468/139206565-9305ccd1-ca37-4f2a-9376-4a4c56fb2234.PNG)

**Difficulties:**
- Can't open with correct password

# Problem 16
**And every time you access the Skypie IP it will be automatically redirected to `www.franky.iup04.com`**

Edit `/var/www/html/.htaccess` like this </br>
![16 1](https://user-images.githubusercontent.com/81411468/139207007-03a4f0d7-c80a-4cb1-90a0-485481b28730.PNG)

Edit `/etc/apache2/sites-available/000-default.conf` like this </br>
![16 2](https://user-images.githubusercontent.com/81411468/139207020-9163f537-6612-4cd3-8d19-3249209661cd.PNG)

**Difficulties:**
- No difficulties

# Problem 17
**Because Franky also wants to invite his friends to be able to contact him through the website `www.super.franky.yyy.com`, and because web server visitors will definitely be confused by the random images that exist, Franky also asks to replace the image request that has the substring "franky" will redirected to franky.png. Then help Luffy to configure this dns and web server!**

Edit `/etc/apache2/sites-available/super.franky.iup04.com.conf` like this </br>
![17 1](https://user-images.githubusercontent.com/81411468/139207825-b9224fd4-c6b6-480a-8a8b-bf22ba9c8d70.PNG)

Edit `/var/www/super.franky.iup04.com/.htaccess` like this </br>
![17 2](https://user-images.githubusercontent.com/81411468/139207844-009a3b0c-e27b-415a-a1c3-a11d539824a0.PNG)

**Difficulties:**
- franky.png cant downloaded

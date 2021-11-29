## How to install WordPress with Plesk on DigitalOcean

This is one of the **cheapest **and **quickest **solutions to have a website up and running that contains a blog with backups and your own email. 
The WordPress site is hosted on DigitalOcean's virtual machine (droplet) that goes for as low as 5$/month. 

DigitalOcean compared to GCP, AWS, Azure, etc, offers a one click deployment with minimal configuration that allows you to host several WordPress sites (or CMS of your choice) through Plesk. This allows you to have personalized email accounts using your domain without additional cost. It's perfect for small businesses, MVPs or early projects. 

To start you need a [DigitalOcean](https://m.do.co/c/1e4904d4946c) account. From the referral link you get 100$ for 60 days. 


The guide is as follows:
1. Install Plesk on DigitalOcean
2. Set up Plesk and install your WordPress site
3. Set up SSL for WordPress
4. Set up the webmail on Plesk
5. Set up backups or snapshots for your DigitalOcean droplet

If you get lost and need technical support I can ignore you on [Twitter @tekbog](https://twitter.com/tekbog) 


# Install Plesk on DigitalOcean

What we are going to do is go to marketplace, search for  [Plesk ](https://marketplace.digitalocean.com/apps/plesk) and click on Create Plesk Droplet:

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636778240717/7AtrCtF1E.png)

After we select our machine (remember to save the password, I personally use  [KeePassXC](https://keepassxc.org/) ).

# Set up Plesk and install WordPress

We go into our droplet and copy the ip, which will lead us to this page:

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636772116594/0Y-qwhx-b.png)

Don't be too quick!

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636772136222/7csGSzVsB.png)

We will need to make an username and password, I'd recommend using a password manager like KeePassXC.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636772203078/5zFAZugHS.png)

Plesk ready to use:

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636772219358/VtWT20wxz.png)

Click on add a new domain, if you don't have one just select temporary domain and go to the install WordPress step:

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636772235249/Nakuo3MPy.png)

Once you have added your domain you will have to configure your DNS, just follow the link: 
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636772291454/4-7-s6K7a.png)

In my case I had to follow  [NameCheap](https://docs.plesk.com/en-US/obsidian/administrator-guide/72225/#namecheap) 's instructions but you can pick your registrar.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636772350199/BTlKe4baK.png)

What we want to do next is go to WordPress and install the site:
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636772408304/H0p_wWgzk.png)

It will ask for your admin's username and password:

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636772538045/D7T2NBKwK.png)

 after you set that up it will install WordPress:

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636772504987/PUcrMZLkV.png)

# Set up SSL for our WordPress site

The first thing you will notice when you have your site ready is that it lacks a security certificate 
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636772627047/D7Kc5pVik.png)

Web servers work through HTTP however in order to add security and encryption we add an SSL certificate (the 'S' in HTTPS stands for secure, so when you see https it just means the data is encrypted and secure). 
Just click on the "no certificate button" and "get SSL/TLS certificate":

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636772849010/k6LXAzITI.png)

You will see this page:
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636772881226/ZmlS_vBjU.png)

Feel free to buy one if you want, however a Let's Encrypt certificate is more than enough, click on install.

We want to secure everything since we will be using the webmail as well: 
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636773002573/nuv8FC17x.png)

In order to validate our domain we will need to add a TXT record in our DNS:


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636773195282/E_ODQ7zvF.png)

Plesk does this automatically.

While this is going on your server (droplet) might suffer a bit, just be patient:

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636773823560/nZJ0pow4Y.png)

Once you are done you will see that your site contains https:

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636773904469/YLDzhQeJvOh.png)

# Set up the webmail on Plesk

Our encryption is ready for our site, let's set up our email. Digital Ocean's default Plesk license allows 3 emails. Go to Mail and click on Create Email Address:

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636774035702/kNFngX_OP.png)

The next thing is to input the data, however I'd recommend on deactivating "Can be used to log in to Plesk" for security reasons:

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636774236685/d5IZwpNba.png)

In order to use our email we can open it through this button:
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636774325556/xLI6M2Q3J.png)
or just go to: https://webmail.your-domain.com

However due to security policies our outgoing mail is ending in spam, to fix this what we need to do is enable DKIM, go to mail, mail settings and click on your account, you will see the following:

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636775647897/r-zwltM2O.png)

Check the DKIM box, click on apply and then OK:
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636775678297/n9Pzx1jrO.png)

And in order to get rid of the 
> 
You cannot send emails from Plesk because outbound connections on TCP port 25 is blocked. Check the firewall settings or contact your hosting provider. If you are sure that the ports are already open, Plesk can recheck them. Start the recheck

Just click on start Recheck, if you are not sure if it has worked go to your DNS settings and check for a DKIM record. 
I've had problems with this issue before, [there's even a support article from Plesk here](https://support.plesk.com/hc/en-us/articles/213934285-Unable-to-receive-or-send-e-mails-port-25-is-blocked) however you shouldn't worry about doing anything with the firewall. 
Another possible issue related to DKIM records can also be found  [here](https://support.plesk.com/hc/en-us/articles/115004142193-Emails-go-to-Spam-DKIM-record-is-corrupted). The solutions is literally to turn it off and on, like always.


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636780144878/4V4VbV6mg.png)

**It's very important to double check that our email works properly before launching our site or starting a marketing campaign, make sure it doesn't land in spam!**

# Set up backups for your DigitalOcean droplet

DO **NOT **FORGET BACKUPS!

You can also use [Plesk ](https://docs.plesk.com/en-US/obsidian/administrator-guide/backing-up-and-restoration.59256/) for backups but we are going to just snapshot our entire VM.

Go to droplets, click on your droplet and then click on backups:
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636780641749/TYj-9NcNO.png)

This costs an additional $1, however you can also just do Snapshots on your own, which is what I do for new projects that haven't exactly started yet:

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636780734533/vnyHyS-yN.png)
Once you have created your snapshot all you have to do is restore when things go wrong:
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636780778982/KDeat2IOL.png)

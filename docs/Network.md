<h1>Network Configuration</h1>

-   [Get my local IP](#get-my-local-ip)
-   [Open my ports](#open-my-ports)
-   [Create a No-IP Domain Name](#create-a-no-ip-domain-name)
    -   [Go to no-ip.com](#go-to-no-ipcom)
-   [Generate the SSL/TLS Certificate](#generate-the-ssltls-certificate)
    -   [Certbot](#certbot)

## Get my local IP

To properly configure Bridger you will at somestimes need to specify your local IP address.

To get your local IP address on Windows 10 :

-   Go to the [Network and Internet settings](ms-settings:network-status)
-   Click on the **Properties** button below the drawing
-   Scroll down to the **Properties** section
-   And look for the **IPv4 Address** row

There, is your local IP, something like `192.168.0.x`, keep it in mind.

## Open my ports

To access and comunicate with RTMP Bridger from the outside world, we need to configure your router and open some ports, nothing more simple right.

So to make this, go to the admin/dashbord page of your router, it is different from an ISP to another but it may be something like [mybox.yourisp.com]() or 192.168.0.1, just google it.

Next look for a Port Forwarding section, click and see if there is an array like:

| Protocol  |     IP      | Port | Note |
| :-------: | :---------: | :--: | :--: |
| TCP / UDP | 192.168.x.x | ...  | ...  |
|    ...    |     ...     | ...  | ...  |

Found it ? Then try to add a new row, well 4 new rows. We will open the port 80 and three random ports, like 3300, 3301 and 3302, as you wish. The ports must redirect the traffic to your computer, either enter the name of your computer if it is possible or in the IP column enter your local IP, see [Get my Local IP](#get-my-local-ip)

> **Note :** Excepted the port 80, the other ports must be set between the numbers 1024 and 49151. Also, **do not** choose port 3299 which is used for internal functions.

At the end it must be something like :

| Protocol |      IP       | Port |          Note           |
| :------: | :-----------: | :--: | :---------------------: |
|   TCP    | your local ip |  80  |         Cerbot          |
| TCP/UDP  | your local ip | 3300 |   RTMP Bridger Stream   |
| TCP/UDP  | your local ip | 3301 | RTMP Bridger Dashboard  |
| TCP/UDP  | your local ip | 3302 | RTMP Bridger OBS Remote |
|   ...    |      ...      | ...  |           ...           |

And thats it, some router require to be restared it depends.

## Create a No-IP Domain Name

To facilitate the usage of your public IP by RTMP Bridger, we need to set up a domain name so that your public IP which must remain secret to your audience can be used by Bridger and yourself. But it is worst noted that a domain name is just a layer for kids who don't know how to use it, not a security in itself. So keep that domain for you and your modaration.

To create our free domains we use no-ip.com but of course you can use any service you want. Your free domain will have to be confirm each month.

### Go to [no-ip.com](https://noip.com)

Create a free account, login, and create your domain e.g. liuzhgjrbbrhj.ddns.net . As you can see, a bunch of characters suits well, it will always be accessible on your [no-ip.com](https://noip.com) account dashboard.

And done ! We will use that domain to [Generate the SSL/TLS Certificate](#generate-the-ssltls-certificate).

## Generate the SSL/TLS Certificate

Because RTMP Bridger uses of course the lastest technologies, it must be secured.

To establish a secure connection with a website (HTTPS) and to garantee the veracity of a domain, we use SSL/TLS Certificates, and this is what you are about to create.

There are free and paid certificate, but in our case a free one will perfectly suits. _Let's Encrypt_ provide free certificates, generated with a tool called **Certbot**. It is worst noted that your certificate will expire 3 month after his generation.

So the objective is to install Certbot and generate a certificate for RTMP Bridger.

### Certbot

So first of all we need to :

-   Download the latest [Certbot](https://github.com/certbot/certbot/releases) release, just click on `certbot-beta-installer-win32.exe ` in the **Assets** section
-   Install it by following the instalation process (let all settings to default if possible)

> **Note :** The port 80 must be open during the next process, see [Open your ports](#open-your-ports) to know how to configure this.\_

Once the installation complete, launch Certbot in administrator and copy/paste the next command :

```shell
certbot certonly --standalone -n --agree-tos -d [DOMAIN] -m [EMAIL] & icacls C:\Certbot\archive\* /grant *S-1-1-0:(OI)(CI)RX & icacls C:\Certbot\live\* /grant *S-1-1-0:(OI)(CI)RX
```

Replace `[DOMAIN]` by the domain name you would like RTMP Bridger to use and replace `[EMAIL]` by your email address, you will be warned when your certificate get to his expiration date.

Et voilà, you now have an SSL/TLS Certifiacte atteched to your domain, it will be automatically installed by RTMP Bridger.

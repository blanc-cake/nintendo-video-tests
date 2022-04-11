# Nintendo Video Tests

Nintendo Video is a discontinued service for the Nintendo 3DS, used to download videos for viewing via the console.

This repo aims to explore methods of replicating this service by feeding archived BOSS (Spotpass) files to the application through the use of a web debugger. This is just the basic setup for testing, and is not guaranteed to work.

(The below tutorial assumes you are using Windows 10)

# Requirements

+ An installation of [Charles Proxy](https://www.charlesproxy.com/), this can also be done with [mitmproxy](https://mitmproxy.org/), though Charles is more user friendly.
+ A Nintendo 3DS running [CFW](https://3ds.hacks.guide/)
+ A CIA of Nintendo Video (USA, this is because the only available BOSS files are for US regions) of which can be found on the Internet Archive.
+ BOSS data of your region and language (Currently only USA - English and USA - Spanish BOSS data is available.). [Link](https://github.com/blanc-cake/nintendo-video-tests/tree/main/boss-files/USA%20(Region%2045))

# Setup

1. First of all, open up Charles Proxy. Open up '**Proxy** > **Proxy Settings**' and take note of the first four-digit port number. If you would like, you can use your own. Click 'OK'.
2. On your 3DS, open System Settings and go to '**Internet** > **Connection Settings** > **(Network shared with your PC)* > **Change Settings** > **Proxy Settings**
3. Select '**Yes**', then choose '**Detailed Setup**'. Input the local IP of your PC as the Proxy Server, and change the port number to the port you used for Charles in step one. Tap 'OK'.

If everything went smoothly, saving your settings and preforming a connection test should prompt you to accept or deny a connection from a local IP (Choose accept), then display a connection to 'http://conntest.nintendowifi.net/' on Charles. If so, you should now be able to move on to the following steps.

# Method 1 - Map Local and Include Requests

When installed and set up (do not do this yet), Nintendo Video will attempt a connection to several URLs.

`http://pubus-p.est.c.app.nintendowifi.net/1/49/1/ESE_MD1`

`http://pubus-p.est.c.app.nintendowifi.net/1/49/1/ESE_MD2`

`http://pubus-p.est.c.app.nintendowifi.net/1/49/1/ESE_MD3`

`http://pubus-p.est.c.app.nintendowifi.net/1/49/1/ESE_MD4`

If you preform a connection test, it will search for

`http://pubus-p.est.c.app.nintendowifi.net/1/49/1/CHECK`

As well as the aforementioned URLs.

To quote 3dbrew on the connection test sequence -
> The server responds with either a 403 or 404 error code, where 403 means that user's region (determined by IP, I guess) doesn't match the region specified by COUNTRYCODE and COUNTRYSUBDOMAIN and 404 means that everything's OK.

Charles has a feature that allows you to respond to request with a locally stored file. This is what we'll be using to feed BOSS data stored on our PC to Nintendo Video. Seeing as we only have 3 backups of ESE_MD1 for USA region English/Spanish, we will be using one of them.

To do this, in Charles open up '**Tools** > **Map Local**' and click '**Add**'. In the menu that opens input the following, mapping to your locally downloaded BOSS data - 

<img src="https://github.com/blanc-cake/nintendo-video-tests/blob/main/tutorial%20images/local_mapping.PNG" width="436.5" height="406">

Click '**OK**'.

Optionally, you can also choose to only record connections from the URLs that we will be focusing on, ignoring others.

For this, open up '**Proxy** > **Recording Settings** > **Include**' and add three URLs. One **http** on port **80** for `*.nintendowifi.net`, and two **https** on port **443** for `*.nintendo.net` and `*.nintendowifi.net`. Although the latter two aren't nessecary, they can help to visualise things.

<img src="https://github.com/blanc-cake/nintendo-video-tests/blob/main/tutorial%20images/include_requests.PNG" width="540" height="352">

# Method 2 - Map Remote and Include Requests

(This method assumes you have a server setup)

Similarly to what was mentioned in Method 1, Charles has a feature that allows you to respond to request with a file stored on a server differing in domain name than that of the reqest. This feature is what we'll be using to feed BOSS data stored on said server to Nintendo Video.

To do this, in Charles open up '**Tools** > **Map Remote**' and click '**Add**'. In the menu that opens input the following, mapping to the BOSS data within your server that.

<img src="https://github.com/blanc-cake/nintendo-video-tests/blob/main/tutorial%20images/remote_mapping.PNG" width="422" height="522">

Click '**OK**'.

Optionally, you can also choose to only record connections from the URLs that we will be focusing on, ignoring others.

For this, open up '**Proxy** > **Recording Settings** > **Include**' and add three URLs. One **http** on port **80** for `*.nintendowifi.net`, and two **https** on port **443** for `*.nintendo.net` and `*.nintendowifi.net`. Although the latter two aren't nessecary, they can help to visualise things.

<img src="https://github.com/blanc-cake/nintendo-video-tests/blob/main/tutorial%20images/include_requests.PNG" width="540" height="352">

# Install and test

We can now get to testing the Charles setup. With Charles 'recording', install your CIA of Nintendo Video and open it up.

Obviously, choose to receive both videos over Spotpass, as well as notifications for Nintendo Video.

After setting up Nintendo Video, leave your 3DS open on the main menu for a minute or two, and it will begin attempting to download BOSS data. If all is right, it should begin downloading your locally/remotely stored ESE_MD1 and fail to download MD2, MD3 and MD4. You should've also recieved a notification telling you that Nintendo Video is moving.

<img src="https://github.com/blanc-cake/nintendo-video-tests/blob/main/tutorial%20images/IMG20220407124904.jpg" width="445.7" height="594.2">

My console's region is AUS - English, so that may be one of the reasons why videos don't show up after being downloaded. However the results will probably differ depending on the datas hex timestamp, the set date/time, the consoles region, or something entirely different.

Huge thanks to the contributers of [Nintendo Videos page on 3dbrew](https://www.3dbrew.org/wiki/Nintendo_Video) (especially popoffka) for their hard work. I really recommend giving it a read.

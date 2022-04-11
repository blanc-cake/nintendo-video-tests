# Nintendo Video Tests

Nintendo Video is a discontinued service for the Nintendo 3DS, used to download videos for viewing via the console.

This repo aims to explore methods of replicating this service by feeding archived BOSS (Spotpass) files to the application through the use of a web debugger.

The below tutorial assumes you are using Windows 10

# Requirements

+ An installation of [Charles Proxy](https://www.charlesproxy.com/), this can also be done with [mitmproxy](https://mitmproxy.org/), though Charles is more user friendly.
+ A Nintendo 3DS running [CFW](https://3ds.hacks.guide/) (Preferred, not required given Nintendo Video's servers use HTTP)
+ A copy of Nintendo Video (USA, this is because the only available BOSS files are for US regions) installed to said 3DS (Can be found on certain sites)
+ BOSS data of your region and language (Currently only USA - English and USA - Spanish BOSS data is available.)

# Setup

1. First of all, open up Charles Proxy. Open up '**Proxy** > **Proxy Settings**' and take note of the first four-digit port number. If you would like, you can use your own. Click 'OK'.
2. On your 3DS, open System Settings and go to '**Internet** > **Connection Settings** > **(Network shared with your PC)* > **Change Settings** > **Proxy Settings**
3. Select '**Yes**', then choose '**Detailed Setup**'. Input the local IP of your PC as the Proxy Server, and change the port number to the port you used for Charles in step one. Tap 'OK'.

If everything went smoothly, saving your settings and preforming a connection test should prompt you to accept or deny a connection from a local IP (Choose accept), then display a connection to 'http://conntest.nintendowifi.net/' on Charles. If so, you should now be able to move on to the following steps.

# Map Local

After being set up, Nintendo Video will attempt a connection to several URLs.

`http://pubus-p.est.c.app.nintendowifi.net/1/49/1/ESE_MD1`

`http://pubus-p.est.c.app.nintendowifi.net/1/49/1/ESE_MD2`

`http://pubus-p.est.c.app.nintendowifi.net/1/49/1/ESE_MD3`

`http://pubus-p.est.c.app.nintendowifi.net/1/49/1/ESE_MD4`

If you preform a connection test, it will search for

`http://pubus-p.est.c.app.nintendowifi.net/1/49/1/CHECK`

As well as the aforementioned URLs.

To quote 3dbrew on the connection test sequence -
> The server responds with either a 403 or 404 error code, where 403 means that user's region (determined by IP, I guess) doesn't match the region specified by COUNTRYCODE and COUNTRYSUBDOMAIN and 404 means that everything's OK.

Charles has a feature that allows you to respond to request with a locally stored file. This is what we'll be using to feed BOSS data stored on our PC to Nintendo Video. Seeing as we only have

To do this -

1. In charles, open up '**Tools** > **Map Local**'

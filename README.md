# Nintendo Video Tests

Nintendo Video is a discontinued service for the Nintendo 3DS, used to download videos for viewing via the console.

This repo aims to explore methods of replicating this service by feeding archived BOSS (Spotpass) files to the application through the use of a web debugger.

The below tutorial assumes you are using Windows 10

# Requirements

+ An installation of [Charles Proxy](https://www.charlesproxy.com/)
+ A Nintendo 3DS running [CFW](https://3ds.hacks.guide/) (Preferred, not required given Nintendo Video's servers use HTTP)
+ A copy of Nintendo Video (USA, this is because the only available BOSS files are for US regions) installed to said 3DS (Can be found on certain sites)

# Setup

1. First of all, open up Charles Proxy. Under the 'Proxy' tab, open up 'Proxy Settings' and take note of the first four-digit port number. If you would like, you can use your own. Click 'OK'.
2. On your 3DS, open System Settings and go to '**Internet** > **Connection Settings** > **(Network shared with your PC)* > **Change Settings** > **Proxy Settings**
3. Select '**Yes**', then choose '**Detailed Setup**'. Input the local IP of your PC as the Proxy Server, and change the port number to the port you used for Charles in step one. Tap 'OK'.

If you did everything right, saving your connection settings and preforming a connection test should display a connection to 'http://conntest.nintendowifi.net/' on Charles. If so, you should now be able to move on to the following steps.


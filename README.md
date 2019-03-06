# PenguinShooterWeb
This project contains a Web Interface to generate invoices for the PenguinShooter Lightning Network game https://github.com/Donno1994/PenguinShooter

This is a demo project on how the LN can be used for user integration in live streams.
You can play PenguinShooter live on twitch or youtube and let your viewers pay invoices to help or annoy you.

Here is a link to my medium article https://medium.com/@BR_Robin/user-intervention-in-livestreams-via-ln-penguinshooter-5e12bdcece49

And a video explaining this https://www.youtube.com/watch?v=gTuWi-WNynQ&t



The game itself is definitely not the best game in the world, but it shows how LN payments can work ingame.
If you sometimes do live videos, you could consider streaming this and let viewers change your livestream with their payments.
Unfortunately I don't know how to stream. I always had a bad video quality and 10 seconds delay (which is a lot if you want to see the results live).
I found out that streaming is a huge project for itself, so I hope there is someone who has already more experience wants to give it a try :)

## Requirements

To connect this game with your own node, you need the LND implementation of LN https://github.com/lightningnetwork/lnd Important are the invoice.macaroon and tls.cert
You need to setup portforwarding (port 8079)

You need a windows computer (your viewers don't need it)

## Instructions 

1. If you have not done it already, download PenguinShooter on https://github.com/Donno1994/PenguinShooter and follow the instructions
2. Download this repository
3. Do you want to connect to your own node? Go to step 4. Connect to developer node? Go to step 7
4. Enter the folder PenguinShooterWeb-master\PenguinShooterWeb_Data\Resources and open donner.conf
5. Replace "penguinshooter.chickenkiller.com" with the IP of your LND node and set the correct port
6. Copy your invoice.macaroon and your tls.cert into the same folder as donner.conf. You can find this in your LND folder under ".lnd/data/chain/bitcoin/mainnet/invoice.macaroon" and ".lnd/tls.cert"
7. Run the file "PenguinShooterWeb.exe"
8. Enter the name in the text field that you use in PenguinShooter (must be the exact same name)
9. The webserver will be accessible on port 8079. Open your webbrowser and enter 127.0.0.1:8079.
If you want your viewers to access it, you need to setup port forwarding. They will have to enter "your-public-ip:8079" into their browser.
10. On the website you can enter a nickname (numbers and letters) which will be displayed in the game
11. Press one of the buttos to create invoices.
12. You can now 
- scan the QR code with your mobile wallet
- click it to open your desktop wallet
- copy the invoice to your clipboard and paste it into your wallet
13. When you pay the invoice, you should see the result in your game.
14. If an invoice is paid, the price  doubles for that feature and then gets down again (halving every 2 minutes) until the price reaches the base price.
On the webserver you can change the base price and disable buttons.
When you are still low level I suggest you disable the "Evil Tiger" function


## How does this work?
The game and the webserver both connect to the LND node as the server.
The game uses the SubscribeInvoices feature of LND to get information about all invoices that were paid. It doesn't matter who created or paid them.
<br>The game will now check if the invoice was created via the game. If yes, do something
<br>It will also check if the username equals the name in the invoice (after the "->"). If yes, do something.
<br>The viewer will connect to the webserver via his webbrowser. If he clicks a button, the webserver will generate an invoice which looks like this
<br>sender->streamer:action

The game will check the "action" part and depending on what it says, it will do something.
<br>The whole communication goes via the invoice memos.
<br>This is not the best approach because everyone could fake the memos who has the invoice.macaroon.
<br>That's why I hard coded my invoice.macaroon into the game.
<br>Another downside is: You need payments. It's not possible to send a simple chat message to the ingame chat without paying an invoice.

Anyway, that's my first approach to LN gaming.
<br>If you want to test it, you are more than welcome to use it.
<br>I would be very happy if there's someone who would like to stream it live.
<br>If I have time, I will join and send some satoshis to freeze and fight you ;)

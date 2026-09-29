# Pandanoko

## StreetPass
This section gives a basic explanation of how StreetPass works on 3DS.  
On every 3DS, there is a StreetPass inbox and outbox for every game. A game can now put StreetPass messages into the outbox and read from the inbox.
The 3DS-system then takes, even if the app is closed, messages from the outbox and sends them to other 3DS systems. Incoming StreetPass messages will be put into the game's inbox.  
The game can also specify how many people can receive outgoing messages and how often they can be forwarded. Forwarding means that, if the 3DS receives a messages it is immediately also put into the outbox for others to receive.

## StreetPass in Yo-kai Watch
Yo-kai Watch games update their StreetPass outbox every time the player talks to the manager of the Wayfarer Manor and every time the player enters Blossom Heigts with new StreetPass messages in their
inbox. The game then puts a "Yo-kai have wandered into your city."-message with the current team into the StreetPass outbox. This message can be sent out an infinite number of times.  
The game also puts a "A strange Yo-kai has wandered into your city!"-message into the outbox that can only be sent out one time and forwarded 255 times (that's a Pandanoko the next StreetPass connection will receive) in two cases:

* The game just received a Pandanoko and it was not already forwarded to another system
* The BitFlag `0xC27065E9` (`passcomm_ex_send`) is set to 1
  * This BitFlag has a 1% chance to be set to 1 at the creation of the save file and is set to 0 after a Pandanoko was sent.

If the game receives a Pandanoko the BitFlag `0x3CDB0D89` (`passcomm_ex_recv`) is set to 1, making Pandanoko appear in the Wayfarer Manor.

## Yo-kai Watch 3
Starry Noko (YW3) works the same way. It uses the BitFlag `0xC3C194B4` (`passcomm_ex_send2`) with another independent 1% RNG roll on game creation. If Starry Noko was received BitFlag `0x8E8D5E84` (`passcomm_ex_recv2`) is set to 1.
That means there is a 0.01% chance that a new save file will send out both Pandanoko and Starry Noko at the same time.  
However if the game has both Starry Noko and Pandanoko in the inbox, the game only spawns a Pandanoko, but forwards only Starry Noko. 
If the game was not started and another StreetPass happens, both Pandanoko and Starry Noko get sent, because of the forward count of 255.  
That means if a game generates both Nokos, they are both sent to the next consoles and if everyone gets another StreetPass before opening the game, everyone will get Pandanoko. If someone then opens the game
before getting another StreetPass, the persons after that will get a Starry Noko.


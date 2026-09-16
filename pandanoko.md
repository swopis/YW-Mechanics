# Pandanoko

## StreetPass
This section gives a basic explanation of how StreetPass works on 3DS.  
On every 3DS, there is a StreetPass inbox and outbox for every game. A game can now put StreetPass messages into the outbox and read from the inbox.
The 3DS-system then takes, even if the app is closed, messages from the outbox and sends them to other 3DS systems. Incoming StreetPass messages will be put into the game's inbox.  
The game can also specify how many people can receive outgoing messages.

## StreetPass in Yo-kai Watch
Yo-kai Watch games update their StreetPass outbox every time the player talks to the manager of the Wayfarer Manor and every time the player enters Blossom Heigts with new StreetPass messages in their
inbox. The game then puts a "Yo-kai have wandered into your city."-message with the current team into the StreetPass outbox. This message can be sent out 255 times.  
The game also puts a "A strange Yo-kai has wandered into your city!"-message into the outbox that can only be sent out one time (that's a Pandanoko the next StreetPass connection will receive) in two cases:

* The game just received a Pandanoko
* The BitFlag `0xC27065E9` (`passcomm_ex_send`) is set to 1
  * This BitFlag has a 1% chance to be set to 1 at the creation of the save file and is set to 0 after a Pandanoko was sent.

Starry Noko (YW3) works the same way. It uses the BitFlag `0xC3C194B4` (`passcomm_ex_send2`) with another independent 1% RNG roll on game creation.

If the game receives a Pandanoko the BitFlag `0x3CDB0D89` (`passcomm_ex_recv`) is set to 1, making Pandanoko appear in the Wayfarer Manor. Starry Noko uses BitFlag `0x8E8D5E84` (`passcomm_ex_recv2`) for that.

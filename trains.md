# Trains

## Happy Go Lucky Express
Each time the player enters a station there is a 10% chance that a bit flag (`0x33CEE5A0`) is set to 1 (otherwise it's set to 0). If this flag is set to 1, every arriving train has a 10% chance to be
the Happy-Go-Lucky Express.

## CfgBin-Tags
```
TRAIN_DATA (
	TrainID|True
	Direction(0=Left,1=Right)|False
	Line|False
	TrainType|False
	DestStationName|True
	Cond|False
	DisplayedDestination|False
	OpposingTermStation|True
	Unk8|False
	TrainRank|False
	TrainTribe|False
)
```

### Explanation
* Line
  * 0: Central Line
  * 1: Central Express Line
  * 2: Echo Line
  * 3: Fox Line
  * 4: Hexpress/Happy-Go-Lucky
* TrainType
  * 0: Normal
  * 1: Nonstop
  * 2: Hexpress
  * 3: Happy-Go-Lucky Express
* DestStationName: The terminating station
* TrainRank (Hexpress): Rank of the train (0 = E, 1 = D, ...)
* TrainTribe (Hexpress): Tribe of the train (1 = Charming, ...)

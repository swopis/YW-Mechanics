# Yo-kai Cam

## MyTags For `/data/res/face/face_config_[ver].cfg.bin`
```
FACE_FEATURE (
    CalcFn|False
    Point1|False
    Point2|False
    Point3|False
    Point4|False
    Threshold1|False
    Threshold2|False
)

FACE_YOKAI (
    FaceID|False
    ParamID|True
)
```

## Face Points
The game identifies the following 27 face points:

```

0                                             1
        28      31 (eyebrows) 25       32

            36                     44
        34  4   38    (eyes)   46  5   42
            40                     48


                      61 (nose)

                      67
                   65    69
                64  (mouth) 70
                   75    71
                      73
3                                             2


```
The numbers represent the IDs of the points, which are used in the CfgBin file.

## Face Feature
The game calculates a face feature as a floating point value, by taking up to four face points (`PointX`) and running them through a calculate function (`CalcFn`).
There are 5 used functions.

### Face Feature Functions

| Function ID | Description                                                                 | Mathematical Description                                                                                     |
| ----------- | --------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| 0           | Calculates the distance between two points.                                 | $d(P1, P2) = \sqrt{(x_{1} - x_{2})^2 + (y_{1} - y_{2})^2} \times 100$                                        |
| 1           | Calculates the ratio of the average of two distances and a reference width. | $\frac{\frac{1}{2}(d(P1,P2) + d(P3,P4))}{2362} \times 100$                                                   |
| 2           | Calculates the ratio of two distances.                                      | $\frac{d(P3, P4)}{d(P1, P2)} \times 100$                                                                     |
| 3           | Calculates the average of orientation of two lines in degrees.              | $\frac{atan2(y_{1} - y_{2}, x_{1} - y_{1}) + atan2(y_{3} - y_{4}, x_{3} - x_{4})}{2} \times \frac{180}{\pi}$ |
| 5           | Takes a value from the face scanner (probably gender?).                     | -                                                                                                            |

## Face ID
Using the face features the game then calculates a Face ID as follows:  
For each face feature the game creates a digit between 0 and 1. One if the face feature value is greater than `Threshold1` and zero if it's smaller than `Threshold1`.
These digits are then packed into a base-4 number, with the first feature being the most significant digit. This number is the Face ID, which is used to look up the Yo-kai from the CfgBin file.


## Face Features in Yo-kai Watch 1 and Yo-kai Watch 2
Yo-kai Watch 1 and 2 use nine face features to differentiate 512 different Face IDs.

| Feature ID | `CalcFn` | `Point1` | `Point2` | `Point3` | `Point4` | Description                                                  | `Threshold1` |
| ---------- | -------- | -------- | -------- | -------- | -------- | ------------------------------------------------------------ | ------------ |
| 0          | 5        | -        | -        | -        | -        | Probably Gender; Male > 0, Female < 0                        | 0            |
| 1          | 0        | 64       | 70       | -        | -        | Distance between outer points of mouth                       | 45           |
| 2          | 2        | 31       | 28       | 38       | 34       | Distance ratio left eye and left eyebrow                     | 80           |
| 3          | 3        | 31       | 28       | 25       | 22       | Average orientation of left and right eyebrow                | -3           |
| 4          | 1        | 34       | 38       | 46       | 42       | Average eye width                                            | 18           |
| 5          | 0        | 38       | 46       | -        | -        | Distance between eyes                                        | 28           |
| 6          | 1        | 38       | 61       | 46       | 61       | Average distance from eye to nose                            | 31           |
| 7          | 1        | 31       | 38       | 25       | 46       | Average distance from inner eye point to inner eyebrow point | 17           |
| 8          | 0        | 61       | 67       | -        | -        | Distance between nose and mouth                              | 10           |

To find out which Yo-kai needs what features and vice versa, you can use this tool: https://swopis.github.io/YW-Mechanics/ycam/

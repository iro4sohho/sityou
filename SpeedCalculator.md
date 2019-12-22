SpeedCalculator object
+ calculates speed of chatdata (per minute).<br><br>
SpeedCalculatorはチャットの勢いを算出するChatProcessorです。<br>
### Usage
### on-demand style
```python
import SpeedCalculator
chat = LiveChat("xxxxxxxxxxx", processor = SpeedCalculator(capacity = 20)) 
while chat.is_alive():
    speed = chat.get()
    print(speed)
    time.sleep(3)
```
### callback style
```python
import SpeedCalculator
chat = LiveChat("xxxxxxxxxxx", 
           processor = SpeedCalculator(), 
           callback = disp_speed) 
while chat.is_alive():
    time.sleep(3)

def disp_speed(speed):
    print(speed)
```



## Constructor parameter 
### capacity : int
(default value = 10) <br>
 <br>
the max capacity of speed data for calculating speed. <br>
`Speed data` has numbers of chat data, and start time / end time of chat. <br>
Each speed data are stored to ring queue, so if the count of speed data  exseeds capacity, <br>
oldest item is overwritten by new one.



SpeedCalculator object

SpeedCalculatorはチャットの勢いを算出するChatProcessorです。<br>

### on-demand モードでの使用例
```python
from pytchat import LiveChat, SpeedCalculator
chat = LiveChat(video_id = "xxxxxxxxxxx", processor = SpeedCalculator(capacity = 20)) 
while chat.is_alive():
    speed = chat.get()
    print(speed)
    time.sleep(3)
```
### callback モードでの使用例
```python
from pytchat import LiveChat, SpeedCalculator
chat = LiveChat("xxxxxxxxxxx", 
           processor = SpeedCalculator(), 
           callback = disp_speed) 
while chat.is_alive():
    time.sleep(3)

def disp_speed(speed):
    print(speed)
```



## パラメータ
### capacity : int
(規定値 ： 10) <br>
 <br>
チャット勢いの算出に使用するチャットブロックの格納数を指定します。 <br>
YouTubeから1回あたりに取得されるチャットブロックは5秒~10秒の間に流れたチャットデータに相当します。<br>
直近に取得した複数のチャットブロックを用いてチャットの勢いを算出します。<br>
指定した数以上のチャットブロックを取得した場合、古いブロックから上書きされます。

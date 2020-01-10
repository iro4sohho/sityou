<br>
複数のChat Processorを使用する場合は、タプルで指定します。

```python
chat = LiveChat("video_id", processor = (DefaultProcessor(), SpeedCalculator()) )

```
<br>
各々のprocessorの戻り値（加工後データ）も、タブルで受け取ります。<br>

```python
data, speed = chat.get()
```

上の例では、`data` に DefaultProcessor の戻り値、  `speed` に SpeedCalculator の戻り値が格納されます.
<br>
<br>
戻り値の順番は、processorパラメータで指定したChat Processorの順番と同じです。
<br>
<br>
## Example code:
```python
from pytchat import LiveChat, DefaultProcessor, SpeedCalculator

def multiple_processor_demo():
  chat = LiveChat("video_id",  
         processor = ( DefaultProcessor(), SpeedCalculator() ))
  while chat.is_alive():
    data, speed = chat.get()
    for c in data.items:
      print(f"{c.elapsedTime.rjust(8)} <{c.datetime}> [{c.author.name}]-{c.message}")
      data.tick()
    print(f"[speed:{speed} it/m]")


if __name__ =='__main__':
  multiple_processor_demo()

```
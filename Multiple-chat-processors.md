You can use multiple chat processors simultaneously,<br>
<br>
by specifying chat processors as **tuple**.<br>
<br>

```python
chat = LiveChat("video_id", processor = (DefaultProcessor(), SpeedCalculator()) )

```
<br><br>
The return values are also tuple.<br>
<br>

```python
data, speed = chat.get()
```

In the above example, `data` is return of DefaultProcessor, and `speed` is return of SpeedCalculator.
<br>
<br>
The order of returns depends on the order of specified processors.
<br>
<br>
## Example code:
```python
from pytchat import LiveChat, DefaultProcessor, SpeedCalculator

def multiple_processor():
  chat = LiveChat("video_id",  
         processor = ( DefaultProcessor(), SpeedCalculator() ))
  while chat.is_alive():
    data, speed = chat.get()
    for c in data.items:
      print(f"{c.elapsedTime.rjust(8)} <{c.datetime}> [{c.author.name}]-{c.message}")
      data.tick()
    print(f"[speed:{speed} it/m]")


if __name__ =='__main__':
  multiple_processor()

```
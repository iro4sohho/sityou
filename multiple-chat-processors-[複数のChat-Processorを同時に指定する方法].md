You can use multiple chat processors simultaneously,<br>
<br>
by specifying chat processors as **tuple**.<br>
<br>
複数のChat Processorを使用する場合は、タプルで指定します。

```python
chat = LiveChat("video_id", processor = (DefaultProcessor(), SpeedCalculator()) )

```

The return values are also tuple.<br>
<br>
各々のptocessorの戻り値（加工後データ）もタブルで返ってきます。<br>
<br>
```python
data, speed = chat.get()

## on the asyncio context
data, speed = await chat.get()
```
`data` is return of DefaultProcessor, and `speed` is return of SpeedCalculator.
<br>
<br>
The order of returns depends on the order of specifying processors.
<br>
<br>
## Example code:
```python
def display(data, speed):
  for c in data.items:
    print(f"{c.elapsedTime.rjust(8)} <{c.datetime}> [{c.author.name}]-{c.message}")

    data.tick()
  print(f"----------speed--------:{speed} it/m")

def multiple_processor():
  chat = ReplayChat("ojes5ULOqhc",  
         processor = ( DefaultProcessor(), SpeedCalculator() ))
  while chat.is_alive():
    data, speed = chat.get()
    display(data, speed)
    time.sleep(3)

if __name__ =='__main__':
  multiple_processor()

```
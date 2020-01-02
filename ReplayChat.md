#### Warning : ReplayChat is deprecated and will be integrated with LiveChat in v0.5.0.0
ReplayChat object 
+ fetches past chat data of archived videos and stores them in buffer with ThreadpoolExecutor.
+ responds to user inquiries of get().
+ invokes callback function with processed chat data.
+ can retrieve chat data disabled by editing video.
```python
from pytchat import ReplayChat
import time

chat = ReplayChat("gb01h_eT0pw", seektime = 1000, callback = disp)
while chat.is_alive():
  time.sleep(3)

def disp(data):
  for c in data.items:
    print(f"{c.datetime} [{c.author.name}]-{c.message} {c.amountString}")
    time.sleep(3)
```
## #constructor params

name|type|required|remarks|default value
---|---|---|---|---
video_id|str|*|ID of youtube video.|-
processor|ChatProcessor|||DefaultProcessor
buffer|Buffer||buffer of chat data fetched background.|Buffer(maxsize=20)
interruptable|bool|||True
callback|func||[optional] function called from _listen() periodically.|None
done_callback|func||[optional] function called when listener ends.|None
direct_mode|bool| |If True, invoke specified callback function without using buffer.|False
seektime|int| |seek time of chat (seconds).|0 (start of chat)
## get()
description|return value
---|---
Get processed chat data from buffer.|processed chat data

## pause()
description|return value
---|---
pause chat fetching to buffer.|-

## resume()
description|return value
---|---
resume chat fetching to buffer.|-

## is_alive()
description|return value
---|---
Check if chat stream is alive.|bool

## terminate()
description|return value
---|---
Terminate fetching chat.|-


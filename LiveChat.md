#### planning to integrate ReplayChat into LiveChat
LiveChat object 
+ fetches chat data and stores them in buffer with ThreadpoolExecutor
+ responds to user inquiries of get().
+ invokes callback function with processed chat data.
+ can replay archived chat data.
## Usage
```
from pytchat import LiveChat
chat = LiveChat("gb01h_eT0pw")

while chat.is_alive():
    data = chat.get()
    items = data.items()
    for c in items:
        print(c.author.name, c.message)
        data.tick()
```
## #constructor params

name|type|required|remarks|default value
---|---|---|---|---
video_id|str|*|ID of youtube video.|-
processor|ChatProcessor|||DefaultProcessor
buffer|Buffer||buffer of chat data fetched background.|Buffer(maxsize=20)
interruptable|bool|||True
callback|func||function called from _listen() periodically.|None
done_callback|func||function called when listener ends.|None
direct_mode|bool| |If True, invoke specified callback function without using buffer.|False
seektime|int| |start position of fetching chat (seconds). This option is valid for archived chat only. If negative value, fetches chatdata which is posted before start broadcasting.|0
force_replay|bool| |force to fetch archived chat data, even if specified video is live.|False
## get()
description|return value
---|---
Get processed chat data from buffer.|processed chat data

## is_alive()
description|return value
---|---
Check if livechat stream is alive.|bool

## terminate()
description|return value
---|---
Terminate fetching livechat.|-


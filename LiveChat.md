# LiveChat

LiveChat object 
+ fetches chat data and store in the buffer with ThreadpoolExecutor
+ responds to user inquiries of get().
+ invokes callback function with processed chat data.

## Usage
```
from pytchat import LiveChat
chat = LiveChat("gb01h_eT0pw")
```
## #constructor params

name|type|required|remarks|default value
---|---|---|---|---
video_id|str|*|ID of youtube video.|-
processor|ChatPrcessor|||DefaultProcessor
buffer|Buffer||buffer of chat data fetched background|Buffer(maxsize=20)
interruptable|bool|||True
callback|func||[optional] function called from _listen()  periodically|None
done_callback|func||[optional] function called when listener ends.|None
direct_mode|bool| |If True, invoke specified callback function without using buffer.|False

## get()
description|return value
---|---
Get processed chat data.|chat_components : List[dict]

## is_alive()
description|return value
---|---
Check if livechat stream is alive.|bool

## terminate()
description|return value
---|---
Terminate fetching livechat.|-


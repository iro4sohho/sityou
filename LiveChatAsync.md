# LiveChatAsync

LiveChatAsync object fetches chat data to buffer with aiohttp on asyncio context.

```
from pytchat import LiveChatAsync
chat = LiveChatAync("gb01h_eT0pw")
```
## #constructor params

name|type|required|remarks|default value
---|---|---|---|---
video_id|str|*|ID of youtube video.|-
processor|ChatPrcessor|||DefaultProcessor
buffer|Buffer||buffer of chat data fetched background|Buffer(maxsize=20)
interruptable|bool|||True
callback|func||function called from _listen()  periodically|None
done_callback|func||function called when listener ends.|None
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

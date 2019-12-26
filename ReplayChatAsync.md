ReplayChatAsync object 
+ fetches past chat data of archived videos and stores them in buffer with aiohttp on asyncio context.
+ responds to user inquiries of get().
+ invokes callback function with processed chat data.
+ can retrieve chat data disabled by editing video.

## Usage
```
from pytchat import ReplayChatAsync
chat = ReplayChatAsync("gb01h_eT0pw", seektime = 1000)
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


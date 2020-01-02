#### planning to integrate ReplayChatAsync into LiveChatAsync
LiveChatAsync object 
+ fetches chat data and stores them in buffer with aiohttp on asyncio context.
+ responds to user inquiries of get().
+ invokes callback function with processed chat data.

## Usage
```python
from pytchat import LiveChatAsync
import asyncio

async def main():
  chat = LiveChatAsync("G1w62uEMZ74", callback = func)
  while chat.is_alive():
    await asyncio.sleep(3)
    #other background operation.

#callback function is automatically called periodically.
async def func(data):
  for c in data.items:
    print(f"{c.datetime} [{c.author.name}]-{c.message} {c.amountString}")
    await data.tick_async()

loop = asyncio.get_event_loop()
loop.run_until_complete(main())

```
## #constructor params

name|type|required|remarks|default value
---|---|---|---|---
video_id|str|*|ID of youtube video.|-
processor|ChatPrcessor|||DefaultProcessor
buffer|Buffer||buffer of chat data fetched background.|Buffer(maxsize=20)
interruptable|bool|||True
callback|func||function called from _listen()  periodically.|None
done_callback|func||function called when listener ends.|None
exception_handler|func||function called when exceptions occur.|None
direct_mode|bool| |If True, invoke specified callback function without using buffer.|False

## await get()
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


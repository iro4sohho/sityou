LiveChatAsync object 
+ fetches chat data and stores them in buffer with aiohttp on asyncio context.
+ responds to user inquiries of get().
+ invokes a callback function with processed chat data.
+ can replay archived chat data (when the specified  video is not live broadcasting).
## Usage
```python
from pytchat import LiveChatAsync
import asyncio

async def main():
  livechat = LiveChatAsync("uIx8l2xlYVY", callback = func)
  while livechat.is_alive():
    await asyncio.sleep(3)
    #other background operation.

  # If you want to check the reason for the termination, 
  # you can use `raise_for_status()` function.
  try:
    livechat.raise_for_status()
  except pytchat.ChatDataFinished:
    print("Chat data finished.")
  except Exception as e:
    print(type(e), str(e))

#callback function is automatically called periodically.
async def func(chatdata):
  for c in chatdata.items:
    print(f"{c.datetime} [{c.author.name}]-{c.message} {c.amountString}")
    await chatdata.tick_async()


if __name__=='__main__':
  try:
    loop = asyncio.get_event_loop()
    loop.run_until_complete(main())
  except asyncio.exceptions.CancelledError:
    pass
```
## constructor params

name|type|required|remarks|default value
---|---|---|---|---
video_id|str|*|ID of youtube video, or youtube URL that includes ID.|-
processor|ChatPrcessor|||DefaultProcessor
buffer|Buffer||buffer of chat data fetched background.|Buffer(maxsize=20)
interruptable|bool||Allows keyboard interrupts. Set this parameter to False if your own threading program causes the problem.|True
callback|func||function called from _listen()  periodically.|None
done_callback|func||function called when listener ends.|None
exception_handler|func||function called when exceptions occur.|None
direct_mode|bool| |If True, invoke specified callback function without using buffer.|False
seektime|int| |~~start position of fetching chat (seconds). This option is valid for archived chat only. If negative value, fetches chatdata which is posted before start broadcasting.~~ **This parameter is not working well. We'll deal with it as soon as possible.** |0
force_replay|bool| |force to fetch archived chat data, even if specified video is live.|False
topchat_only|bool| |If True, get only top chat.|False
replay_continuation|str| |continuation parameter(archived chat only)|None

## continuation
The continuation parameter of recent chat data.<br>
This parameter can be used for retrieving chat data of any timing by specifying in the constructor as `replay_continuation`.<br>
(This parameter is valid only archived chat data.)


## await get()
description|return value
---|---
Get processed chat data from buffer.|processed chat data

## is_alive()
description|return value
---|---
Check if livechat stream is alive.|bool

## pause()
pause fetching chat (*callback mode only)


## resume()
resume fetching chat (*callback mode only)


## terminate()
Finish getting the chat.


## raise_for_status()
Raise internal excetion after is_alive()  becomes False.
By this function, you can check the reason for the termination.


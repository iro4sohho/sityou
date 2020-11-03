+ Simple non-buffered object for fetching live chat.

Get with `pytchat.create()` function.

### Example code
```python
import pytchat
import time

chat = pytchat.create(video_id="uIx8l2xlYVY")

while chat.is_alive():
    chatdata = chat.get()
    print(chatdata.json())
    time.sleep(5)

try:
   chat.raise_for_status()
except pytchat.ChatdataFinished:
   print("chat data finished")
except Exception as e:
   print(type(e), str(e))
```

## constructor params

name|type|required|remarks|default value
---|---|---|---|---
video_id|str|*|ID of youtube video, or youtube URL that includes ID.|-
processor|[ChatProcessor](https://github.com/taizan-hokuto/pytchat/wiki/ChatProcessor)|||[DefaultProcessor](https://github.com/taizan-hokuto/pytchat/wiki/DefaultProcessor)
interruptable|bool||Allows keyboard interrupts. Set this parameter to `False` if your own threading program causes the problem.|True
seektime|int| |start position of fetching chat (seconds). This option is valid for archived chat only. If negative value, fetches chatdata which is posted before start broadcasting.|0
force_replay|bool| |force to fetch archived chat data, even if specified video is live.|False
topchat_only|bool| |If True, get only top chat.|False
hold_exception|bool| |If True, when exceptions occur, the exception is held internally, and can be raised by raise_for_status().|True
[logger](https://github.com/taizan-hokuto/pytchat/wiki/Logging-pytchat)|logging.Logger| |any Logger object|internal logger(set NullHandler)

## get()
description|return value
---|---
Get processed chat data from buffer.|processed chat data

## is_alive()
description|return value
---|---
Check if livechat stream is alive.|bool

## is_replay()
description|return value
---|---
Check if replaying archived chat.|bool

## terminate()
description|return value
---|---
Terminate fetching chat.|-

## raise_for_status()
Raise internal exception after is_alive() becomes False.

By this function, you can check the reason for the termination.

*This function is valid only when `hold_exception` option is True.


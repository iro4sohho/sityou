+ Simple non-buffered object for fetching live chat.

Get with `pytchat.create()` function.

```
import pytchat
import time

chat = pytchat.create(video_id="Zvp1pJpie4I")

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

## #constructor params

name|type|required|remarks|default value
---|---|---|---|---
video_id|str|*|ID of youtube video, or youtube URL that includes ID.|-
processor|ChatProcessor|||DefaultProcessor
buffer|Buffer||buffer of chat data fetched background.|Buffer(maxsize=20)
interruptable|bool||Allows keyboard interrupts. Set this parameter to `False` if your own threading program causes the problem.|True
callback|func||function called periodically.|None
done_callback|func||function called when listener ends.|None
direct_mode|bool| |If True, invoke specified callback function without using buffer.|False
seektime|int| |start position of fetching chat (seconds). This option is valid for archived chat only. If negative value, fetches chatdata which is posted before start broadcasting.|0
force_replay|bool| |force to fetch archived chat data, even if specified video is live.|False
topchat_only|bool| |If True, get only top chat.|False
[logger](https://github.com/taizan-hokuto/pytchat/wiki/Logging-pytchat)|logging.Logger| |any Logger object|internal logger(set NullHandler)

## get()
description|return value
---|---
Get processed chat data from buffer.|processed chat data

*When callback parameter is set, get() function is not available. (Illegal function call occurs.)

## is_alive()
description|return value
---|---
Check if livechat stream is alive.|bool

## terminate()
description|return value
---|---
Terminate fetching livechat.|-

<br>
<br>


# LiveChat

livechat object.
```
from pytchat import LiveChat
chat = LiveChat("gb01h_eT0pw")
```
## constructor params

name|type|required|remarks|default value
---|---|---|---|---
video_id|str|*|ID of youtube video.|-
processor|ChatPrcessor|||DefaultProcessor
buffer|Buffer||buffer of chat data fetched background|Buffer(maxsize=20)
interruptable|bool|||True
callback|func||function called from _listen()  periodically|None
done_callback|func||function called when listener ends.|None
direct_mode|bool| |If True, invoke specified callback function without using buffer.|False

## functions

```
get()
```

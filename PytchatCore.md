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


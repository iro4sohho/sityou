JsonfileArchiver
+ saves chat data as text of JSON lines.

### Parameter

#### savefilepath : str

If a file with the same name exists, it is automatically saved under a different name.

### Return
actual saved file path.

### Usage
```python
import asyncio
from pytchat import LiveChatAsync

video_id = "8PIe_F9MI80"

async def main():
  chat = LiveChatAsync(　  
    video_id, 
    callback=func,
    processor =JsonfileArchiver("c:/temp/test.data")
  )
  while chat.is_alive():
    await asyncio.sleep(5)        
 
async def func(param):
  pass

loop = asyncio.get_event_loop()
try:
  loop.run_until_complete(async_def_callback())
except asyncio.CancelledError:
  print('Cancelled')
```
### Data Format
This processor saves chat data as lines of each chat data JSON.<br>
for example...

```
{"addChatItemAction": {"item": {"liveChatTextMessageRenderer": {"message": {"runs": [{"text": ...
{"addChatItemAction": {"item": {"liveChatPaidMessageRenderer": {"id": "xxx", "timestampUsec": ...
{"addChatItemAction": {"item": {"liveChatTextMessageRenderer": {"message": {"runs": [{"text": ...
```


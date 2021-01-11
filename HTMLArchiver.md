+ archives chat data as an HTML file, with embedded custom emojis.

## parameter
+ save_path : str

path for save file.

## sample code
+ archive live chat data
```python
import asyncio
from pytchat import HTMLArchiver, LiveChatAsync

video_id = "**********"
async def main():
    livechat = LiveChatAsync(video_id, processor=HTMLArchiver("v:/test.html"))
    while livechat.is_alive():
        await livechat.get()
        await asyncio.sleep(1)

asyncio.run(main())
```
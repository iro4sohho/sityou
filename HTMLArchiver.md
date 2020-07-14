+ archives chat data as an HTML file, with embedded custom emojis.

## parameter
+ save_path : str

path for save file.

## sample code 1
+ extract chat data from archived video.
```python
from pytchat import HTMLArchiver, Extractor

video_id = "*******"
ex = Extractor(
    video_id,
    div=10,
    processor=HTMLArchiver("c:/test.html")
)

ex.extract()
print("finished.")
```
## sample code 2
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
+ archives chat data as HTML file , with embedded custom emojis.

## parameter
+ save_path : str

path for save file.

## sample code
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
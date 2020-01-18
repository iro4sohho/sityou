コンストラクタの logger パラメータに、任意の [Logger](https://docs.python.org/ja/3/library/logging.html) オブジェクトをセットして<br>
pytchatのログ出力を取得することが可能です。<br>

configをインポートすることで、内部で使用している `config.logger` も利用可能です.<br>

```python
from pytchat import config
import logging
LiveChat(video_id = "xxxxxxxxxxx", 
                logger = config.logger(__name__, logging.DEBUG))
```

<br>

## コード例

```python
from pytchat import LiveChat, config
import logging

chat = LiveChat(video_id = "Zvp1pJpie4I", 
                logger = config.logger(__name__, logging.DEBUG))

while chat.is_alive():
  try:
    data = chat.get()
    items = data.items
    for c in items:
        print(f"{c.datetime} [{c.author.name}]- {c.message}")
        data.tick()
  except KeyboardInterrupt:
    chat.terminate()
    break
```


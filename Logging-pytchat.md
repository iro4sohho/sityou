## Logging example
By default, outputs of logger are all invisible.<br>

By setting logger parameter, you can use any customized logger.<br>

Internal logger `config.logger` is also available.

```python
from pytchat import LiveChat, config, logging
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


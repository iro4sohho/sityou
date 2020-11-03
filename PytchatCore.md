+ Simple non-buffered object for fetching live chat.

Get with `pytchat.create()` function.

```
import pytchat

chat = pytchat.create(video_id="Zvp1pJpie4I")

while chat.is_alive():
    for c in chat.get().sync_items():
        print(f"{c.datetime} [{c.author.name}]- {c.message}")
```

## create()
Returns PytchatCore object.
+ the chat processor compatible with the structures that YT API returns.

### Example Code

```python
from pytchat import LiveChat, CompatibleProcessor
import time

chat = LiveChat("uIx8l2xlYVY", 
  processor = CompatibleProcessor() )

while chat.is_alive():
  try:
    data = chat.get()
    polling = data['pollingIntervalMillis']/1000
    for c in data['items']:
      if c.get('snippet'):
        print(f"[{c['authorDetails']['displayName']}]"
              f"-{c['snippet']['displayMessage']}")
        time.sleep(polling/len(data['items']))
  except KeyboardInterrupt:
    chat.terminate()
```
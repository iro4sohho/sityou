## SuperchatCalculator
+ aggregates the amount of Superchat for each currency.

### Returns
dict<br> { currency_symbol : amount }<br>
e.g.
`{'￥': 170000.0, '$': 115.0, 'SEK\xa0': 90.0, 'PHP\xa0': 100.0, 'NT$': 30.0, 'R$': 5.0}`
### Example
```python
'''Display the total result up to that point 
   at regular intervals.
   video_id can be both live and archived.'''
import asyncio
from concurrent.futures import CancelledError
from pytchat import (LiveChatAsync, 
     DefaultProcessor, SuperchatCalculator)

video_id = "_i_AxXSfceM"

async def main():
    chat = LiveChatAsync(video_id, callback = display,
           processor = DefaultProcessor(), SuperchatCalculator() )
    while chat.is_alive():
        await asyncio.sleep(3)        
 
async def display(data, amount):
    print(data.items[-1].elapsedTime, amount)

if __name__ =='__main__':
    loop = asyncio.get_event_loop()
    try:
        loop.run_until_complete(main())
    except asyncio.CancelledError:
        pass
```


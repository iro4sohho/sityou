## SuperchatCalculator
+ aggregates the amount of Superchat for each currency.

### Returns
dict<br> { currency_symbol : amount }<br>
e.g.
`{'￥': 170000.0, '$': 115.0, 'SEK\xa0': 90.0, 'PHP\xa0': 100.0, 'NT$': 30.0, 'R$': 5.0}`
### Example 1
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

### Example 2
Aggregate the total amount of superchat for each currency. (using Extractor)<br>
Requires tqdm to display the progress bar. (`pip install tqdm`)
<br>
`pip install tqdm`
<br>
```python
from tqdm import tqdm
from pytchat import Extractor, VideoInfo, SuperchatCalculator
import signal

class ProgressBar:
    def __init__(self,total):
        self.total = total*1000
        self.pbar = tqdm(total = self.total, ncols = 80, unit_scale = 1,
            bar_format='{desc}{percentage:3.1f}%|{bar}|'
                       '[{n_fmt:>7}/{total_fmt}]{elapsed}<{remaining}')
        
    def callback(self, actions, fetched):
        if self.total - fetched < 0:
            fetched = self.total
        self.total -= fetched
        self.pbar.update(fetched)
    
    def close(self):
        self.pbar.update(self.total)
        self.pbar.close()
    
    def cancel(self):
        self.pbar.close()

if __name__ == '__main__':
    video_id = "GY-LSsYVpJ4"
    info  = VideoInfo(video_id)
    print('Calculate Superchat: [title] ', info.get_title())    

    pbar = ProgressBar(info.get_duration())
 
    ex = Extractor(
        video_id,
        callback = pbar.callback,
        div = 10,
        processor = SuperchatCalculator()
    )

    #Cancel handler
    signal.signal(signal.SIGINT,  
        (lambda a, b: ex.cancel()))

    #execute extraction
    result = ex.extract()

    #display results
    pbar.close()
    print(result)

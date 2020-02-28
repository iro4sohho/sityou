## Extractor object<br>
+ extracts chat data.

By specifying any ChatProcessor at processor parameter, you can process chat data after extraction.

*Due to YouTube specifications, not all chat data can be extracted. <br> (Omission may occur for some videos with high chat speed) <br> Also, the chat data fetched may change depending on the number of divisions specified `div` parameter.

## Parameters
### video_id : str
video id

### div : int
the number of divisions to download concurrently.<br>
From 1 to 10.<br>
Default value: 1.<br>



### callback : function
A function passed the progress data during download. <br>
The chat data and the number of seconds (milliseconds) are passed. <br>
However, the number of seconds and chat data passed to callback function may overlap.

### processor
[ChatProcessor](https://github.com/taizan-hokuto/pytchat/wiki/ChatProcessor) to process chat data after extracting.

## functions
### extract()
Start to extract.

### cancel()
Cancell the process.



## Usage
Aggregate the total amount of supoerchat.(processor : SuperchatCalculator)<br>
Install tqdm to display progress bar.<br>
`pip install tqbm`



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
    print(info.get_title())    

    pbar = ProgressBar(info.get_duration())
 
    ex = Extractor(
        video_id,
        callback = pbar.callback,
        div = 10,
        processor = SuperchatCalculator()
    )

    signal.signal(signal.SIGINT,  
        (lambda a, b: ex.cancel()))

    result = ex.extract()
    pbar.close()

    print(result)
```
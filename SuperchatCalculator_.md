## SuperchatCalculator
チャットデータ中のスパチャ合計額（スーパーステッカー含む）を通貨ごとに集計します。

### 戻り値
{ 通貨シンボル:金額 }の辞書<br>
例：
`{'￥': 170000.0, '$': 115.0, 'SEK\xa0': 90.0, 'PHP\xa0': 100.0, 'NT$': 30.0, 'R$': 5.0}`
### コード例１
```python
'''一定間隔でその時点までの集計結果を表示。
video_idはライブ中／アーカイブ済み両方可。'''
import asyncio
from concurrent.futures import CancelledError
from pytchat import (LiveChatAsync, 
     DefaultProcessor, SuperchatCalculator)

video_id = "_i_AxXSfceM"

async def main():
    chat = LiveChatAsync(video_id, callback = display,
           processor = (DefaultProcessor(), SuperchatCalculator()) )
    while chat.is_alive():
        await asyncio.sleep(3)        
 
async def display(data, amount):
    if len(data.items) > 0:
        print(data.items[-1].elapsedTime, amount)

if __name__ =='__main__':
    loop = asyncio.get_event_loop()
    try:
        loop.run_until_complete(main())
    except asyncio.CancelledError:
        pass
```

### コード例２
指定した動画IDのスパチャ合計額を集計表示する。(processor に SuperchatCalculatorを指定)<br>
プログレスバー表示のため別途tqdmのインストールが必要。<br>
`pip install tqdm`

```python
from tqdm import tqdm
from pytchat import Extractor, VideoInfo, SuperchatCalculator
import signal

'''
進捗状況を表すプログレスバー
'''
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

    # プログレスバーを用意する。
    pbar = ProgressBar(info.get_duration())
 
    # Extractorの生成
    ex = Extractor(
        video_id,
        callback = pbar.callback,
        div = 10,
        processor = SuperchatCalculator()
    )

    #Ctrl+Cでキャンセルする
    signal.signal(signal.SIGINT,  
        (lambda a, b: ex.cancel()))

    #抽出の実行
    result = ex.extract()

    #集計結果の表示
    pbar.close()
    print(result)

## SuperchatCalculator
チャットデータ中のスパチャ合計額（スーパーステッカー含む）を通貨ごとに集計します。

### 戻り値
{ 通貨シンボル:金額 }の辞書<br>
例：
`{'￥': 170000.0, '$': 115.0, 'SEK\xa0': 90.0, 'PHP\xa0': 100.0, 'NT$': 30.0, 'R$': 5.0}`
### コード例
```python
'''一定間隔でこのコードの実行開始時点以降の集計結果を表示。
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


## SuperchatCalculator
チャットデータ中のスパチャ合計額（スーパーステッカー含む）を通貨ごとに集計します。

### 戻り値
{キー：通貨シンボル、値：金額 }の辞書

### コード例
```
'''一定間隔で集計結果を表示。'''
import asyncio
from concurrent.futures import CancelledError
from pytchat import LiveChatAsync, SuperchatCalculator
video_id = "_i_AxXSfceM"
async def main():
    chat = LiveChatAsync(video_id, callback = display,
           processor = SuperchatCalculator())
    while chat.is_alive():
        await asyncio.sleep(3)        
 
async def display(amount):
    print(amount)

if __name__ =='__main__':
    loop = asyncio.get_event_loop()
    try:
        loop.run_until_complete(main())
    except asyncio.CancelledError:
        pass
```

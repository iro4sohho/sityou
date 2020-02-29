Extractorは、チャットデータを一括抽出するためのオブジェクトです。<br>

processorパラメータに任意の[ChatProcessor]を指定することで、取得後のチャットデータを加工できます。<br><br>



※YouTubeの仕様上、必ずしもブラウザの任意の地点で表示されるすべてのチャットデータを抽出できるとは限りません。<br>（チャットの流れが速い部分では取得漏れが生じることがあります）<br>


## パラメータ
### video_id
動画ID

### div
同時分割並行ダウンロードのための分割数。<br>
（1～10の整数。10を超える数を指定した場合であっても10で処理されます。）

### callback (省略可)
ダウンロード中の途中経過データを渡す関数。<br>
読み込んだチャットデータと、読み込んだチャットデータの秒数（ミリ秒）が渡されます。<br>
ただし、callbackに渡される秒数およびチャットデータは一部重複する可能性があります。

### processor (省略可)
抽出後の後処理を行う[ChatProcessor](https://github.com/taizan-hokuto/pytchat/wiki/ChatProcessor)<br>


## 関数
### extract()
抽出を開始します。
<br>
#### 戻り値
processorにChatProcessorを指定する場合：ChatProcessorによって加工されたデータ<br>
processorを指定しない場合：生のチャットデータ（actions）<br>
<br>

### cancel()
処理をキャンセルします。


## Extractorの使用例
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
```
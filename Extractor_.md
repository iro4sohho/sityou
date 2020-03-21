Extractorは、チャットデータを抽出するためのオブジェクトです。<br>

processorパラメータに任意の[ChatProcessor](https://github.com/taizan-hokuto/pytchat/wiki/ChatProcessor)を指定することで、取得後のチャットデータを加工できます。<br><br>



※YouTubeの仕様上、必ずしも投稿されたすべてのチャットデータを抽出できるとは限りません。<br>（pytchatブラウザは一般的なブラウザ上で表示できるチャットデータは原則すべて取得していますが、<br>一般的なブラウザで表示されるアーカイブのチャットは、ライブ配信時に表示されていたチャットデータの一部を取得していない場合があります。<br>（「すべてのチャット」に切り替えていても同様）<br>ライブ当時のチャットの流れが速い部分ではアーカイブ後にYouTubeが返すチャットデータに欠落が生じている場合があり、pytchatのextractorで取得できるデータはこれに準じます。<br>
<br>


## パラメータ
### video_id
動画ID

### div
同時分割並行ダウンロードのための分割数。<br>
（1～10の整数。10を超える数を指定した場合であっても10で処理されます。）

### callback (省略可)
ダウンロード中の途中経過データを渡す関数。<br>
読み込んだチャットデータと、読み込んだチャットデータの秒数（ミリ秒）が渡されます。<br>
ただし、callbackに渡される秒数およびチャットデータは一部重複する可能性があります。<br>
このため、callbackから渡されるデータはダウンロードの進捗状況を把握するためだけに利用することを推奨します。<br>


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
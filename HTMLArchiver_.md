## 概要

チャットデータをHTMLテーブルとして保存します。

## 使用法

LiveChat / LiveChatAsync / Extractor のprocessor パラメータにHTMLArchiver()を指定します。

## パラメータ
```
save_path : ファイルの保存パス
```
ファイル名が重複する場合は、ファイル名の末尾（拡張子の前）に連番を付与します。

## サンプルコード
アーカイブ済みの動画からチャットデータを抽出し、HTMLファイルとして保存します。<br>

```python
from pytchat import Extractor, VideoInfo, HTMLArchiver
from pytchat.exceptions import InvalidVideoIdException

import signal, os

def disp(*args):
    print('.', end="",flush=True)

if __name__ == '__main__':
    video_id = "U5YrJlOjDj"
    save_path = "test.html"
    archiver = HTMLArchiver(save_path)

    try:
        # Extractorの生成
        ex = Extractor(
            video_id,
            div = 10,
            callback = disp,
            processor = archiver
        )
    except InvalidVideoIdException:
        print(f"動画ID[{video_id}]は無効です")
        exit(0) 

    #Ctrl+Cでキャンセルする
    signal.signal(signal.SIGINT,  
        (lambda a, b: ex.cancel()))

    #抽出の開始
    info = VideoInfo(video_id)
    if info.get_duration() == 0:
        print("指定した動画はアーカイブされていないか、チャットデータが存在しません")
        exit(0)
    print("Extracting: "+info.get_title())
    print('Save path: ',
        os.path.realpath(save_path)[:-len(os.path.basename(save_path))] + 
        os.path.basename(archiver.save_path))
    result = ex.extract()

    #抽出完了
    print("\nFinished extraction.")
```
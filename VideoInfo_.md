VideoInfo は動画ページから動画情報を取得するためのオブジェクトです。

## コード例
```python
info  = VideoInfo(video_id = "fzI9FNjXQ0o")

print("title:", info.get_title())
print("channel", info.get_channel_name())
print("duration", info.get_duration())

# 出力結果
#> GitHub Arctic Code Vault
#> GitHub
#> 147

```

## パラメータ
video_id : str<br>
動画ID<br><br>

## 例外
### InvalidVideoIdException :
動画IDが存在しない場合に発生します。<br><br>

## 関数
#### get_duration() : int
動画の長さ。<br>動画がライブもしくは待ち受け中の場合は0。<br>durationが存在しない場合None。<br><br>

#### get_title() : str
動画のタイトル。<br>

#### get_channel_id() : str
チャンネルID。<br>

#### get_author_image() : str
配信者のアイコン画像URL。<br>

#### get_thumbnail : str
動画のサムネイルURL。<br>

#### get_channel_name : str
配信チャンネルのチャンネル名。<br>

#### get_moving_thumbnail : str (*)<br>
動画のwebmサムネイルURL。


VideoInfo object retrieves YouTube video informations from the video page.

## Usage
```python
info  = VideoInfo(video_id = "fzI9FNjXQ0o")

print("title:", info.get_title())
print("channel", info.get_channel_name())
print("duration", info.get_duration())

#> GitHub Arctic Code Vault
#> GitHub
#> 147

```

## Parameter
video_id : str

##Exception
### InvalidVideoIdException :
Occurs when video_id does not exist on YouTube.

## Functions
get_duration() : int

get_title() : str

get_channel_id() : str

get_author_image() : str (*)

get_thumbnail : str (*)

get_channel_name : str

get_moving_thumbnail : str (*)

*as image url

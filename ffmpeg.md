## converts most without need to specify formats
```
ffmpeg -i iput.VOB output.mp4
ffmpeg -i iput.m4b output.mp3
```
## split by timestamp
```
ffmpeg -ss 00:00:00 -t 00:50:00 -i largefile.mp4 -acodec copy \-vcodec copy smallfile.mp4
```

## crop pixels

top and bottom
```
ffmpeg -i input.mp4 -filter:v "crop=iw:ih-200" output.mp4
```


## add subs from file

```
ffmpeg -i "imput.mp4" -lavfi "subtitles=subtitles.srt:force_style='Alignment=0,OutlineColour=&H100000000,BorderStyle=3,Outline=1,Shadow=0,Fontsize=18,MarginL=5,MarginV=25'" -crf 1 -c:a copy "output.mp4"


ffmpeg -y -i "input.mp4" -vf "subtitles=subtitles.srt:fontsdir=fonts:force_style='Fontname=Arturo Trial,Fontsize=10'" output.mp4

```




## add audio with volume


```
ffmpeg -i video.mp4 -filter_complex "amovie=audio.mp3:loop=0,asetpts=N/SR/TB,volume=0.2[audio];[0:a]volume=3[sa];[sa][audio]amix[fa]" -map 0:v -map [fa] -vcodec libx264 -preset ultrafast -shortest output.mp4
```

## concat
```
(for %i in (*.mp4) do @echo file '%i') > mylist.txt  &&  ffmpeg -f concat -i mylist.txt -c copy output.mp4 
```

# yt-dl clip from stream
```
Use youtube-dl --youtube-skip-dash-manifest -g "URL" to get the video and audio streams.

Now use:

ffmpeg -ss 12:15 -i "1st-URL" -ss 12:15 -i "2nd-URL" -t 5:15 -map 0:v -map 1:a -c:v libx264 -c:a aac output.mkv

```


## Crop 16:9 to 9:16
```
 ffmpeg -i input.mkv -filter:v "crop=9/16*ih:ih" output33.mp4
```

## letterbox pad for 9:16
```
ffmpeg -i input.mkv -vf "pad=iw:2*trunc(iw*16/18):(ow-iw)/2:(oh-ih)/2,setsar=1" -c:a copy output_letterbox.mp4
```

### rotate,  res++
```
ffmpeg -i input.mov  -r 30 -b:v 50000k -vf "transpose=dir=2" output.mp4

```


### speed
```
ffmpeg -i input.mp4 -filter:v "setpts=0.5*PTS" faster.mp4

ffmpeg -i input.mp4 -filter:v setpts=2.0*PTS slower.mp4
```


### compress 
```
ffmpeg -i input.mp4 -vcodec libx264 -crf 24 output.mp4
```

### scale down 1/3
```
ffmpeg -i input.mp4 -vf "scale=iw/3:ih/3" output.mp4
```

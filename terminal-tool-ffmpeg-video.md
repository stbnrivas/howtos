-formats   print the list of supported file formats
-codecs    print the list of supported codecs (E=encode,D=decode)
-i         set the input file. Multiple -i switchs can be used
-f         set video format (for the input if before of -i, for output otherwise)
-an        ignore audio
-vn        ignore video
-ar        set audio rate (in Hz)
-ac        set the number of channels
-ab        set audio bitrate
-acodec    choose audio codec or use “copy” to bypass audio encoding
-vcodec    choose video codec or use “copy” to bypass video encoding
-r         video fps. You can also use fractional values like 30000/1001 instead of 29.97
-s         frame size (w x h, ie: 320x240)
-aspect    set the aspect ratio i.e: 4:3 or 16:9
-sameq     ffmpeg tries to keep the visual quality of the input
-t N       encode only N seconds of video (you can use also the hh:mm:ss.ddd format)
-croptop, -cropleft, -cropright, -cropbottom   crop input video frame on each side
-y         automatic overwrite of the output file
-ss        select the starting time in the source file
-vol       change the volume of the audio
-g         Gop size (distance between keyframes)
-b         Video bitrate
-bt        Video bitrate tolerance
-metadata  add a key=value metadata


########################################################################


ffmpeg -formats

ffmpeg -i input.file
ffprobe videofile

# conversion to webm in two pass

ffmpeg -i input.mp4 -s 1280x720 -vpre libvpx-720p -b 3900k -pass 1 -an -f webm -y output.webm

ffmpeg -i input.mp4 -s 1280x720 -vpre libvpx-720p -b 3900k -pass 2 -acodec libvorbis -ab 100k -f webm -y output.webm

# conversion to mp4 in two pass

ffmpeg -i input -pass 1 -s 1280x720 -vcodec mpeg4 -vtag XVID -b 500k -mbd rd -flags +4mv+trell+aic -cmp 2 -subcmp 2 -g 300 -acodec copy video2.mp4
ffmpeg -i input -pass 2 -s 1280x720 -vcodec mpeg4 -vtag XVID -b 500k -mbd rd -flags +4mv+trell+aic -cmp 2 -subcmp 2 -g 300 -acodec mp3 -ab 128 -ac 2 -async 1 D2-video1

	ffmpeg -i i.avi out-file.mp4 -pass 1
	ffmpeg -i i.avi out-file.mp4 -pass 2

# another way

	ffmpeg -i input-file.avi out-file.webm

# change resolution
	ffmpeg -i input.file -s 1024x768 output.file


# crop video

	ffmpeg -i input.file -vf crop:width:height:x:y

	Crop the input video to out_w:out_h:x:y:keep_aspect


# Turn X images to a video sequence

ffmpeg -f image2 -i image%d.jpg video.mpg

# Turn a video to X images

ffmpeg -i video.mpg image%d.jpg


# Encode a video sequence for the iPpod/iPhone
ffmpeg -i source_video.avi input -acodec aac -ab 128kb -vcodec mpeg4 -b 1200kb -mbd 2 -flags +4mv+trell -aic 2 -cmp 2 -subcmp 2 -s 320x180 -title X final_video.mp4



# corta a partir del segundo 3 solo 8 segundos
######################################################3
ffmpeg -i movie.mp4 -ss 00:00:03 -t 00:00:08 -async 1 -strict -2 cut.mp4



# cut video at second

ffmpeg -ss 00:00:30.0 -t 00:00:10.0 -i input.wmv -acodec copy -vcodec copy -async 1 output.wmv

ffmpeg -ss 00:00:00.0 -t 00:00:39.0 -i input.mov -acodec copy -vcodec copy -async 1 output.mov

ffmpeg -i INPUT.wav -ss 00:10:00 -t 00:05:00 -acodec copy OUTPUT.wav





# corta 1 minuto comenzando por el segundo 0
ffmpeg -i source.mp3 -acodec copy -t 00:01:00 -ss 00:00:00 target.mp3

$ ffmpeg -i miMp3.mp3 -t 11 mis11segundos.mp3

# corta 40 segundos despues del primer minuto
ffmpeg -i source.mp3 -acodec copy -t 00:40:00 -ss 00:01:00 target.mp3

# -t 1500 processes the first 1500 seconds (25 min * 60 sec/min)
# -acodec copy and -vcodec copy copy the codec data without transcoding (which would incur quality loss).
ffmpeg -i 40minvideo.mp4 -t 1500 -acodec copy -vcodec copy 25minvideo.mp4


ffmpeg -i source.m4v -ss 0 -t 593.3 -vcodec copy -acodec copy part1.m4v



# remove audio
ffmpeg -i input -o output -an
ffmpeg -i <input_file> -vcodec copy -an <output_file>



# extract audio

ffmpeg -i filename.mp4 filename.mp3

# add new audio, discard old

ffmpeg -i video.avi -i audio.mp3 -map 0 -map 1 -codec copy -shortest output_video.avi

ffmpeg -i video.mp4 -i audio.aac -map 0:0 -map 1:0 -vcodec copy -acodec copy newvideo.mp4



# convert input.dav output.mp4

```
ffmpeg -y -i HCVR_fileinput.dav -vcodec libx264 -crf 24 -filter:v "setpts=1*PTS" ouptput.mp4

# to do video more slowly

ffmpeg -y -i HCVR_fileinput.dav -vcodec libx264 -crf 24 -filter:v "setpts=3*PTS" ouptput.mp4
```

# concat or append video

```
ffmpeg -i concat:"intermediate1.mpg|intermediate2.mpg" -c copy intermediate_all.mpg

ffmpeg -i concat:"DSC_0001.MOV|DSC_0002.MOV|DSC_0003.MOV" -c copy merged.mov


ffmpeg -safe 0 -f concat -i files_to_combine -vcodec copy -acodec aac -strict -2 -b:a 384k merged.mp4
```


```
ffmpeg -f concat -safe 0 -i list.txt -c copy output.mov
```





# Join video & audio 
 
ffmpeg -i ..\..\01-presentation.avi -i es-01-presentation.mp3 -map 0:0 -map 1:0 -c:v copy -c:a copy es-01-presentation.avi
 
Resincronizar audio: ffmpeg -i produced.mp4 -itsoffset 0.3 -i produced.mp4  -vcodec copy -acodec copy -map 0:0 -map 1:1 synced.mp4


# audio optimice only for voice

echo off
mkdir optimized
for %%x in (.\*.mp3) do (
   ffmpeg -i %%x -ac 1 -ab 24000 -ar 22050  optimized\%%x
)
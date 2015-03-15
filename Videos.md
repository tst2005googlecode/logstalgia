## Recording Videos ##

### General ###

You can create a video of Logstalgia using the `--output-ppm-stream` option. This creates an uncompressed sequence of screenshots in PPM format which can then be processed a video encoder (such as ffmpeg) to produce a video.

You can also adjust the output frame rate with `--output-framerate`. Note you will need to adjust the frame rate used by the encoder (eg ffmpeg -r) to match, unless you are going for a speed-up timelapse or slow motion effect.

Make sure you keep the window of Logstalgia entirely visible while recording. If you minimize or partially obscure the window, your video card may decide not draw the output consistently and you will get artifacts in your recording. You may like to use the `-f` option to run in full-screen mode to stop this happening.

You may want to record your video in widescreen as that is the trend for online video now days. You can record in 720p by adding -1280x720 to the command line.

Given the nature of the data in access logs, please consider the implications before posting any videos online and make appropriate redactions.

### Linux / Mac ###

## FFmpeg using x264 codec ##

The below command lines will create a video at 60fps using the [x264](http://en.wikipedia.org/wiki/X264) codec in an mp4 container.

This assumes you have recent version of ffmpeg **with libx264 support**. Some distributions like Ubuntu do not enable libx264 support by default in ffmpeg (See [this thread](http://ubuntuforums.org/showthread.php?t=1117283) for various ways to [enable libx264 support on Ubuntu](http://ubuntuforums.org/showthread.php?t=1117283)). Consult guides for your distribution if this is the case.

In one command (raw video piped directly into ffmpeg):

```
logstalgia -1280x720 --output-ppm-stream - | ffmpeg -y -r 60 -f image2pipe -vcodec ppm -i - -vcodec libx264 -preset ultrafast -pix_fmt yuv420p -crf 1 -threads 0 -bf 0 logstalgia.mp4
```

As two commands:

```
logstalgia -1280x720 --output-ppm-stream logstalgia.ppm
ffmpeg -y -r 60 -f image2pipe -vcodec ppm -i logstalgia.ppm -vcodec libx264 -preset ultrafast -pix_fmt yuv420p -crf 1 -threads 0 -bf 0 logstalgia.mp4
```

This one has the advantage of keeping the raw video file (logstalgia.ppm) so you can go back and tweak the encoding parameters if you don't like the output quality or need a different video format without recording the video again. The disadvantage is that this raw uncompressed video and you can expect it to use up 100gs of gigs, so keep that in mind!

You can interchange the extension 'mp4' with 'mkv' or 'avi' to get ffmpeg to use a different container format for the video. 'avi' is typically discouraged for long videos as there is a 2GB file limit associated with that format.

**Note**: **ffmpeg seems to be a constantly moving target**, so you may find you need slightly different arguments with your version. There is a good guide to using x264 with ffmpeg [here](https://wiki.archlinux.org/index.php/FFmpeg).

## FFmpeg using WebM codec ##

A good alternative codec to x264 is [WebM](http://en.wikipedia.org/wiki/WebM). Below is a very basic command line example of using ffmpeg to produce a Logstalgia WebM video:

```
logstalgia -1280x720 --output-ppm-stream - | ffmpeg -y -r 60 -f image2pipe -vcodec ppm -i - -vcodec libvpx -b 10000K logstalgia.webm
```

### Windows ###

On Windows if you aren't too fussed about the precision of the output, you might want to try a direct video capture program like [Fraps](http://www.fraps.com). Fraps works with any program that uses OpenGL or Direct3D and is pretty fast (you can capture Logstalgia at 60fps with no slow down in many cases).

If you don't want to use an external capture program, here is an example command-line using the built in PPM frame capture support, using ffmpeg to generate a video:

```
logstalgia -1280x720 --output-ppm-stream logstalgia.ppm
C:\\ffmpeg\\bin\\ffmpeg -y -r 60 -f image2pipe -vcodec ppm -i logstalgia.ppm -vcodec libx264 -preset ultrafast -pix_fmt yuv420p -crf 1 -threads 0 -bf 0 logstalgia.x264.avi
```

You can interchange the extension 'avi' with 'mp4' or 'mkv' to get ffmpeg to use a different container format for the video. 'avi' is typically discouraged for long videos as there is a 2GB file limit associated with that format.

You can get an `ffmpeg` build for Windows from [here](http://ffmpeg.zeranoe.com/).

**Note**: **ffmpeg seems to be a constantly moving target**, so you may find you need slightly different arguments with your version. There is a good guide to using x264 with ffmpeg [here](https://wiki.archlinux.org/index.php/FFmpeg).
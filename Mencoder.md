---
title: Mencoder
layout: default
---

mpeg4 lavc 3 pass;

    mencoder dvd://1 -aid 128 -oac mp3lame -lameopts br=96:cbr:vol=6 -ovc frameno -o frameno.avi
    mencoder dvd://1 -sws 2 -oac copy -ovc lavc -lavcopts vcodec=mpeg4:vhq:vbitrate=629:vpass=1\
     -vf crop=720:346:0:154,scale=704:304 -o Matrix.avi
    mencoder dvd://1 -sws 2 -oac copy -ovc lavc -lavcopts vcodec=mpeg4:vhq:vbitrate=629:vpass=2 \
     -vf crop=720:346:0:154,scale=704:304 -o Matrix.avi

mpeg4 lavc;

    mencoder dvd://1 -ovc lavc -lavcopts vcodec=mpeg4:vhq:vbitrate="1200" \
    -vop scale -zoom -xy 640 -oac mp3lame -lameopts br=128 -o dvd.avi

LibAVC / XviD / x264 Examples

    mencoder dvd:// -aid 128 -o dvd.avi \
    -oac mp3lame -lameopts br=128:cbr \
    #-oac faac -faacopts br=64
    -vf crop=720:352:0:66 \
    #-ovc lavc -lavcopts vcodec=mpeg4:vhq:vbitrate=650:vpass=1:threads=2
    #-ovc xvid -xvidencopts bitrate=1200:vhq=4:bvhq=1:pass=1:threads=2:trellis:hq_ac
    #-ovc x264 -x264encopts bitrate=1200:pass=1:threads=2

PS3 WORKING --- H.264/MPEG-4 AVC + FAAC --- need to run MP4Box to
convert

    mencoder dvd:// -aid 128 -o dvd.avi \
    -oac faac -faacopts br=64 \
    -vf crop=720:352:0:66 \
    -ovc x264 -x264encopts subq=6:bitrate=2000:bframes=3:partitions=p8x8,b8x8,i4x4:weight_b:threads=auto:nopsnr:nossim:frameref=3:mixed_refs:bime:brdo:level_idc=41:direct_pred=auto:trellis=1:threads=2

    MP4Box -aviraw video dvd.avi
    MP4Box -aviraw audio dvd.avi
    mv dvd_audio.raw dvd_audio.aac
    MP4Box -add dvd_audio.aac -add dvd_video.h264 dvd.mp4

OR??

    ffmpeg -y -i [input.mov] -sameq -acodec libfaac -ac 2 -ab 128 -vcodec mpeg4 -r 24 -b 800k -level 41 -mbd 2 -aic 2 [output.mp4]

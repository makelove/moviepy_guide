## GitHub: https://github.com/makelove/moviepy_guide
- moviepy+Jupiter ,支持中文字幕 https://hub.docker.com/r/play4fun/moviepy_chinese_font

- 下载
    - docker pull play4fun/moviepy_chinese_font

- 运行
    - cd 到某目录
    - ``docker run -it  -v `pwd`:/test -p 8888:8888 play4fun/moviepy_chinese_font:latest``
- 在docker内执行
    - cd /test
    - jupyter-lab --no-browser --ip=0.0.0.0  --allow-root
- 打开浏览器 http://127.0.0.1:8888/lab
    - 新建notebook
- 测试代码

```python
from moviepy.editor import TextClip

TextClip.list('font')

x='Microsoft-YaHei'
txt='欢迎光临本店welcome-#$&*#🌈🚲🎼'
tc=TextClip(txt, font=x, fontsize=16, color='red')
tc.save_frame(x+'.png')
```
- 建议购买个服务器，在服务器运行
    - 只需打开浏览器 http://服务器IP:8888/lab
    - 就能使用moviepy了，非常方便

- 版本 version
    - Ubuntu 19.04

- Python 3.7.3
- pip 18.1

```
ipython==7.11.1
jupyterlab==1.2.4
notebook==6.0.2
numpy==1.18.1

moviepy==1.0.0
imageio==2.6.1
imageio-ffmpeg==0.3.0

youtube-dl==2020.1.1
Pillow==7.0.0
srt==3.0.0
```

- ffmpeg +ImageMagick

```
root@8787e8690261:/# ffmpeg -version
ffmpeg version 4.1.3-0ubuntu1 Copyright (c) 2000-2019 the FFmpeg developers
built with gcc 8 (Ubuntu 8.3.0-6ubuntu1)
configuration: --prefix=/usr --extra-version=0ubuntu1 --toolchain=hardened --libdir=/usr/lib/x86_64-linux-gnu --incdir=/usr/include/x86_64-linux-gnu --arch=amd64 --enable-gpl --disable-stripping --enable-avresample --disable-filter=resample --enable-avisynth --enable-gnutls --enable-ladspa --enable-libaom --enable-libass --enable-libbluray --enable-libbs2b --enable-libcaca --enable-libcdio --enable-libcodec2 --enable-libflite --enable-libfontconfig --enable-libfreetype --enable-libfribidi --enable-libgme --enable-libgsm --enable-libjack --enable-libmp3lame --enable-libmysofa --enable-libopenjpeg --enable-libopenmpt --enable-libopus --enable-libpulse --enable-librsvg --enable-librubberband --enable-libshine --enable-libsnappy --enable-libsoxr --enable-libspeex --enable-libssh --enable-libtheora --enable-libtwolame --enable-libvidstab --enable-libvorbis --enable-libvpx --enable-libwavpack --enable-libwebp --enable-libx265 --enable-libxml2 --enable-libxvid --enable-libzmq --enable-libzvbi --enable-lv2 --enable-omx --enable-openal --enable-opengl --enable-sdl2 --enable-libdc1394 --enable-libdrm --enable-libiec61883 --enable-chromaprint --enable-frei0r --enable-libx264 --enable-shared
libavutil      56. 22.100 / 56. 22.100
libavcodec     58. 35.100 / 58. 35.100
libavformat    58. 20.100 / 58. 20.100
libavdevice    58.  5.100 / 58.  5.100
libavfilter     7. 40.101 /  7. 40.101
libavresample   4.  0.  0 /  4.  0.  0
libswscale      5.  3.100 /  5.  3.100
libswresample   3.  3.100 /  3.  3.100
libpostproc    55.  3.100 / 55.  3.100

root@8787e8690261:/# convert -version
Version: ImageMagick 6.9.10-14 Q16 x86_64 20181023 https://imagemagick.org
Copyright: © 1999-2018 ImageMagick Studio LLC
License: https://imagemagick.org/script/license.php
Features: Cipher DPC Modules OpenMP
Delegates (built-in): bzlib djvu fftw fontconfig freetype jbig jng jpeg lcms lqr ltdl lzma openexr pangocairo png tiff wmf x xml zlib
```

## 报错
```
root@43ffc12d6d7d:/# ipython
Python 3.6.9 (default, Nov  7 2019, 10:44:02)
Type 'copyright', 'credits' or 'license' for more information
IPython 7.11.1 -- An enhanced Interactive Python. Type '?' for help.

In [1]: from moviepy.editor import TextClip
/usr/bin/python3: Relink `/usr/local/lib/python3.6/dist-packages/PIL/.libs/./liblzma-6cd627ed.so.5.2.4' with `/lib/x86_64-linux-gnu/librt.so.1' for IFUNC symbol `clock_gettime'
Segmentation fault (core dumped)
```

- 原因 OpenCV
- 解决 删除 pip3 uninstall opencv-contrib-python
- 可以安装 pip3 install  opencv-contrib-python-headless==4.1.2.30

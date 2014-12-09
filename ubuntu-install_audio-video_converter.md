# How to get a cool and customisable audio and video converter
1. Go to [the ffmpeg doc](http://trac.ffmpeg.org/wiki/CompilationGuide/Ubuntu) for more informations
2. Update your system and install dependencies
```
sudo apt-get update
sudo apt-get -y install autoconf automake build-essential libass-dev libfreetype6-dev libgpac-dev libsdl1.2-dev libtheora-dev libtool libva-dev libvdpau-dev libvorbis-dev libx11-dev libxext-dev libxfixes-dev pkg-config texi2html zlib1g-dev unzip
```
3. Create directory
```
mkdir ~/ffmpeg_sources
cd ~/ffmpeg_sources
```
4. Here it is my personnal configuration
  1. yasm
  ```
  cd ~/ffmpeg_sources
  wget http://www.tortall.net/projects/yasm/releases/yasm-1.3.0.tar.gz
  tar xzvf yasm-1.3.0.tar.gz
  cd yasm-1.3.0
  ./configure --prefix="$HOME/ffmpeg_build" --bindir="$HOME/bin"
  make
  make install
  make distclean
  cd ..
  ```
  2. H.264
  ```
  sudo apt-get install libx264-dev
  ```
  3. AAC
  ```
  cd ~/ffmpeg_sources
  wget -O fdk-aac.zip https://github.com/mstorsjo/fdk-aac/zipball/master
  unzip fdk-aac.zip
  cd mstorsjo-fdk-aac*
  autoreconf -fiv
  ./configure --prefix="$HOME/ffmpeg_build" --disable-shared
  make
  make install
  make distclean
  cd ..
  ```
  4. MP3
  ```
  sudo apt-get install libmp3lame-dev
  ```
  5. Opus
  ```
  sudo apt-get install libopus-dev
  ```
  6. VP8/VP9
  ```
  cd ~/ffmpeg_sources
  wget http://webm.googlecode.com/files/libvpx-v1.3.0.tar.bz2
  tar xjvf libvpx-v1.3.0.tar.bz2
  cd libvpx-v1.3.0
  PATH="$HOME/bin:$PATH" ./configure --prefix="$HOME/ffmpeg_build" --disable-examples
  PATH="$HOME/bin:$PATH" make
  make install
  make clean
  cd ..
  ```
  7. VisualOn AAC
  ```
  cd ~/ffmpeg_sources
  wget http://webm.googlecode.com/files/libvpx-v1.3.0.tar.bz2
  tar xjvf libvpx-v1.3.0.tar.bz2
  cd libvpx-v1.3.0
  PATH="$HOME/bin:$PATH" ./configure --prefix="$HOME/ffmpeg_build" --disable-examples
  PATH="$HOME/bin:$PATH" make
  make install
  make clean
  cd ..
  ```
5. The final part where you install ffmpeg
```
cd ~/ffmpeg_sources
wget http://ffmpeg.org/releases/ffmpeg-snapshot.tar.bz2
tar xjvf ffmpeg-snapshot.tar.bz2
cd ffmpeg
PATH="$HOME/bin:$PATH" PKG_CONFIG_PATH="$HOME/ffmpeg_build/lib/pkgconfig" ./configure --prefix="$HOME/ffmpeg_build" --extra-cflags="-I$HOME/ffmpeg_build/include" --extra-ldflags="-L$HOME/ffmpeg_build/lib" --bindir="$HOME/bin" --enable-gpl --enable-libass --enable-libfdk-aac --enable-libfreetype --enable-libmp3lame --enable-libopus --enable-libtheora --enable-libvorbis --enable-libvpx --enable-libx264 --enable-nonfree --enable-x11grab --enable-version3 --enable-libvo-aacenc
PATH="$HOME/bin:$PATH" make
make install
make distclean
hash -r
```
## A candy for the end
If you don't want to read [the doc](http://ffmpeg.org/documentation.html), you can still install a GUI for it
```
sudo apt-get install winff
```

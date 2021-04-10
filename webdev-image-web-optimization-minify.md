# image web optimization


step 1.-    Image is processed with a "lossy" filter that eliminates some pixel data
step 2.-    Image is processed with a "lossless" filter that compresses the pixel data


## tools requirements

- optipng
- jpegoptim
- gifsicle
- pngquant


## lossy optimization

	$ dnf install jpegoptim


$ jpegoptim photo.jpg
$ jpegoptim -v photo.jpg
$ jpegoptim -d ./compressed photo.jpg
$ jpegoptim -m50 photo.jpg


## dnf install optipng

$ optipng [options] filename.png

$ optipng file.png		(default speed)
$ optipng -o5 file.png		(slow)
$ optipng -o7 file.png		(very slow)





## other method
$ git clone https://github.com/rflynn/imgmin.git


imgmin source.jpg destination.jpg




# into ruby


```
sudo apt-get install -y advancecomp gifsicle jhead jpegoptim libjpeg-progs optipng pngcrush pngquant

bundle add image_optim


```

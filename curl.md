I had the problem to installing RCUL in R. The solution was to used sudo -apt-get but I do not have admin rights so I install curl on my software direcotry wich I have rights

Download curl sources, untar and cd into the extracted directory. Then

```
./configure --prefix=$HOME/usr
make
make install
```

and add this to you ~/.profile:
```
PATH="$HOME/usr/bin:$PATH"
export PATH
LD_LIBRARY_PATH="$HOME/usr/lib:$LD_LIBRARY_PATH"
export LD_LIBRARY_PATH
PKG_CONFIG_PATH="$HOME/usr/lib/pkgconfig:$PKG_CONFIG_PATH"
export PKG_CONFIG_PATH
```

Note, after you've setup such $HOME/usr in your ~/.profile once you can easily install most other packages to that prefix too.

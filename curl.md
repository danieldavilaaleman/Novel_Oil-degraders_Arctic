I had the problem to installing RCUL in R. The solution was to used sudo -apt-get but I do not have admin rights so I install curl on my software direcotry wich I have rights
Download curl sources, untar and cd into the extracted directory. Then
```
./configure --prefix=$HOME/usr
make
make install
```
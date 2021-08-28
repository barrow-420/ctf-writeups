# Compression in Linux

[CheatSheet](https://www.cyberciti.biz/howto/question/general/compress-file-unix-linux-cheat-sheet.php)

## # 1 tar
```
$ tar cfz bigfile.tgz bigfile
            ^            ^
            |            |
            +- new file  +- file to be compressed
```
```
$ ls -l bigfile*
-rw-rw-r-- 1 shs shs 103270400 Apr 16 16:09 bigfile
-rw-rw-r-- 1 shs shs 21608325 Apr 16 16:08 bigfile.tgz
```
 It is the combination of tar and gzip so the extension is .tgz
 
 The original file will still remain although the compression has made. 
     
## # 2 zip
```
$ zip ./bigfile.zip bigfile
updating: bigfile (deflated 79%)
$ ls -l bigfile bigfile.zip
-rw-rw-r-- 1 shs shs 103270400 Apr 16 11:18 bigfile
-rw-rw-r-- 1 shs shs  21606889 Apr 16 11:19 bigfile.zip
```

Original file remains.

Leaves the original file intact.

## # 3 gzip
```
$ gzip bigfile
$ ls -l bigfile*
-rw-rw-r-- 1 shs shs  21606751 Apr 15 17:57 bigfile.gz
```

Original file will be replaced to the .gz file.

## # 4 xz
```
$ xz bigfile
$ ls -l bigfile*
-rw-rw-r-- 1 shs shs 13427236 Apr 15 17:30 bigfile.xz
```

xz is the most impresive and newest compression method. 

For the big files, it might take longer but is more efficient in compression.

## Size Reduction Comparison

Winner is xz. Got compressed as only 13% size of the original file.
```
-rw-rw-r-- 1 shs shs 103270400 Apr 16 14:01 bigfile
------------------------------------------------------
-rw-rw-r-- 1 shs shs 18115234 Apr 16 13:59 bigfile.bz2    ~17%
-rw-rw-r-- 1 shs shs 21606751 Apr 16 14:00 bigfile.gz     ~21%
-rw-rw-r-- 1 shs shs 21608322 Apr 16 13:59 bigfile.tgz    ~21%
-rw-rw-r-- 1 shs shs 13427236 Apr 16 14:00 bigfile.xz     ~13%
-rw-rw-r-- 1 shs shs 21606889 Apr 16 13:59 bigfile.zip    ~21%
```

## Whether the original files are replaced

The bzip2, gzip and xz commands all replace the original files with compressed versions. The tar and zip commands to not.

## Run time
```
command   run-time
tar	  4.9 seconds
zip	  5.2 seconds
bzip2	 22.8 seconds
gzip	  4.8 seconds
xz       50.4 seconds
```

[Source](https://www.networkworld.com/article/3538471/how-to-compress-files-on-linux-5-ways.html)

If any problem, leave a issue and I will make changes about it. 

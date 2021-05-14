
#Bandit level 12 to 13
 Author: Raghavendra( Raghavendra1933)
Problem Page:https://overthewire.org/wargames/bandit/bandit13.html
#list of commands Used
ls -a
mkdir /tmp/Raghavendra1933
xxd -r data.txt > /tmp/Raghavendra1933/file.bin
cd /tmp/Raghavendra1933
ls-a
file file.bin
zcat file.bin | file -
zcat file.bin | bzcat | file -
zcat file.bin | bzcat | zcat | file -
zcat file.bin | bzcat | zcat | tar xO | file -
zcat file.bin | bzcat | zcat | tar xO | tar xO | file -
zcat file.bin | bzcat | zcat | tar xO | tar xO | bzcat | file -
 zcat file.bin | bzcat | zcat | tar xO | tar xO | bzcat | tar xO | file -
zcat file.bin | bzcat | zcat | tar xO | tar xO | bzcat | tar xO | zcat | file -
zcat file.bin | bzcat | zcat | tar xO | tar xO | bzcat | tar xO | zcat
cd ..
rm -rf Raghavendra1933
reset
#walkthrough
The password here is stored in data.txt file,which is a hexdump of a file that has been repeatedly compressed, so ive confused several times here missing one or other for several times, firstly i did ls in place of ls-a. and at final we must remove created directory after we are done.
#password
8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL
#bash script
hd -b input.txt
hd -x input.txt
od -b input.txt 

 

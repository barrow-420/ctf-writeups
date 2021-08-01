# 0ops!
## Short Story

As a freshman of JI, Joint institute at SJTU.
I got curious whether SJTU has a CTF team. 

I did some googling and soon found out this interesting looking [website](https://0ops.sjtu.cn/)

I instantly dived in and started to solve the puzzle.

# Task 1

![1](https://user-images.githubusercontent.com/76433661/127762978-18fcbf1e-0cc1-4e63-b432-9c33e4dacaf4.png)

There was a shell that on the website and I was able to type in commands as I wish.

However, it seemed like commands are restricted.

![2](https://user-images.githubusercontent.com/76433661/127763026-b222d887-ac5d-4830-af61-ac9ac3d5e6e6.png)

I typed ```ls``` and read through all the txt files. From the ```contact.txt``` file, I found out there is a flag hidden inside this website.

## Task 2

Although I am a very beginner at this, I had a strong feeling that I won't need strong enumeration such as nmap or dirbuster for this game so I just divded right into the source code.

As I read through the source code, I found interesting looking code containing the keyword:  ```flag```.

![3](https://user-images.githubusercontent.com/76433661/127763130-6a876030-8ea4-4ce1-8616-1e98d84f30c6.png)

According to the last line of code from the picture above, I typed ```cat .flag``` and I got nothing useful.

![4](https://user-images.githubusercontent.com/76433661/127763166-4d9d55be-38db-4560-8290-229f1eede5fb.png)

However, once I typed ```hint```, I found out this has something to do with "Konami"

## Task 3

This is where I got stuck for a long time.

I have never heard about Konami before, so I spent lots of time researching about it. 

I am kind of a guy, who pursue full understanding of the topic so I tried my best to understand as thoroughly as possible.

![5](https://user-images.githubusercontent.com/76433661/127763255-f5624413-f5a6-4fee-b2e6-f95a9544230a.png)

this is called the Konami Code and you can read more about it from [here](https://en.wikipedia.org/wiki/Konami_Code)

![6](https://user-images.githubusercontent.com/76433661/127763299-cf799004-b4e1-49bd-9e88-2cf9d59e7158.png)

I typed the Konami code and I my privilege got upgraded to the root user. 

I typed the Konami code several more times and this is what I got.

![7](https://user-images.githubusercontent.com/76433661/127763340-95d8aa91-b02a-4ed8-980e-691ff85278bd.png)

```emxpYi5kZWNvbXByZXNzKCd4nLPTpgrQsyFdi50uBtDDpg63ndiMwAVwGoPFYEzNNrp6dpjOwVQIVU6WC3CZBtcPAIrcScYnKQ==```

## Task 4
After seeing this string, I instantly guessed this has something to do with decoding, and I easily decoded it using [base64 decoder](https://www.base64decode.org/)

After decoding it, I got result of...

```zlib.decompress('x\x9c\xb3\xd3\xa6\n\xd0\xb3!]\x8b\x9d.\x06\xd0\xc3\xa6\x0e\xb7\x9d\xd8\x8c\xc0\x05p\x1a\x83\xc5`L\xcd6\xbazv\x98\xce\xc1T\x08UN\x96\x0bp\x99\x06\xd7\x0f\x00\x8a\xdcI\xc6')```

## Task 5
I have learned bit of python and Javascript, so I can roughly read the code, but I am really bad a programming, so I had to research a lot to understand how ```zlib.decompress``` works.

[This website](https://stackoverflow.com/questions/28641731/decode-gzip-compressed-and-base64-encoded-data-to-a-readable-format) helped me a lot when studying.

![8](https://user-images.githubusercontent.com/76433661/127763949-c7f20a37-7f7e-42d8-be0b-eba26b25c541.png)

I used Ubuntu and used terminal python3 to decompress.

When I decompressed it, I got this weird looking string.

```>++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++.<+++++++++++++++++++++++++++++++++++++++++++++++++.>------------------.+++++++++++++++++++.++++++++++++++++++++++++.<.>------------------------------------------.++++++++++++++++++++++++++++++++++++++++++.-----------------.<-.>++++++.+++++++++++.-----------------------.---------------------.+++++++++++++++++++++++++++++++.-------------------------------.```

## Task 6
After doing some googling, I found out this kind of string is called ```Brainfuck```

I simply used this [website](https://www.dcode.fr/brainfuck-language) to decode the brainfuck and got the flag

Find out the falg by your self. 

This was a interesting CTF and I was happy to find out that university that I would be attending has a CTF playing team.

I wish I can join the team later when I get to Shanghai.

: )

*** I will remove the the md file if there is any problem related to spoiler ***
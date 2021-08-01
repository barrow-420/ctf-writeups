# 0ops!
## Short Story

As a freshman for JI, Joint institute at SJTU.
I got curious whether SJTU has a CTF team. 

I did some googling and soone found out this interesting looking [website](https://0ops.sjtu.cn/)

I instantly dived in and started to solve the puzzle.

# Task 1

![1](https://user-images.githubusercontent.com/76433661/127762978-18fcbf1e-0cc1-4e63-b432-9c33e4dacaf4.png)

There was a shell that on the website and I was able to type in commands as I wish.

However, it seemed like commands are restricted.

![2](https://user-images.githubusercontent.com/76433661/127763026-b222d887-ac5d-4830-af61-ac9ac3d5e6e6.png)

I did ```ls``` and read through all the txt files. From the contact.txt file, I found out there is a flag hiddne inside this website.

## Task 2

Although I am a very beginner at this, I had a strong feeling that I won't need strong enumeration like nmap or dirbuster for this game so I just divded right into the source code.

As I read through the source code, I found interesting looking code containing keyword ```flag```.

![3](https://user-images.githubusercontent.com/76433661/127763130-6a876030-8ea4-4ce1-8616-1e98d84f30c6.png)

According to the last line of code from the picture above, I typed ```cat .flag``` and I got nothing useful.

![4](https://user-images.githubusercontent.com/76433661/127763166-4d9d55be-38db-4560-8290-229f1eede5fb.png)

However, once I typed ```hint```, I found out this has something to do with "Konami"


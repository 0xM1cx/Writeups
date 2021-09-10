# Taking LS

https://ctflearn.com/challenge/103

Just take the Ls. Check out this zip file and I be the flag will remain hidden. https://mega.nz/#!mCgBjZgB!_FtmAm8s_mpsHr7KWv8GYUzhbThNn0I8cHMBi4fJQp8.

When unzipping the file there is a **The Flag.pdf** within it.

When you try opening the file a password is required. 

First I tried strings then saving the output to a **flag.txt** file. [flag.txt](https://github.com/Shockx14-coder/Writeups/files/7144713/flag.txt)


![Kazam_screenshot_00000](https://user-images.githubusercontent.com/46009834/132875812-ac2b481f-2d49-4715-92ca-cae34f339b8a.png)


Then I tried Binwalk to see if there's any zip files hidden inside it. NOTHING THERE.

![Kazam_screenshot_00000](https://user-images.githubusercontent.com/46009834/132874773-2dbf1147-4929-4385-a504-e61968249871.png)


Lastly, I tried using bless to look for any evidence of tampering in hex format. STILL NOTHING THERE.

![Kazam_screenshot_00001](https://user-images.githubusercontent.com/46009834/132874535-8e5a145c-f49d-4100-a091-4778a1a299a7.png)

After ~30 mins I realized that I was overthinking it and thought of other ways on how to hide passwords.

So I thought of an idea; "What if the file is hidden in the same directory"

So I ran the `$ ls -a` to show all files in the directory including hidden files/sub-directories represented with the dot prefix ".ThePassword"

Then I saw txt file inside it and after running the `$ cat ThePassword.txt`
and it revealed the password: **Nice Job!  The Password is "Im The Flag".**

![Kazam_screenshot_00004](https://user-images.githubusercontent.com/46009834/132877554-89f11aaf-0ef2-417a-ae58-45d6c081caee.png)

By this point it was straightforward, typing password in the pdf file and there the password was revealed.

![Kazam_screenshot_00005](https://user-images.githubusercontent.com/46009834/132878317-f6b9a9d4-2a08-4b76-b92f-8e23ec6cf71f.png)

The Flag: **ABCTF{T3Rm1n4l_is_C00l}**

# Forensics 101

https://ctflearn.com/challenge/96

Think the flag is somewhere in there. Would you help me find it? https://mega.nz/#!OHohCbTa!wbg60PARf4u6E6juuvK9-aDRe_bgEL937VO01EImM7c

This is the image:

![95f6edfb66ef42d774a5a34581f19052](https://user-images.githubusercontent.com/46009834/132868920-bb04ab0f-e824-4206-b92a-45b6f3935380.jpg)

This is just an easy challenge I'm just writing this cause I just want to learn how to write Markdown files in github.

So basically just run this command: `$ strings <image_name> | grep flag`.

When running the command it will return/extract the `strings` in a given file, in this case the image

and the `grep` command is searching for a specific string is a file, you can specify a string/text next to the grep command; in our case

we needed to find a flag so guessing that the flag has a text of flag then typing flag next to grep will search for the flag word in the strings output.

The Flag is: flag{wow!_data_is_cool}

# Basic-file-exploit

### Description 
The program provided allows you to write to a file and read what you wrote from it. Try playing around with it and see if you can break it!
Connect to the program with netcat:`$ nc saturn.picoctf.net 52681`

The program's source code with the flag redacted can be downloaded [here](https://artifacts.picoctf.net/c/543/program-redacted.c).


> [!NOTE] Hints
> Try passing in things the program doesn't expect. Like string instead of a number.
> 

When we first run the program we get this prompt.
![[Pasted image 20220407193413.png]]
Doing what the hint suggest by passing in strings instead of a number we get this error. 
![[Pasted image 20220407193910.png]]
Judging from this output we now know that the program has some kind of input checking feature. Which we can break the conditions in this feature.

But first I tried to follow its instructions to see where it would lead.
When I typed 1 it asked me to enter data to write to a file and the program then assigns a entry number to the written data. 
![[Pasted image 20220407202126.png]]
No luck! Even if I tried to pass in large amounts of input.

The challege provided the source code for use to analyze. [Sorce Code](https://artifacts.picoctf.net/c/543/program-redacted.c)
From analyzing the `main` function, it seems that when the user types the 1 the `data_write()` function is invoked. Additionally, if the user types 2 the `data_read()` function is invoked.
![[Pasted image 20220410104706.png]]

The next thing I did was to checking the `data_write()` function to see if their are limitations to this program like limited number of inputs, limited number of conditions or condition where i can invoke the flag.
![[Pasted image 20220407203809.png]]
From the code you can see that a variable `char input[100]` has a limited number(100) of characters that can be stored in this array.
![[Pasted image 20220407202213.png]]
At first this could be a vulnerability to be exploited, but previously I tried this when I typed 1 and created a data entry of random number and found no lead on the flag. 

So I moved on and looked at the `data_read()` function.
![[Pasted image 20220410105649.png]]
From the code you can see that the flag keyword is passed in the `puts()` method and this can be called if the specific condition is met.
![[Pasted image 20220407204256.png]]
Notice the `char entry[4]` variable, `entry` argument in the if statement above and the `r = tgetinput(entry, 4)` variable. This tells us that the entry can only have 4 character in it which can cause a problem if a number say 10,000 entries have been created. 

With haste I invoked the `data_write()` function to create a data entry of >100 characters and when it prompted my to give length of the data I created I typed `101` which is greater than the `char input[100]` variable can store.
![[Pasted image 20220410111139.png]]Then in the `Please enter the entry number of your data` I typed a string(`Give me the flag`) instead of a number as I remembered the hint.
 ![[Pasted image 20220410111449.png]]
 Finally, the flag has been found

FLAG: `picoCTF{M4K3_5UR3_70_CH3CK_Y0UR_1NPU75_E0394EC0}`
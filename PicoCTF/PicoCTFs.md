# Basic-file-exploit

### Description 
The program provided allows you to write to a file and read what you wrote from it. Try playing around with it and see if you can break it!
Connect to the program with netcat:`$ nc saturn.picoctf.net 52681`

The program's source code with the flag redacted can be downloaded [here](https://artifacts.picoctf.net/c/543/program-redacted.c).


> [!NOTE] Hints
> Try passing in things the program doesn't expect. Like string instead of a number.
> 

When we first run the program we get this prompt.
![Pasted image 20220407193413](https://user-images.githubusercontent.com/46009834/162869476-534c2b7f-8926-455f-b82c-a07f2915dd25.png)


Doing what the hint suggest by passing in strings instead of a number we get this error. 
![[Pasted image 20220407193910.png]]
![Pasted image 20220407193910](https://user-images.githubusercontent.com/46009834/162869533-92397891-7dcf-415f-813b-c77a248ae320.png)

Judging from this output we now know that the program has some kind of input checking feature. Which we can break the conditions in this feature.

But first I tried to follow its instructions to see where it would lead.
When I typed 1 it asked me to enter data to write to a file and the program then assigns a entry number to the written data. 
![[Pasted image 20220407202126.png]]
![Pasted image 20220407202126](https://user-images.githubusercontent.com/46009834/162869557-ae8f8905-73a1-4903-88c9-b74d7327c81c.png)

No luck! Even if I tried to pass in large amounts of input.

The challege provided the source code for use to analyze. [Sorce Code](https://artifacts.picoctf.net/c/543/program-redacted.c)
From analyzing the `main` function, it seems that when the user types the 1 the `data_write()` function is invoked. Additionally, if the user types 2 the `data_read()` function is invoked.
![[Pasted image 20220410104706.png]]
![Pasted image 20220410104706](https://user-images.githubusercontent.com/46009834/162869606-9bd929fb-568b-4891-9c6a-53dc9a4b2f36.png)

The next thing I did was to checking the `data_write()` function to see if their are limitations to this program like limited number of inputs, limited number of conditions or condition where i can invoke the flag.
![[Pasted image 20220407203809.png]]
![Pasted image 20220407203809](https://user-images.githubusercontent.com/46009834/162869636-df04c4d9-f2d7-4827-ad71-c35675c2fc91.png)

From the code you can see that a variable `char input[100]` has a limited number(100) of characters that can be stored in this array.
![[Pasted image 20220407202213.png]]
![Pasted image 20220407202213](https://user-images.githubusercontent.com/46009834/162869680-14457686-04b0-4bb9-ad4b-9512f6aee2bf.png)

At first this could be a vulnerability to be exploited, but previously I tried this when I typed 1 and created a data entry of random number and found no lead on the flag. 

So I moved on and looked at the `data_read()` function.
![[Pasted image 20220410105649.png]]
![Pasted image 20220410105649](https://user-images.githubusercontent.com/46009834/162869727-87417e04-2d18-428d-ae30-e821ad921a85.png)

From the code you can see that the flag keyword is passed in the `puts()` method and this can be called if the specific condition is met.
![[Pasted image 20220407204256.png]]
![Pasted image 20220407204256](https://user-images.githubusercontent.com/46009834/162869753-d3cb2ae9-c514-4bd4-9476-dc8ebdec8cdb.png)


Notice the `char entry[4]` variable, `entry` argument in the if statement above and the `r = tgetinput(entry, 4)` variable. This tells us that the entry can only have 4 character in it which can cause a problem if a number say 10,000 entries have been created. 

With haste I invoked the `data_write()` function to create a data entry of >100 characters and when it prompted my to give length of the data I created I typed `101` which is greater than the `char input[100]` variable can store.
![[Pasted image 20220410111139.png]]
![Pasted image 20220410111139](https://user-images.githubusercontent.com/46009834/162869796-c1ac9645-39ef-4ef0-b932-0e09e0737ef5.png)

Then in the `Please enter the entry number of your data` I typed a string(`Give me the flag`) instead of a number as I remembered the hint.
 ![[Pasted image 20220410111449.png]]
 ![Pasted image 20220410111449](https://user-images.githubusercontent.com/46009834/162869810-e314f593-5a2d-49b5-898f-34ac50d2d2a5.png)

 
 Finally, the flag has been found

FLAG: `picoCTF{M4K3_5UR3_70_CH3CK_Y0UR_1NPU75_E0394EC0}`

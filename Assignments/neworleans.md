
You will immediately notice that there are a lot of functions in the beginning of the code section that do some setup work.
we are almost always only really interested in what happens once we hit the main function.
A quick look at the call’s that get made, we can see the flow is pretty simple. First we run a create_password routine, then get_password, then do a check_password.
Depending on the contents of r15 once we have done that, we will jump to unlock the lock or not.
Lets take a closer look at create_password.
The create_password routine seems to be moving some bytes (using mov.b) at incrementing offsets relative to 0x2400. The final mov.b instruction at 0x44ac moves a null byte into the last memory location before returning the method call. I guess its obvious what is going on here already.
Lets take a look at check_password
A quick read seems like 8 cmp.b operations are performed from the same offset we have had when create_password started writing those bytes. So, create_password writes the password to memory, check_password just compares those bytes to the ones entered by the user.
Lets debug this application and see what it looks like. First, set a breakpoint just after create_password is done at 0x4440 with break 4440. This will let us have a peek at 0x2400 to see what that the memory looks like there. The next break point that might be interesting would be where the character comparisons are occurring in check_password at 0x44c2, so add another break point with break 44c2. Finally, hit c to continue the CPU
Right after we hit our first breakpoint, we can see that the bytes 2e67 374d 4748 2f00 were written from 0x2400 onwards.
Using a small one-liner, we can convert the bytes that were written to ASCII and confirm it matches the section in memory:
I am pretty sure this is the password, so continue the CPU and enter .g7MGH/ when the interrupt prompts you for a password. Continue the CPU again until we hit our next breakpoint to see the byte comparisons occur. 
The CPU should step all the way though the loop for the password and finally hit the mov instruction at 0x44ce which sets r15 to 0x1 for that tst instruction in main later.
The tst instruction on register r15 should have a non-zero return in the state register sr, resulting in a win condition. This means the password is .g7MGH/!
password : .g7MGH/ in ASCII or 2e67374d47482f00 as hex 

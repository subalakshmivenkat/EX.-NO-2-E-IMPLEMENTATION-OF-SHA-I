# EX.-NO-2-E-IMPLEMENTATION-OF-SHA-I

## AIM:
  To implement the SHA-I hashing technique using C program.
  
## ALGORITHM:

  STEP-1: Read the 256-bit key values.
  
  STEP-2: Divide into five equal-sized blocks named A, B, C, D and E.
  
  STEP-3: The blocks B, C and D are passed to the function F.
  
  STEP-4: The resultant value is permuted with block E.
  
  STEP-5: The block A is shifted right by ‘s’ times and permuted with the result of
  
  
  STEP-6: Then it is permuted with a weight value and then with some other key pair and taken as the first block.
  
  STEP-7: Block A is taken as the second block and the block B is shifted by ‘s’ times and taken as the third block.
  
  STEP-8: The blocks C and D are taken as the block D and E for the final output.

## PROGRAM:
~~~
# SHA hash algorithms. 
import hashlib 

# initializing string 
str = "helloworld"
print("Text: ",str)

# then sending to SHA1() 
result = hashlib.sha1(str.encode()) 

# printing the equivalent hexadecimal value. 
print("\nThe hexadecimal equivalent of SHA1 is : ", result.hexdigest())
~~~ 
## OUTPUT:
![image](https://github.com/user-attachments/assets/8a7daeab-0a89-4ecf-bfb0-86297c6bedf9)

## RESULT:
  Thus the SHA-1 hashing technique had been implemented successfully.
  

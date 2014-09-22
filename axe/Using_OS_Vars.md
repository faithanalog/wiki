#Manipulating TI-OS Variables in Axe

##Saving to OS strings
1. Create a string variable with a length equal to your string length
2. Copy the contents of your string to the returned pointer, without the
   0 byte (null terminator) at the end.

Keep in mind that in Axe strings are stored as single byte characters
which do not match up exactly to the OS tokens used to stored OS
strings. This means that lower case letters and many special characters
will not display properly when saved to an OS string, including { } ( )
[ ]. All upper case letters, numbers, spaces should work properly.

###Example:
```
.We will write to OS string 1
"Str1"->GDB1SAVE

.String being saved
"HELLO WORLD"->Str1

length(Str1)->L

.Create string var to hold our data
GetCalc(GDB1SAVE,L)->D

.Copy contents to newly created string
Copy(Str1,D,L)
```

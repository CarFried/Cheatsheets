######Cheatsheets scripts

Scripts are nothing more than automated workflows which means less work for repetitive tasks. 

###### Beginners Guide 

1. You create a textfile (touch <file.sh>)
2. You check the permission (ls -l)
3. change the permission and make your script excecutable (chmod + x <scriptname>)
4. This step could also be the second but now you can add stuff to your file don't forget the shebang line at top of your script (#!/bin/bash) 
5. you can comment out with # 

######common errors 

- always check the spacing between the commands it won't work if the space is to wide.
- Variables are uppercase by convention & should be referenced with a $ before the variable
- closing the if statements with an fi 
- overwriting a file by using > instead of >> (which adds stuff at the end of the script whereas > overwrites the file)

######Commands 

#####print stuff : 
echo 
#####reference variables: 

NAME="Timmy"
echo "My name is $NAME"

#####prompt user: 
read -p

#####if statement: 

if [ "$NAME" == "Timmy"]
then 
echo "Your name is Timmy"
fi 

#####else if and else

if [ "$NAME" == "Timmy" ]
then 
echo "Your name is Timmy"
elif [ "$NAME"== "Caro"]
then 
echo "Your name is Caro"
else 
echo "Your name is NOT Timmy or Caro"
fi 

#####comparison 

-eq returns true if values are equal
-ne returns true if values are not equal 
-gt greater than 
-ge greater than or equal 
-lt lesser than 
-le lesser or equal than 

#####File condition
-d file  true if the file is a directory
-e file   true if the file exists note that this is not particulary portable to usually -f is used) 
-f file  true if the provided string is a file 
-g file  true if the group id is then on a file 
-r file  true if the file is readable 
-s file true if the file has a non-zero size 
-u file true if the user id is set on a file 
-w true if the file is writable 
-x true if the file is an executable 

#####ForLoop

NAMES="Brad Kevin Alice Mark"
for NAME in $NAMES 
do 
echo "Hello $NAME"
done

#####FOR LOOP to RENAME FILES

FILES=$(ls *.txt)
NEW="new"
for FILE in $FILES
do 
echo "Renaming $File to new-$FILE"
mv $FILE $NEW-$FILE
done

####### write to a file 

use vim ;) 
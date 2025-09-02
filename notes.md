### Basic syntax
- Comments starts with #
- Commands run one after the other from top to bottom, this affects the logic and functionality of the script
- use ; to run multiple commands on the same line
```bash
# this is a comment
echo "Hello"
echo "hi"; echo "all"
```

### Simple script
```bash
# vi example_script.sh

#!/bin/bash  # shebang
echo "Hello"
```

### Using variables
```bash
#!/bin/bash
name="Ram"
echo "Hello, $name!"
number=4
echo "The number is $number"
```

### environment variable example
```bash
# To check environmental variables
env

# lets say you installed python under the path '/home/user/python3/bin'

# temporarily add python to path (works for current terminal session)
export PATH="/home/user/python3/bin:$PATH"

# To add permanently to path
echo 'PATH="/home/user/python3/bin:$PATH"' >> ~/.bashrc  # echo 'PATH="/home/user/python3/bin:$PATH"' >> ~/.zshrc  and later give  source ~/.zshrc
source ~/.bashrc
which python3



# To define a custom temporary variable
export MY_VAR="this is user custom variable"
echo $MY_VAR

# To add it to permanently user-wide env variable and this variable will be available for that user
echo 'export MY_VAR="this is user custom variable"' >> ~/.bashrc
source ~/.bashrc

# To add system-wide, edit /etc/environment  
sudo vi /etc/environment # add -> MY_VAR="this is user custom variable"

source /etc/environment
```

### local and global variables
```bash
#!/bin/bash

my_function(){
    local local_var="This local   variable"
    echo $local_var   #  $local_var -> This local variable  (it collapses multiple spaces),   and if you give echo '$local_var'-> $local_var
    echo "$local_var"  # "$local_var" -> This local   variable (it preserves the spaces)
    echo '$local_var'  # It literally prints $local_var
}
my_function

```

### How to take input from user
```bash
# example 1
echo "Enter your name"
read name
echo "Hello, $name"

# example 2
read -p "Enter your name and age:" name age
echo "Name is $name and age is $age"

# example 3
read -sp "Enter password" pass  # s->hides the input, p-> prompt
echo  # echo after read adds a newline because the prompt leaves the cursor on the same line
echo "password entered successfully"

```

### Types of arrays
```bash
# Indexed arrays
#!/bin/bash
data=("ram" 25 "newyork" 99.5) # index starts with 0
echo "particular value: ${data[0]}"
echo "All values: ${data[@]}"

# Add at specific index
data[1]="23" # replacing 25
# Add at end
data+=("male")


# remove element at specific index
unset data[4]  # removes male

unset data  # nothing will show deleting whole array

for i in "${data[@]}"; do
   echo "$i"
done


```
```bash
# Associated arrays

#!/bin/bash

declare -A person

person[name]="ram"
person[age]=25
person[city]="newyork"
person[marks]=99.5

# Access individual value
echo "Name: ${person[name]}"

# Add a new element
person[gender]="male"

# remove element gender
unset person[gender]

unset person  # nothing will show deleting whole array

for i in "${!person[@]}"; do
   echo "$i : ${person[$i]}    
done

```

```bash
# strings
s="Hello"
n="Ram"
r="$s, $n!"
echo "$r"


# numbers
n1=5
n2=5
add=$((n1+n2))
sub=$((n1-n2))
mul=$((n1*n2))
quo=$((n1/n2))
rem=$((n1%n2))
echo "$n1, $n2, $add, $sub, $mul, $quo, $rem"

# operators
: '
# comparison operators

-eq  equals to
-ne  not equal to
-lt  less than
-le  less than or equal to
-gt  greater than
-ge  greater than or equal to

=  equal to
!= not equal to
<  less than
>  greater than 


# Arithmetic operators
+ addition
- subtraction
* multiplication
/ division
% modulus (remainder of division)


# logical operators
&& logical AND
|| logical OR
!  logical NOT


# File operators
-e checks if a file exists
-d checks if a directory exists
-f checks if a file is a regular file
-s checks if a file is not empty

'

# conditional statements
a=5
if [ "$a" -lt 10 ]; then
  echo "It is less"
fi


b=10
if [ "$b" -le 9 ]; then
  echo "It is less"
else
  echo "It is equal"
fi

c=10
if [ "$c" -le 9 ]; then
  echo "It is less"
elif [ "$c" -ge 9 ]; then
  echo "It is greater"
else
  echo "It is equal"
fi

if [ "$c" -ge 9 ]; then
  if [ "$c" -lt 17 ]; then
     echo "It is less"
  fi
fi

# loops
for i in {1..5}; do
  echo -n "$i "
done

echo 

c=1
while [ $c -le 5 ]; do
  echo "$c"
  ((c++))
done

for i in {1..3}; do
  for j in {1..2}; do
    echo  "$i, $j"
  done
done

for i in {1..5}; do
  if [ $i -eq 3 ]; then
    continue
  fi
  echo "$i"
  if [ $i -eq 4 ]; then
    break
  fi
done

echo

# until loops execute until a specified condition becomes true
c=1
until [ $c -ge 5 ]; do
  echo "$c"
  ((c++))
done

# functions
wish(){
    echo "wish"
}
wish
echo
greet(){
    echo "The parameters are $1, $2"
    local sum=$(($1 + $2))
    echo "The sum is, $sum"
}
greet 5 12
echo
result=$(greet 5 12)
echo "$result"

```

### Users
```bash
# To check users
cat /etc/passwd

# Create a user
sudo adduser user_name

# To set password or change the password to user
sudo passwd user_name

# add user is in sudo group
sudo usermod -aG sudo user_name
groups user_name  # To check added or not 


# To switch to the user
su user_name  # switch to current directory
su - user_name 

# To lock the user account
sudo passwd -l user_name
sudo passwd -S user_name  # To check the password status of the user and L -> means account is locked

# To unlock user account
sudo passwd -u user_name
sudo passwd -S user_name  # P -> password is set and account is unlocked

# To delete a password for user
sudo passwd -d user_name

# To delete user account but keep the home directory and files are kept
sudo deluser user_name
# To delete user account and everything like home directory and mail spool
sudo deluser --remove-home user_name 



# for root path
cat /etc/passwd
sudo passwd root
sudo passwd -l root
sudo passwd -S root
su -   # To switch to the root from non-root  , It will ask password
sudo passwd -u root
sudo passwd -S root
sudo passwd -d root  # delete password for the user
```

```bash
# To create a new group
sudo groupadd group_name

# To check the group added or not
getent group   # getent group group_name

# Add user to group
sudo usermod -aG group_name user_name

# To check memberships
groups user_name

# To remove user from group
sudo gpasswd -d user_name group_name
groups user_name

# To delete a group
getent group
sudo groupdel group_name


# example
# Both user 'ubuntu, test' are under same group 'devops'. So if a file/folder is given group permission(chmod g+rwx), both can read/write inside it. So you can go and access any file or folder of these users.
sudo groupadd devops
getent group
sudo usermod -aG devops ubuntu
groups ubuntu
sudo usermod -aG devops test
groups test


```


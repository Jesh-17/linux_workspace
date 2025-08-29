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



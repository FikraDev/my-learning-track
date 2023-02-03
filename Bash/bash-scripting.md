# BASH Scripting Guide

## Creating a Script File

- First make sure the home directory is the current directory.
- In the home directory, create the script file. This can be named anything but must end with **.sh**:

```bash
    touch scriptname.sh
```

- If you attempt to run the file as it is at this stage it will not work and will tell you that you do not have any permission to do so.  to change the permission level on the file, run:

```bash
    chmod 755 scriptname.sh
    
    or 
    
    chmod a+x scriptname.sh
```

- You can run the script using either:

```bash
    bash scriptname.sh
    
    or
    
    ./scriptname.sh
```

## Viewing Available Shells

- To view available shells on a Linux systems type:

```sql
    cat /etc/shells
```

## Editing a Script File

- Using your favorite text editor, to edit the script file, open the file.  Using vim, the command is:

```bash
    vim scriptname.sh
 ```

- This will open the file in an editable manner.
- From here you need to make sure that the file is recognized by the correct interpreter. So enter the shebang ( #! ) and the directory to your bash, /bin/bash:

```bash
    #!/bin/bash
```

## Variables

- System variables are usually in capital letters
- User-defined variables are normally in common letters
- To define a user variable, simply type the name of the variable followed by the equal sign without any space and finally the value you want to assign to the variable:

    ```bash
    name=value
    ```

- To use the variable or call the variable, simply place a dollar sign ($) before the variable name:

    ```bash
    $name 
    ```

## Reading User Input

- To read user input, the “read” command is used:

    ```bash
    echo "Enter Name: "
    read variablname
    ```

- To read multiple inputs:

    ```bash
    read variable1 variable2 variable2
    ```

- The names are entered in the same manner as they are read, ie each variable value is separated by a space.
- To enter the username on the same line as the text:

    ```bash
    read -p 'username: ' variablename
    ```

- To get silent input such as a password on the same line:

    ```bash
    read -sp 'username: ' variablename
    ```

## Saving User input in an Array

- To save user input into an array, the -a flag is used:

    ```bash
    echo "Enter Names: "
    
    read -a variablename
    ```

- To print out the values from the array:

    ```bash
    echo "The values from the array are ${variablename[0]},  ${variablename[1]}"
    ```

## Excluding Variable Name after Read command

- If you do not place a variable name after the read command, the value enter can still be retrieved by using the default $REPLY command:

    ```bash
    echo "Enter your name : "
    read
    
    echo The name entered is $REPLY
    ```

## Passing Arguments to a Bash Script

- There are two ways in which you can pass arguments into a bash script:
  - In the first method you create inside of the script the variables where the arguments will be passed to:

     ```bash
        echo $a $b 
    ```

  - Next you pass the arguments when calling the script eg:

    ```bash
        ./scriptname argument1 argument2
        
        ./myscript ryan dionne
    ```

## If Else Statements

- The `if` statement is closed with a `fi` (reverse of if).
- There must be a space between the opening and closing brackets
and the condition you write. Otherwise, the shell will complain of
error.
- There must be space before and after the conditional
operator (=, ==, <= etc). Otherwise, you'll see an error like "unary
operator expected".
- You can use an elif (else-if) statement whenever you want to test more than one expression (condition) at the same time.

    ```bash
    numberTwelve=12
    
    if [ $numberTwelve -eq 12 ]
    then
            echo "numberTwelve is equal to 12"
    elif [ $numberTwelve -gt 12 ]
    then
            echo "numberTwelve variable is greater than 12"
    else
            echo "neither of the statemens matched"
    fi
    ```

## Numeric Comparisons[]

- If you want to do a numerical comparison you will need to use one of the following operators between square brackets [] .
  - eq (is equal)
  - ge (equal or greater than)
  - gt (greater than)
  - le (less than or equal)
  - lt (less than)
  - ne (not equal)
- So for example if you wanted to see if 12 is equal to or less than 25 it would you like:

    ```bash
    [ 12 -le 25 ]
    ```

- The 12 and 25, of course, can be variables:

    ```bash
    [$twelve -le $twentyfive]
    ```

## **String comparisons [[]]**

- Uses the double square brackets [[]] and the following operators equal or not equal:
  - == (equal)
  - != (not equal)
- Keep in mind strings have several other comparisons that we will not discuss but dig in and read about them and how they work.

    ```bash
    #variable with a string
        stringItem="Hello"
    
    #This will match since it is looking for an exact match with $stringItem
        if [[ $stringItem = "Hello" ]]
        then
                echo "The string is an exact match."
        else
                echo "The strings do not match exactly."
        fi
    
    #This will utilize the then statement since it is not looking for a case sensitive match
        if [[ $stringItem = "hello" ]]
        then
                echo "The string does match but is not case sensitive."
        else
                echo "The string does not match because of the capitalized H."
        fi
    ```

## File Test Operators

- Used to test if a file exists, file type, is readable/writeable etc.
- List of File test operators:

    | -e | File exists |
    | --- | --- |
    | -f | File is a regular file |
    | -s | file is not zero size |
    | -d | File is a directory |
    | -c | File is a character device |
    | -p | File is a pipe |
    | -h | File is a symbolic link |
    | -L | File is a symbolic link |
    | -S | File is a socket |
    | -t | File is associated with a terminal device |
    | -r  | file has read permission for the person running the test |
    | -w | file has write permission (for the user running the test) |
    | -x  | file has execute permission (for the user running the test) |
    | -O | you are owner of file |
    | -G | group-id of file same as yours |
    | -N | file modified since it was last read |
    | f1 -nt f2 | file f1  is newer than f2 |
    | f1 -ot f2 | file f1  is older than f2 |
    | f1 -ef f2 | files f1  and f2  are hard links to the same file |
    | ! | "not" -- reverses the sense of the tests above (returns true if condition absent) |

## Scripting Commands

- **echo** - used to return something to the terminal.  You can use single quotes, double quotes or no quotes:

    ```bash
    echo Hello World!
    echo 'Hello World!'
    echo "Hello World!"
    ```

- **Command Substitution $( ) or ``** - Command substitution allows you to get the results of a command you might execute at the command line and write that result to a variable:

    ```bash
    command1=`ls`
    echo $command1
    
    command2=$(ls)
    echo $command2
    ```

    **Note that there is no space between the command, equal sign and the substitution.  Spaces will throw an error.**

- **Double Parentheses (())** - Double parentheses are simple, they are for mathematical equations.

    ```bash
    echo $((5+3)) 
    echo $((5-3)) 
    echo $((5*3)) 
    echo $((5/3))
    ```

## Adding Comments

- To add a comment anywhere in a bash script use the pound/hashtag sign:

    ```bash
    #this is a comment
    #it will not be printed on screen
    ```

- **‘:’**  and **“ ’ ”**  symbols are used to add multi-line comments in bash script:

    ```bash
    : '
    The following script calculates
    the square value of the number, 5.
    '
    ((area=5*5))
    echo $area
    ```

## Logical ‘AND’ Operator

- performs Boolean AND operation
- Bash Boolean AND operator takes two operands and returns true if both the operands are true, else it returns false.

    ```bash
    if [ condition1 ] && [ condition2 ];
    
    or 
    
    if [ condition1 **-a**  condition2 ];
    
    or
    
    if [[ condition1 &&  condition2 ]];
    ```

## Logical ‘OR’ Operator

- Bash Boolean OR operator takes two operands and returns true if any of the operands is true, else it returns false.

    ```bash
    if [ condition1 ] || [ condition2 ];
    ```

## Pipe Operator |

- Grep searches one or more input files for lines containing a match to a specified pattern. By default, Grep outputs the matching lines.

    ```bash
    ls -l | grep learn
    
    ls -l /etc | less
    ```

- Normally the *ls -l*  command would provide a list of the files on your screen. Here the full results of the *ls*  *-l* command are piped into the grep command which searches for the string *learn*. Think of the pipe command like a filter. A command is run, in this case *ls -l* , and the results are limited to the files inside your directory. These results are sent via the pipe command to *grep*
which searches for the work *learn*  and only that line appears.

- Less  is a program similar to more(1), but which allows backward movement in the file as well as forward movement.  Also, less does not have to read the entire input file  before  starting,  so with  large input files it starts up faster than text editors like vi(1).  Less uses termcap (or terminfo on some systems), so it can run on a variety of terminals.  There is even limited  support  for hardcopy terminals.  (On a hardcopy terminal, lines which should be printed at the top of the screen are prefixed with a caret.)

## Standard Output(stdout) >,>>,1>, 1>>

- The output of a command preceding the > or >> is sent to a file whose name follows.
- The >> and 1>> will append the data to the end of the file.
- In each case (> or >>) the file is created if it does not exist.

## **Standard Error (stderr), 2>, and 2>>**

- The error output of a command preceding the > or >> is sent to a file whose name follows. Keep in mind that 2> and 2>> have the same result but the 2>> will append the data to the end of the file. So what is the purpose of these? What if you only want to catch an error. Then the 2> or 2>> is here to help. The 2 indicates the output that would normally go to stderr (standard error). Now put this into practice by listing a non-existent file.

## **All Output &>, &>> and |&**

- n Bash 5 the preferred way to redirect both stdout and stderr to the same file is to use &> or, as you might guess, &>> to append to a file.

## Functions

- Think of this as a simple way to put a part of a script that is used over and over into one reusable group.
- You will need a name for your function, the opening and closing parentheses, and curly brackets to enclose the commands that are included in your function.

    ```bash
    helloFunc() {
            echo "Hello from a function."
    }
    
    #invoke the first function helloFunc()
    helloFunc
    ```

- Functions are a good way to reuse a group of commands but they can be even more useful if you can make them operate on different data each time they are used. This requires that you provide data, referred to as arguments, to the function each time you call it.

- To provide arguments, you simply add them after the function name when you invoke it. To use the data you provide, you use the positional references in the function commands. They will be named $1, $2, $3, and so on, depending on the number of arguments your function will need.

    ```bash
    helloFunc() {
    echo "Hello from a function."
    echo $1
    echo $2
    echo "You gave me $# arguments"
    }
    
    #invoke the function helloFunc()
    helloFunc "How is the weather?" Fine
    ```

- Notice that the first argument was a single string enclosed in double quotes, “How is the weather?” . The second one, “Fine”, had no spaces so the quotes where not needed.
- In addition to using $1, $2, etc. you can determine the number of arguments being passed to the function by using the variable $#. This means that you can create a function which accepts a variable number of arguments.

## While Loop

- The commands  contained between *do*  and *done*  are executed since the *while* comparison is true. so we *echo*  some text and add one to the value of *number* . We continue until the *while*
statement is no longer true and it breaks out of the loop and echo’s “We have completed the while loop since $number is greater than 10.”

    ```bash
    number=1
    
    while [ $number -le 10 ]
    do
            echo "We checked the current number is $number so we will increment once"
            ((number=number+1))
    done
            echo "We have completed the while loop since $number is greater than 10."
    ```

## For Loop

- The basic **for**  loop declaration is shown in the following example:

    ```bash
    for (( counter=10; counter>0; counter-- ))
    do
    echo -n "$counter "
    done
    printf "\n"
    ```

## Get User Input

- The ‘**read**’ command is used to take input from user in bash.  Here, one string value will be taken from the user and display the value by combining other string value:

    ```bash
    echo "Enter Your Name"
    read name
    echo "Welcome $name to LinuxHint"
    ```

## Case Statement

- The **Case**  statement is used as the alternative of **if-elseif-else**  statement. The starting and ending block of this statement is defined by ‘**case** ’ and ‘**esac**’.

    ```bash
    echo "Enter your lucky number"
    read n
    case $n in
    101)
    echo echo "You got 1st prize" ;;
    510)
    echo "You got 2nd prize" ;;
    999)
    echo "You got 3rd prize" ;;
    *)
    echo "Sorry, try for the next time" ;;
    esac
    ```

## Combining String Variables

- You can combine string variables in bash by placing variables together or using **‘+’** operator.

    ```bash
    string1="Linux"
    string2="Hint"
    echo "$string1$string2"
    string3=$string1+$string2
    string3+=" is a good tutorial blog site"
    echo $string3
    ```

## Getting substring of String

- Here, the value, **6**  indicates the starting point from where the substring will start and **5**  indicates the length of the substring:

    ```bash
    Str="Learn Linux from LinuxHint"
    subStr=${Str:6:5}
    echo $subStr
    ```

## Make Directory

- Bash uses the ‘mkdir’ command to make a new directory:

    ```bash
    echo "Enter directory name"
    read newdir
    `mkdir $newdir`
    ```

## Read a File

- You can read any file line by line in bash by using loop:

    ```bash
    file='book.txt'
    while read line; do
    echo $line
    done < $file
    ```

## Delete a File

- ‘**rm**’ command is used in bash to remove any file:

    ```bash
    echo "Enter filename to remove"
    read fn
    rm -i $fn
    ```

## Get Parse Current Date

- You can get the current system date and time value using `**date**` command. Every part of date and time value can be parsed using ‘**Y’, ‘m’, ‘d’, ‘H’, ‘M’**
and ‘**S’:**

    ```bash
    Year=`date +%Y`
    Month=`date +%m`
    Day=`date +%d`
    Hour=`date +%H`
    Minute=`date +%M`
    Second=`date +%S`
    echo `date`
    echo "Current Date is: $Day-$Month-$Year"
    echo "Current Time is: $Hour:$Minute:$Second"
    ```

## Wait Command

- **wait**  is a built-in command of Linux that waits for completing any running process. **wait** command is used with a particular process id or job id. If no process id or job id is given with wait command then it will wait for all current child processes to complete and returns exit status.

    ```bash
    echo "Wait command" &
    process_id=$!
    wait $process_id
    echo "Exited with status $?"
    ```

## Sleep Command

- When you want to pause the execution of any command for specific period of time then you can use **sleep** command. You can set the delay amount by **seconds (s), minutes (m), hours (h) and days (d).**

## Reading File Contents

- There are many ways to read file contents in Bash. One of the easiest ways is to use a while loop:
- **Option 1:**

    ```bash
    while read variableName_to_store_content
    do
        echo $variableName
    done < file_to_read
    ```

- **Option 2:**

    ```bash
    cat file_to_read | while read variableName
    do
        echo $variableName
    done
    ```

- **Option 3:**:

    ```bash
    while IFS= read -r line
    do
        echo $line
    done < file_to_read
    ```

## Until Loop

The syntax for the until loop is:

```bash
until [ command ]
do
    code to be executed
done
```

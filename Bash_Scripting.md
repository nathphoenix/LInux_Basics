BASH
Bash :Bourne again shell.
(e)grep :filters input based on regex pattern matching.
cat : conactenate file contents line-by-line
tail \ head give only the last -n (a flag) lines
Wc : does a word or line count (with flags -w -l) 
sed : does pattern-match string replacement

grep 'a' fruits.txt  : returns all content in the file

grep 'p' fruits.txt : will use regext to get contents containing p

Running script with the command below
if firsr line start with (#!/bin/bash)
bash script_name.sh OR 
if firsr line start with (#!/usr/bash)
bash ./script_name.sh


Counting items in a text file containing
categories of animal i.e 
shark fish
eagle bird
vulture bird

bash script(group.sh)
#!/bin/bash
concatenate the text file which will split on spaces, sort them and count the unique animal
cat animals.txt | cut -d " " -f 2 | uniq -c

STDIN-STDOUT-STDERR
STDIN: standard input
STDOUT: standard output
STDERR: standard error

"2 > /dev/null" : means redirecting STDERR to be deleted
"1 > /dev/null" : means redirecting STDOUT to be printed

cat sports.txt 1> new_sport.txt which will write same content to the new file

ARGV is the array of all arguments given to the program. which is accessible with $ notation i.e first $1, seond as $2
$@ and $* which returns all the argument together
$# gives length of the arguments

Creating a variable in bash
we use the $ sign to create a variable i.e:
firstname= 'Cynthia'
Lastname = 'Liu'
echo "Hi there " $firstname $lastname

Shell within a shell
double_quotest = "The date is `date`" 
echo $double_quotest will return : The date is 23 June 2022

Addition in bash
is done using expr
i.e expr 1 + 4 = 5
but this does not work for decimal numbers
echo "5 + 7.5" | bc

echo "10 / 3" | bc while this will return 3
echo "scale=3; 10 / 3" | bc which will return 3.33

using a shell in a shell

model1=88.34
model=86.21
echo "Total score is $(echo "$model1 + $model2" | bc)"
echo "Total score is $(echo "($model1 + $model2) / 2" | bc)"

creating an array

declare -a my_first_array
my_first_array=(1 2 3)

returning all array elements
echo ${my_first_array[@]}

Length of an array is return using:
#array_name[@]
echo $(#my_first_array[@])

manipulating array, indexing an array
echo ${my_first_array[2]}

assigning a new value to an existing element in an array
my_first_array[1]=20
echo ${my_first_array[1]}

Slicing an array
array_name[@]:N:M
where N means starting index, and M means number of elements to return

Appending to an array
array_name+=(elements)

IF ESLE STATEMENT IN BASH
we finish an if else statement with fi
if [CONDITION]; then
    # SOME CODE
else
    # SOME CODE
fi

Example

x="Queen"
if [$x = "King"]; then
    echo "$x is a King"
else
    echo "$x is a Queen"
fi

x=10
if (($x > 5)); then
    echo "$x is more than 5"
fi
other flags
-eq : equal to
-ne : not equal to
-lt : less than
-le : less than or equal to
-gt : greater than
-ge : greater than or equal to

x=10
if [$x -gt 5]; then
    echo "$x is greater than 5!"
fi

other bash conditional flags
-e if file exist
-s if file exist and has size greater than zero
-r if the file exist and is readable
-w if the file exist and is writable
https://www.gnu.org/software/bash/manual/html_node/Bash-conditional-Expressions.html

Using AND and OR in bash
&& AND operator
|| OR operator

Multiple condition

x=10
if [$x -gt 5] && [$x -lt 11]; then
    echo "$x is more than 5 and less than 11"
fi

OR

if [[$x -gt 5 && $x -lt 11]]; then
    echo "$x is more than 5 and less than 11"
fi

Using grep

if grep -q 'Hello' words.txt; then
    echo "Hello is inside!"
fi

IF with shell within a shell

if $(grep -q 'Hello' words.txt);
    echo "Hello is inside!"
fi


FORLOOP in bash

for x in 1 2 3
do
    echo $x
done

loop through between 1 to 5 and skip in 2 step
for x in {1..5..2}
do
    echo $x
done

for ((x=2, x<=6; x+=2>))
do
    echo $x
done

Looping through a file in bash

for book in books/*
do
    echo $book
done


Shell within a shell
for book in $(ls books/ | grep -i 'air)
do
    echo $book
done

WHILE LOOP statement
x=1
while [$x -le 3];
do
    echo $x
    ((x+=1))
done


FUNCTION IN BASH
function print_hello () {
    echo "Hello world"
}
print_hello : we then call the function like this

temp_f=30

function convert_temp(){
    temp_c=$(echo "scale=2; ($temp_f - 32) *5 /9" | bc)
    echo $temp_c
}
convert_temp  #calling the function

function convert_temp{
    $(echo "scale=2; ($temp_f - 32) *5 /9" | bc)
}
converted=$(convert_temp 30)
echo "30F IN Celsius is $converted C"
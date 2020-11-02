# bash

## Scripting

### Coding Guidelines

Coding guidelines -
1. Please find the naming conventions below -
    1. shell script file names     :
        1. The file names should be meaning full and need to represent the operation that is being performed
        2. The file names are LOWER CASE LETTERS in "UNDERSCORE" naming convention
               Ex: process_inputs.sh
    2. function names              :
        1. The function names should be meaning full and need to represent the operation that is being performed
        2. The function names are LOWER CASE LETTERS in "UNDERSCORE" naming convention
              Ex: function check_empty_and_exit_on_empty
    3. global variables            :
        1. The global variables are UPPER CASE LETTERS in "UNDERSCORE" naming convention
               Ex: JENKINS_SCRIPT_DIR
    4. function local variables    :
        1. The local variables are LOWER CASE LETTERS in "UNDERSCORE" naming convention
               Ex: exit_code
2. Please follow the philosophy of not trusting the end user of the script :P:P
3. Please check every step. Because Murphy's Law will hold true :P:P
      So remember "what can go wrong will go wrong".
4. Please follow space based indentations with each indentation level spaced by "4" spaces
5. Any functions that could be reused across different scripts should be placed under "common_functions.sh".
6. Any variables that could be reused across different scripts should be placed under "common_variables.sh".
7. Please use appropriate print functions according to needed debug level
      print_info
      print_debug
8. Please make all comparisons to "0" instead of "1" i.e. assume that we are comparing a unsinged integer
        This is to upold the below logic -
    1. "0" is defined as "false"
    2. Any other value is treated as "true"
9. All functions should have below information
    TODO:


### Adding function to file

```bash
source ${SCRIPT_PATH}
. ${SCRIPT_PATH}
```
When you run a script, your current shell, such as bash, launches a child shell, most often sh, to run the script.
You can instead execute a script that modifies the current shell environment using the source command.

### Export

Use it to export a value to a child script

## Commands

### set

```bash
set -eu
set -o pipefail
```

-u makes it an error to reference a non-existent environment variable such as ${HSOTNAME}, at the cost of requiring some gymnastics with checking ${#} before you reference ${1}, ${2}, and so on.
pipefail makes things like misspeled-command | sed -e 's/^WARNING: //' raise errors.

[When to use set -e](https://stackoverflow.com/a/13478622/2843359)

### Job Control

```bash
jobs - list the current jobs
fg - resume the job that\'s next in the queue
fg %[number] - resume job [number]
bg - Push the next job in the queue into the background
bg %[number] - Push the job [number] into the background
kill %[number] - Kill the job numbered [number]
kill -[signal] %[number] - Send the signal [signal] to job number [number]
disown %[number] - disown the process(no more terminal will be owner), so command will be alive even after closing the terminal.
```

[how can I resume a stopped job](https://superuser.com/a/268268)

## Cheat Sheet

```bash
The following reference cards provide a useful summary of certain scripting concepts. The foregoing text treats these matters in more depth, as well as giving usage examples.


Table B-1. Special Shell Variables

Variable    Meaning
$0          Filename of script
$1          Positional parameter #1
$2 - $9     Positional parameters #2 - #9
${10}       Positional parameter #10
$#          Number of positional parameters
"$*"        All the positional parameters (as a single word) *
"$@"        All the positional parameters (as separate strings)
${#*}       Number of positional parameters
${#@}       Number of positional parameters
$?          Return value
$$          Process ID (PID) of script
$-          Flags passed to script (using set)
$_          Last argument of previous command
$!          Process ID (PID) of last job run in background
* Must be quoted, otherwise it defaults to $@.


Table B-2. TEST Operators: Binary Comparison

Operator                    Meaning                 -----   Operator                Meaning
Arithmetic Comparison                                       String Comparison
-eq                         Equal to                        =                       Equal to
                                                            ==                      Equal to
-ne                         Not equal to                    !=                      Not equal to
-lt                         Less than                       \<                      Less than (ASCII) *
-le                         Less than or equal to
-gt                         Greater than                    \>                      Greater than (ASCII) *
-ge                         Greater than or equal to
                                                            -z                      String is empty
                                                            -n                      String is not empty

Arithmetic Comparison   within double parentheses (( ... ))
>                           Greater than
>=                          Greater than or equal to
<                           Less than
<=                          Less than or equal to
* If within a double-bracket [[ ... ]] test construct, then no escape \ is needed.


Table B-3. TEST Operators: Files

Operator                    Tests Whether               -----       Operator                Tests Whether
-e                          File exists                             -s                      File is not zero size
-f                          File is a regular file
-d                          File is a directory                     -r                      File has read permission
-h                          File is a symbolic link                 -w                      File has write permission
-L                          File is a symbolic link                 -x                      File has execute permission
-b                          File is a block device
-c                          File is a character device              -g                      sgid flag set
-p                          File is a pipe                          -u                      suid flag set
-S                          File is a socket                        -k                      "sticky bit" set
-t                          File is associated with a terminal

-N                          File modified since it was last read    F1 -nt F2               File F1 is newer than F2 *
-O                          You own the file                        F1 -ot F2               File F1 is older than F2 *
-G                          Group id of file same as yours          F1 -ef F2               Files F1 and F2 are hard links to the same file *

!                           NOT (inverts sense of above tests)
* Binary operator (requires two operands).


Table B-4. Parameter Substitution and Expansion

Expression                  Meaning
${var}                      Value of var (same as $var)

${var-$DEFAULT}             If var not set, evaluate expression as $DEFAULT *
${var:-$DEFAULT}            If var not set or is empty, evaluate expression as $DEFAULT *

${var=$DEFAULT}             If var not set, evaluate expression as $DEFAULT *
${var:=$DEFAULT}            If var not set or is empty, evaluate expression as $DEFAULT *

${var+$OTHER}               If var set, evaluate expression as $OTHER, otherwise as null string
${var:+$OTHER}              If var set, evaluate expression as $OTHER, otherwise as null string

${var?$ERR_MSG}             If var not set, print $ERR_MSG and abort script with an exit status of 1.*
${var:?$ERR_MSG}            If var not set, print $ERR_MSG and abort script with an exit status of 1.*

${!varprefix*}              Matches all previously declared variables beginning with varprefix
${!varprefix@}              Matches all previously declared variables beginning with varprefix
* If var is set, evaluate the expression as $var with no side-effects.

# Note that some of the above behavior of operators has changed from earlier versions of Bash.

Table B-5. String Operations

Expression                                  Meaning
${#string}                                  Length of $string

${string:position}                          Extract substring from $string at $position
${string:position:length}                   Extract $length characters substring from $string at $position [zero-indexed, first character is at position 0]

${string#substring}                         Strip shortest match of $substring from front of $string
${string##substring}                        Strip longest match of $substring from front of $string
${string%substring}                         Strip shortest match of $substring from back of $string
${string%%substring}                        Strip longest match of $substring from back of $string

${string/substring/replacement}             Replace first match of $substring with $replacement
${string//substring/replacement}            Replace all matches of $substring with $replacement
${string/#substring/replacement}            If $substring matches front end of $string, substitute $replacement for $substring
${string/%substring/replacement}            If $substring matches back end of $string, substitute $replacement for $substring


expr match "$string" '$substring'           Length of matching $substring* at beginning of $string
expr "$string" : '$substring'               Length of matching $substring* at beginning of $string
expr index "$string" $substring             Numerical position in $string of first character in $substring* that matches [0 if no match, first character counts as position 1]
expr substr $string $position $length       Extract $length characters from $string starting at $position [0 if no match, first character counts as position 1]
expr match "$string" '\($substring\)'       Extract $substring*, searching from beginning of $string
expr "$string" : '\($substring\)'           Extract $substring* , searching from beginning of $string
expr match "$string" '.*\($substring\)'     Extract $substring*, searching from end of $string
expr "$string" : '.*\($substring\)'         Extract $substring*, searching from end of $string
* Where $substring is a Regular Expression.


Table B-6. Miscellaneous Constructs

Expression                                  Interpretation

Brackets
if [ CONDITION ]                            Test construct
if [[ CONDITION ]]                          Extended test construct
Array[1]=element1                           Array initialization
[a-z]                                       Range of characters within a Regular Expression

Curly Brackets
${variable}                                 Parameter substitution
${!variable}                                Indirect variable reference
{ command1; command2; . . . commandN; }     Block of code
{string1,string2,string3,...}               Brace expansion
{a..z}                                      Extended brace expansion
{}                                          Text replacement, after find and xargs


Parentheses
( command1; command2 )                      Command group executed within a subshell
Array=(element1 element2 element3)          Array initialization
result=$(COMMAND)                           Command substitution, new style
>(COMMAND)                                  Process substitution
<(COMMAND)                                  Process substitution

Double Parentheses
(( var = 78 ))                              Integer arithmetic
var=$(( 20 + 5 ))                           Integer arithmetic, with variable assignment
(( var++ ))                                 C-style variable increment
(( var-- ))                                 C-style variable decrement
(( var0 = var1<98?9:21 ))                   C-style ternary operation

Quoting
"$variable"                                 "Weak" quoting
'string'                                    'Strong' quoting

Back Quotes
result=`COMMAND`                            Command substitution, classic style

Special variables
	$0	 Name of the script from the command line
	$1	 First command-line argument
	$2	 Second command-line argument
	$3	 Third command-line argument
	$4	 Fourth command-line argument
	$5	 Fifth command-line argument
	$6	 Sixth command-line argument
	$7	 Seventh command-line argument
	$8	 Eighth command-line argument
	$9	 Ninth command-line argument
	$#	 Number of command-line arguments
    $*	 All command-line arguments, separated with spaces
```

# Hashtags

#linux #bash
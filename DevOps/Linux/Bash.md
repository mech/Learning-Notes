# Bash

* [Mastering Bash and Terminal](https://www.blockloop.io/mastering-bash-and-terminal)
* [Bash conditional statements](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_07_01.html)
* [Command Line Text Processing](https://github.com/learnbyexample/Command-line-text-processing)

## Special Parameters

* [The shell treats several parameters specially. These parameters may only be referenced; assignment to them is not allowed](https://www.gnu.org/software/bash/manual/html_node/Special-Parameters.html)

```
$0 - Positional argument, the program itself
$1 - Argument 1
$2 - Argument 2
$3 - Argument 3 and so on...

$* - All the arguments
$@ - All the arguments (same but with subtle difference)

$# - The count of arguments

$? - Print last error code. Most recent foreground pipeline exit status.

$! - PID of the most recent background command
$$ - PID of the current shell (not sub-shell)

$- - Current options set for the shell

// The ampersand give us back the prompt without waiting for it
▶ ./somelongwork &

// Run in order with semicolon
▶ pwd ; ls
```

```
// Find out what shell you are in
▶ ps -p $$
```

```
▶ for file in *.jpg;do echo convert $file ${file%.jpg}.png;done
```

```
▶ find . -name "*.haml" | wc -l
▶ find . -type f | sed 's/.*\.//' | sort | uniq -c
```

```
// Find the process that is using this port
▶ lsof -i :3000
```

## Permission

* 600 - Read/Write by owner only
* 755 - Execute permission set. Same as a+x

## Variables

* Surround your variables with quotes: `"$x"`
* Use braces to denote where your variable name end: `"${foo}bar"`
* Use `$HOME` instead of `~`

```
NAME=mech
echo $NAME
echo ${NAME}
echo "$NAME"
echo "${NAME}"
echo ${NAME%e} # Take off the e character
▶ convert "$PIC" "${PIC%.jpg}.png"

dirname="${1%/*}"
basename="${1##*/}" // double # get the longest match

// Using double quote is always recommended
bindir="${HOME}/bin"

// Get the length of the string in a variable
${#var}

# In contrast to C, a Bash variable declared inside a function
# is local ONLY if declared as such
file_env() {
  local name=mech # Declared as local variable
  global_var=9999
}```

## Command Substitution

```
date=$(date)
```

## I/O Redirection

```
/dev/stdin = 0
/dev/stdout = 1
/dev/stderr = 2
/dev/null

Since 2 is the specific stream number for error, you can do 2>, so:
▶ cmd 2> /dev/null # Will discard all errors

▶ 2>&1 # Redirects stderr into stdout

▶ ls -l data.txt > output.txt
▶ ls -l not.here 2> error.txt
▶ ls -l data.txt not.here &> both.txt
▶ ls -l data.txt not.here > output.txt 2>&1 # Order is important

▶ ls | wc # STDOUT is being pipe to STDIN to wc
```

`2>&1` is redirect standard error??

## Decisions

```
# Tests on files and directories
# [[...]] is a bash extension. No quotes needed around variables.
if [[ ! -d $VOLUME_HOME/mysql ]]; then
fi

# Arithmetic tests
if [[ $# -ne 2 ]]; then
  echo "Need exactly two arguments"
  exit 1
fi

# Do not use double equal and must have space
if [[ $1 = "cat" ]]; then
  echo "meow"
fi
```

```
▶ help [[
▶ help test
```

### While

```
while test; do
  ;;
done

until test; do
  ;;
done
```

### For loop



## Printf

```
▶ printf "|%20s |%20s |%20s |\n" $(ls)
```

## sed

```
sed -i -r "s/license key here/${1}" newrelic.js
```


# Bash

* [Mastering Bash and Terminal](https://www.blockloop.io/mastering-bash-and-terminal)
* [Bash conditional statements](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_07_01.html)
* [Command Line Text Processing](https://github.com/learnbyexample/Command-line-text-processing)

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


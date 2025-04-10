# 1. Parameter Expansion

Bash parameter expansion provides powerful ways to manipulate variables, extract substrings, apply conditional defaults, and more — all without invoking external commands. This makes scripts faster and more readable.

- [1. Parameter Expansion](#1-parameter-expansion)
    - [1.0.1. Expansion Types](#101-expansion-types)
      - [1.0.1.1. Basic Usage:](#1011-basic-usage)
      - [1.0.1.2. Default Value:](#1012-default-value)
      - [1.0.1.3. Set Default:](#1013-set-default)
      - [1.0.1.4. Error if Unset:](#1014-error-if-unset)
      - [1.0.1.5. Check if Non-Empty](#1015-check-if-non-empty)
      - [1.0.1.6. String Length](#1016-string-length)
      - [1.0.1.7. Substring Extraction](#1017-substring-extraction)
      - [1.0.1.8. Remove Prefix](#1018-remove-prefix)
      - [1.0.1.9. Remove Long Prefix](#1019-remove-long-prefix)
      - [1.0.1.10. Remove Suffix](#10110-remove-suffix)
      - [1.0.1.11. Remove Long Suffix](#10111-remove-long-suffix)
      - [1.0.1.12. Replace First Match](#10112-replace-first-match)
      - [1.0.1.13. Replace All Matches](#10113-replace-all-matches)
      - [1.0.1.14. Uppercase First Char](#10114-uppercase-first-char)
      - [1.0.1.15. Uppercase All Chars](#10115-uppercase-all-chars)
      - [1.0.1.16. Lowercase First Char](#10116-lowercase-first-char)
      - [1.0.1.17. Lowercase All Chars](#10117-lowercase-all-chars)
      - [1.0.1.18. Toggle Case](#10118-toggle-case)
      - [1.0.1.19. Toggle all cases](#10119-toggle-all-cases)
      - [1.0.1.20. Array slicing and substrings](#10120-array-slicing-and-substrings)
      - [1.0.1.21. String slicing with negative offsets](#10121-string-slicing-with-negative-offsets)
      - [1.0.1.22. String slicing with negative offset and length](#10122-string-slicing-with-negative-offset-and-length)
      - [1.0.1.23. Parameter transformation `${parameter@operator}`](#10123-parameter-transformation-parameteroperator)


### 1.0.1. Expansion Types


#### 1.0.1.1. Basic Usage:

| Syntax   | What it does?           | Example and Output                                                                                           |
| -------- | ----------------------- | ------------------------------------------------------------------------------------------------------------ |
| `${var}` | Gets the value of `var` | <pre>dzuniga@vm_aws#~ name="Diego" <br>dzuniga@vm_aws#~ echo "${name}" <br>dzuniga@vm_aws#~ Diego <br></pre> |
|          |                         |                                                                                                              |

#### 1.0.1.2. Default Value:

| Syntax            | What it does?                                        | Example and Output                                                                                                                                                            |
| ----------------- | ---------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `${var:-default}` | Uses `default` value if `var` is not set or is empty | <pre><br>dzuniga@vm_aws#~ var=" " <br>dzuniga@vm_aws#~ echo "${var:-'no_value'}" <br>dzuniga@vm_aws#~ no_value <br>dzuniga@vm_aws#~ echo $var <br>dzuniga@vm_aws#~ " " </pre> |

#### 1.0.1.3. Set Default:

| Syntax            | What it does?                                               | Example and Output                                                                                                                                                                   |
| ----------------- | ----------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `${var:=default}` | Sets `var` to `default` if unset or empty (and returns it). | <pre><br>dzuniga@vm_aws#~ var=" " <br>dzuniga@vm_aws#~ echo "${var:='no_value'}" <br>dzuniga@vm_aws#~ no_value <br>dzuniga@vm_aws#~ echo $var <br>dzuniga@vm_aws#~ "no_value" </pre> |

#### 1.0.1.4. Error if Unset:

| Syntax          | What it does?                                 | Example and Output                                                                                                                                              |
| --------------- | --------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `${var:?Error}` | Exits with `Error` if `var` is unset or empty | <pre><br>dzuniga@vm_aws#~ var=" " <br>dzuniga@vm_aws#~ echo "${var:?'Value of var is not set'}" <br>dzuniga@vm_aws#~ bash: var: Value of var is not set" </pre> |


#### 1.0.1.5. Check if Non-Empty 

| Syntax          | What it does?                                        | Example and Output                                                                                                                                             |
| --------------- | ---------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `${var:+value}` | Returns `value` only if `var` is *set and not empty* | <pre><br>dzuniga@aws_vm#~ var='regex'<br>dzuniga@aws_vm#~ echo "\$\{var:+'var_value'\}"<br>'var_value'<br>dzuniga@aws_vm#~ echo "\$\{var\}"<br>regex<br></pre> |


#### 1.0.1.6. String Length

| Syntax    | What it does?                | Example and Output                                                                     |
| --------- | ---------------------------- | -------------------------------------------------------------------------------------- |
| `${#var}` | Returns  the length of `var` | <pre><br>dzuniga@aws_vm#~ var='regex'<br>dzuniga@aws_vm#~ echo "\$\{#var\}"<br>5</pre> |


#### 1.0.1.7. Substring Extraction

| Syntax                | What it does?                            | Example and Output                                                                                      |
| --------------------- | ---------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| `${var:start:length}` | Extracts a substring from variable `var` | <pre><br>dzuniga@aws_vm#~ var='abcdefg1234567890'<br>dzuniga@aws_vm#~ echo "\$\{var:5:3\}"<br>fg1</pre> |

#### 1.0.1.8. Remove Prefix

| Syntax           | What it does?                                      | Example and Output                                                                                                       |
| ---------------- | -------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| `${var#pattern}` | Removes the shortest prefix matching the `pattern` | <pre><br>dzuniga@aws_vm#~ file='sosreport_caseid_103446.tar.gz'<br>dzuniga@aws_vm#~ echo "\$\{file#*.\}"<br>tar.gz</pre> |

#### 1.0.1.9. Remove Long Prefix

| Syntax            | What it does?                                         | Example and Output                                                                                                    |
| ----------------- | ----------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| `${var##pattern}` | Removes the **longest** prefix matching the `pattern` | <pre><br>dzuniga@aws_vm#~ file='sosreport_caseid_103446.tar.gz'<br>dzuniga@aws_vm#~ echo "\$\{file##*.\}"<br>gz</pre> |

#### 1.0.1.10. Remove Suffix 

| Syntax           | What it does?                                          | Example and Output                                                                                                                            |
| ---------------- | ------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------- |
| `${var%pattern}` | Removes the **shortest** suffix matching the `pattern` | <pre><br>dzuniga@aws_vm#~ file='sosreport_caseid_103446.tar.gz'<br>dzuniga@aws_vm#~ echo "\$\{file%*.\}"<br>sosreport_caseid_103446.tar</pre> |

#### 1.0.1.11. Remove Long Suffix

| Syntax            | What it does?                                         | Example and Output                                                                                                                         |
| ----------------- | ----------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `${var%%pattern}` | Removes the **longest** suffix matching the `pattern` | <pre><br>dzuniga@aws_vm#~ file='sosreport_caseid_103446.tar.gz'<br>dzuniga@aws_vm#~ echo "\$\{file%%*.\}"<br>sosreport_caseid_103446</pre> |


#### 1.0.1.12. Replace First Match

| Syntax           | What it does?                                                       | Example and Output                                                                                                                                                             |
| ---------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `${var/old/new}` | Replaces the **first** occurrence of `old` with the value of `new`. | <pre><br>dzuniga@aws_vm#~ favorite_distro='My favorite distro is Fedora'<br>dzuniga@aws_vm#~ echo "\$\{favorite_distro/Fedora/Ubuntu\}"<br>My favorite distro is Ubuntu </pre> |


#### 1.0.1.13. Replace All Matches

| Syntax            | What it does?                                                  | Example and Output                                                                                                                                                                                                                                                                          |
| ----------------- | -------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `${var//old/new}` | Replaces **all** occurrences of `old` with the value of `new`. | <pre><br>dzuniga@aws_vm#~ fs_choosen='EXT4 is a filesystem widely used in Linux Systems. EXT4 not allows snapshots as BTRFS does. '<br>dzuniga@aws_vm#~ echo "\$\{fs_choosen//EXT4/XFS\}"<br>XFS is a filesystem widely used in Linux Systems. XFS not allows snapshots as BTRFS does</pre> |

#### 1.0.1.14. Uppercase First Char

| Syntax    | What it does?                            | Example and Output                                                                                     |
| --------- | ---------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| `${var^}` | Capitalizes the first character of `var` | <pre><br>dzuniga@aws_vm#~ status='shutdown'<br>dzuniga@aws_vm#~ echo "\$\{status^\}"<br>Shutdown</pre> |

#### 1.0.1.15. Uppercase All Chars

| Syntax     | What it does?                                 | Example and Output                                                                                      |
| ---------- | --------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| `${var^^}` | Converts all characters in `var` to uppercase | <pre><br>dzuniga@aws_vm#~ status='shutdown'<br>dzuniga@aws_vm#~ echo "\$\{status^^\}"<br>SHUTDOWN</pre> |


#### 1.0.1.16. Lowercase First Char

| Syntax    | What it does?                            | Example and Output                                                                               |
| --------- | ---------------------------------------- | ------------------------------------------------------------------------------------------------ |
| `${var,}` | Lowercases the first character of  `var` | <pre><br>dzuniga@aws_vm#~ string='Regex'<br>dzuniga@aws_vm#~ echo "\$\{string,\}"<br>regex</pre> |


#### 1.0.1.17. Lowercase All Chars

| Syntax     | What it does?                                 | Example and Output                                                                                                                                                                                                                                                             |
| ---------- | --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `${var,,}` | Converts all characters in `var` to lowercase | <pre><br>dzuniga@aws_vm#~ string='EXT4 is a filesystem widely used in Linux Systems. EXT4 not allows snapshots as BTRFS does.'<br>dzuniga@aws_vm#~ echo "\$\{string,,\}"<br>'ext4 is a filesystem widely used in linux systems. ext4 not allows snapshots as btrfs does'</pre> |

#### 1.0.1.18. Toggle Case

| Syntax    | What it does?                             | Example and Output                                                                                             |
| --------- | ----------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| `${var~}` | Toggles the `case` of the first character | <pre><br>dzuniga@aws_vm#~ string='Shell script'<br>dzuniga@aws_vm#~ echo "\$\{string~\}"<br>shell script</pre> |


#### 1.0.1.19. Toggle all cases

| Syntax     | What it does?                        | Example and Output                                                                                              |
| ---------- | ------------------------------------ | --------------------------------------------------------------------------------------------------------------- |
| `${var~~}` | Toggles the `case` of all characters | <pre><br>dzuniga@aws_vm#~ string='Shell script'<br>dzuniga@aws_vm#~ echo "\$\{string~~\}"<br>sHELL SCRIPT</pre> |

#### 1.0.1.20. Array slicing and substrings

| Syntax                     | What it does?                                                             | Example and Output                                                                                           |
| -------------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| `${array[@]:start:length}` | Expands to `length` elements starting at position `start`                 | <pre>dzuniga@aws_vm#~ arr=(a b c d e)<br>dzuniga@aws_vm#~ echo "\${arr[@]:1:3}"<br>b c d</pre>               |
| `${array[@]: -n}`          | Expands to the last `n` elements of the array (note the space before `-`) | <pre>dzuniga@aws_vm#~ arr=(one two three four)<br>dzuniga@aws_vm#~ echo "\${arr[@]: -2}"<br>three four</pre> |
| `${#array[@]}`             | Expands to the number of elements in the array                            | <pre>dzuniga@aws_vm#~ arr=(x y z)<br>dzuniga@aws_vm#~ echo "\${#arr[@]}"<br>3</pre>                          |
| `${#array[index]}`         | Expands to the length (in characters) of a specific element in the array  | <pre>dzuniga@aws_vm#~ arr=(abc def)<br>dzuniga@aws_vm#~ echo "\${#arr[1]}"<br>3</pre>                        |
| `${!array[@]}`             | Expands to the list of indices of the array                               | <pre>dzuniga@aws_vm#~ arr=(a b c)<br>dzuniga@aws_vm#~ echo "\${!arr[@]}"<br>0 1 2</pre>                      |
| `${array[@]}`              | Expands to all the elements of the array                                  | <pre>dzuniga@aws_vm#~ arr=(sun moon star)<br>dzuniga@aws_vm#~ echo "\${array[@]}"<br>sun moon star</pre>     |

#### 1.0.1.21. String slicing with negative offsets

| Syntax                 | What it does?                                                              | Example and Output                                                                          |
| ---------------------- | -------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| `${var:offset}`        | Extracts substring from `offset` to end                                    | <pre>dzuniga@aws_vm#~ str="abcdef"<br>dzuniga@aws_vm#~ echo "\${str:2}"<br>cdef</pre>       |
| `${var:offset:length}` | Extracts `length` characters from position `offset`                        | <pre>dzuniga@aws_vm#~ str="abcdef"<br>dzuniga@aws_vm#~ echo "\${str:1:3}"<br>bcd</pre>      |
| `${var: -n}`           | Extracts the last `n` characters from the string (space before `-` needed) | <pre>dzuniga@aws_vm#~ str="networking"<br>dzuniga@aws_vm#~ echo "\${str: -4}"<br>king</pre> |


#### 1.0.1.22. String slicing with negative offset and length

| Syntax         | What it does?                                                              | Example and Output                                                                                         |
| -------------- | -------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| `${var: -N}`   | Extracts the last `N` characters from the string (space before `-` needed) | <pre>dzuniga@aws_vm#~ str="abcdef"<br>dzuniga@aws_vm#~ echo "\${str: -2}"<br>ef</pre>                      |
| `${var: -N:M}` | Extracts `M` characters starting from `N`th-last position                  | <pre>dzuniga@aws_vm#~ str="abcdef"<br>dzuniga@aws_vm#~ echo "\${str: -3:2}"<br>de</pre>                    |
| `${var:X:-Y}`  | **Invalid** syntax — length can't be negative                              | <pre>dzuniga@aws_vm#~ str="abcdef"<br>dzuniga@aws_vm#~ echo "\${str:2:-1}"<br>bash: bad substitution</pre> |

> Tip: Always insert a space before the negative offset to avoid bash interpreting it as an option. Negative `length` is **not supported** and will cause an error.

#### 1.0.1.23. Parameter transformation `${parameter@operator}`

| Syntax     | What it does?                                                                                              | Example and Output                                                                                                                                                                                                              |
| ---------- | ---------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `${var@U}` | Converts **all characters** in the value of `var` to **uppercase**                                         | <pre>dzuniga@aws_vm#~ var='bash power'<br>dzuniga@aws_vm#~ echo \${var@U}<br>BASH POWER</pre>                                                                                                                                   |
| `${var@u}` | Converts **only the first character** of `var` to uppercase                                                | <pre>dzuniga@aws_vm#~ var='bash'<br>dzuniga@aws_vm#~ echo \${var@u}<br>Bash</pre>                                                                                                                                               |
| `${var@L}` | Converts **all characters** in the value of `var` to **lowercase**                                         | <pre>dzuniga@aws_vm#~ var='BASH Power'<br>dzuniga@aws_vm#~ echo \${var@L}<br>bash power</pre>                                                                                                                                   |
| `${var@Q}` | Prints the value in a **quoted form** that can be reused in Bash input                                     | <pre>dzuniga@aws_vm#~ var='my "var" value'<br>dzuniga@aws_vm#~ echo \${var@Q}<br>'my var value'</pre>                                                                                                                           |
| `${var@E}` | Expands **backslash-escaped sequences** (like `\n`, `\t`) into their **literal characters**, like `$'...'` | <pre>dzuniga@aws_vm#~ msg='Rumi Phrase:\t\n The Quieter You Become,\n The More You Are Able To Hear\n'<br>dzuniga@aws_vm#~echo "\${msg@E}"<br>Rumi Phrase:	<br> The Quieter You Become,<br> The More You Are Able To Hear</pre> |
| `${var@P}` | Interprets the value of `var` as a **prompt string** with escape sequences like `\u`, `\h`, `\w`, etc.     | <pre>dzuniga@aws_vm#~:/etc$ prompt='\n[\u@\H \d \t]\n[\w]\n\\$ '<br>dzuniga@aws_vm#~:/etc$ echo "\${prompt@P}"<br>[dzuniga@aws_vm dom abr 06 22:32:03]<br>[/etc]<br>$ </pre>                                                    |
| `${var@A}` | Expands as a `declare` **assignment string**, recreating the variable with type and value                  | <pre>dzuniga@aws_vm#~ declare -A map=([k]="v")<br>dzuniga@aws_vm#~ echo \${map@A}<br>declare -A map=([k]="v")</pre>                                                                                                             |
| `${var@a}` | Outputs variable **attributes as flags**, such as `a` (array), `i` (integer), etc.                         | <pre>dzuniga@aws_vm#~ declare -i num=5<br>dzuniga@aws_vm#~ echo \${num@a}<br>i</pre>                                                                                                                                            |

>  Notes:
> - Most transformations require **Bash 4.4+**.
> - For `@P`, expansions follow **PS1-style prompt escapes** and display shell-like formatted prompts.
> - `@a` reveals variable flags like `i` (integer), `a` (array), `x` (exported), etc.

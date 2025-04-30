# 🐧 Advanced Linux Shell Operations

Mastering redirection, piping, and text manipulation allows for powerful command-line workflows in Linux. Below is a categorized guide with annotated examples.

----------

## 🔁 I/O Redirection

### 🔸 Output Redirection (`>` and `>>`)

-   `>`: Overwrites file contents.
    
-   `>>`: Appends to file.
    

```bash
ls -l /var/log > myoutput.txt      # Overwrites myoutput.txt with the directory listing
echo "Hello World" >> peanuts.txt  # Appends text to peanuts.txt
> somefile.txt                     # Creates or empties somefile.txt

```

### 🔸 Input Redirection (`<`)

-   Redirects a file's contents into a command's standard input.
    

```bash
cat < peanuts.txt > banana.txt     # Reads from peanuts.txt, writes to banana.txt

```

Note: Commands like `ls` or `pwd` do not read from standard input, so using `< peanuts.txt` with them is typically invalid.

### 🔸 Error and Combined Redirection (`2>`, `&>`, `2>&1`)

-   Redirect stderr and/or combine with stdout.
    

```bash
ls /fake/path 2> error.txt             # Redirects stderr to error.txt
ls /fake/path > out.txt 2>&1           # Redirects both stdout and stderr to out.txt
ls /fake/path &> combined.txt          # Same as above
ls /fake/path 2> /dev/null             # Suppresses only errors
ls /fake/path > /dev/null 2>&1         # Suppresses all output

```

----------

## 🔗 Command Chaining and `tee`

### 🔸 Piping (`|`)

-   Passes output of one command to another.
    

```bash
ls -la /etc | less                     # Paginate long output

```

### 🔸 Using `tee`

-   Outputs to both screen and file(s).
    

```bash
ls | tee peanuts.txt                  # Saves and displays output
ls | tee peanuts.txt banana.txt       # Writes to multiple files

```

----------

## 🌍 Environment Variables

```bash
echo $HOME     # User's home directory
echo $USER     # Current user
env            # Lists all environment variables
echo $PATH     # Executable search path

```

----------

## ✂️ Text Manipulation Tools

### 🔸 `cut`: Extract columns or character ranges

```bash
cut -c 5 sample.txt                    # 5th character of each line
cut -c 5-10 sample.txt                 # Characters 5 through 10
cut -c 5- sample.txt                   # From 5th character to end
cut -c -5 sample.txt                   # First 5 characters
cut -f 1 -d ";" sample.txt             # First field using ';' delimiter

```

### 🔸 `paste`: Merge lines horizontally

Given `sample2.txt`:

```
The
quick
brown
fox

```

```bash
paste -s sample2.txt                  # Merges lines into one
paste -d ' ' -s sample2.txt           # Same with space delimiter
paste -s sample2.txt sample.txt       # Side-by-side from both files

```

----------

## 📃 Viewing File Content

### 🔸 `head` and `tail`

```bash
head -n 15 /var/log/messages          # First 15 lines
head -c 15 /var/log/messages          # First 15 bytes
tail -n 10 /var/log/messages          # Last 10 lines
tail -f /var/log/messages             # Follow live updates

```

----------

## ↔️ Tabs and Spaces

### 🔸 `expand` and `unexpand`

```bash
expand sample.txt                     # Converts tabs to spaces
expand sample.txt > result.txt
unexpand -a result.txt                # Converts spaces back to tabs

```

Without arguments, `expand` waits for input from stdin.

----------

## 🔗 File Joining and Splitting

### 🔸 `join`: Merge files by common fields

**file1.txt**

```
1 John
2 Jane
3 Mary

```

**file2.txt**

```
1 Doe
2 Doe
3 Sue

```

```bash
join file1.txt file2.txt

```

Output:

```
1 John Doe
2 Jane Doe
3 Mary Sue

```

Use custom fields:

```bash
join -1 2 -2 1 file1.txt file2.txt    # Join using field 2 from file1 and 1 from file2

```

### 🔸 `split`: Break a file into parts

```bash
split somefile                        # Creates files like xaa, xab, etc.

```

----------

## 🔤 Sorting and Filtering

### 🔸 `sort`

```bash
sort file1.txt                        # Alphabetical sort
sort -r file1.txt                     # Reverse sort
sort -n file1.txt                     # Numerical sort
ls /etc | sort -rn                    # Sort numerically, in reverse

```

### 🔸 `tr`: Translate or delete characters

```bash
echo hello | tr a-z A-Z               # Uppercase transformation
echo hello | tr -d ello               # Deletes 'e', 'l', 'o'

```

### 🔸 `uniq`: Remove duplicates (adjacent lines only)

```bash
uniq reading.txt                      # Removes repeated lines
uniq -c reading.txt                   # Shows count of occurrences
uniq -u reading.txt                   # Unique lines only
uniq -d reading.txt                   # Duplicates only
sort reading.txt | uniq               # Sort before uniq for proper filtering

```

Question: What does `uniq -uc` do?

> Displays unique lines only, along with their count.

----------

## 📏 Counting and Numbering

### 🔸 `wc` - Word Count

```bash
wc /etc/passwd                        # Lines, words, bytes
wc -l /etc/passwd                     # Just lines

```

### 🔸 `nl` - Number Lines

```bash
nl file1.txt                          # Prepend line numbers
nl file1.txt | wc -l                  # Count numbered lines

```

----------

## 🔍 Pattern Matching with `grep`

```bash
grep fox sample.txt                   # Exact match
grep -i somepattern somefile          # Case-insensitive match
env | grep -i User                    # Search environment variables
ls /somedir | grep '.txt$'            # Regex for .txt files

```

----------
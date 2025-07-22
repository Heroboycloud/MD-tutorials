# Mastering `grep`, `sed`, `cut`, `sort`, and `awk`

These are powerful command-line tools for text processing in Unix/Linux. Let me explain each with practical examples.

## 1. `grep` - Search for patterns in files

**Purpose**: Search for text patterns in files or input streams.

### Basic usage:
```bash
grep "pattern" file.txt
```

### Common options:
- `-i`: Case insensitive search
- `-v`: Invert match (show lines that DON'T match)
- `-r`: Recursive search in directories
- `-n`: Show line numbers
- `-c`: Count matching lines
- `-A n`: Show n lines after match
- `-B n`: Show n lines before match
- `-E`: Extended regex (same as egrep)

### Examples:
```bash
# Find all lines containing "error" in log file
grep "error" /var/log/syslog

# Case insensitive search for "warning"
grep -i "warning" file.txt

# Count how many times "success" appears
grep -c "success" data.log

# Find lines with "192.168" and show 2 lines after each match
grep -A 2 "192.168" access.log

# Search for multiple patterns
grep -E "error|warning|critical" app.log

# Search all .txt files in current directory recursively
grep -r "TODO" .
```

## 2. `sed` - Stream editor for text transformations

**Purpose**: Perform text transformations on an input stream.

### Basic syntax:
```bash
sed 's/pattern/replacement/' file.txt
```

### Common options:
- `-i`: Edit files in-place (with backup if you use `-i.bak`)
- `-n`: Suppress automatic printing
- `-e`: Add multiple commands

### Examples:
```bash
# Replace first occurrence of "foo" with "bar" in each line
sed 's/foo/bar/' file.txt

# Replace ALL occurrences (global)
sed 's/foo/bar/g' file.txt

# Replace only on lines matching a pattern
sed '/error/s/foo/bar/' file.txt

# Delete lines containing "debug"
sed '/debug/d' file.txt

# Print lines 5-10
sed -n '5,10p' file.txt

# Multiple commands (replace foo AND delete lines with debug)
sed -e 's/foo/bar/' -e '/debug/d' file.txt

# In-place edit with backup
sed -i.bak 's/old/new/' file.txt
```

## 3. `cut` - Extract portions of lines

**Purpose**: Extract columns or fields from lines of text.

### Common options:
- `-d`: Delimiter (default is tab)
- `-f`: Fields to select (can be ranges like 1-3)
- `-c`: Select specific characters/columns

### Examples:
```bash
# Extract first column from CSV (comma-delimited)
cut -d',' -f1 data.csv

# Extract first and third columns
cut -d',' -f1,3 data.csv

# Extract characters 1-10 from each line
cut -c1-10 file.txt

# Extract username from /etc/passwd (first field, colon-delimited)
cut -d':' -f1 /etc/passwd

# Combine with other commands - get IPs from access log
grep "GET" access.log | cut -d' ' -f1
```

## 4. `sort` - Sort lines of text

**Purpose**: Sort lines in text files.

### Common options:
- `-n`: Numeric sort
- `-r`: Reverse sort
- `-k`: Sort by specific field/column
- `-u`: Unique (remove duplicates)
- `-t`: Field delimiter (default is whitespace)

### Examples:
```bash
# Simple sort
sort file.txt

# Numeric sort
sort -n numbers.txt

# Sort by second column (tab-delimited)
sort -t$'\t' -k2 data.txt

# Sort by third column numerically, then by first column alphabetically
sort -k3n -k1 data.csv

# Sort IP addresses (fourth column) numerically
sort -t. -k1n,1 -k2n,2 -k3n,3 -k4n,4 ip_list.txt

# Sort and remove duplicates
sort -u words.txt
```

## 5. `awk` - Powerful text processing language

**Purpose**: Pattern scanning and processing language.

### Basic syntax
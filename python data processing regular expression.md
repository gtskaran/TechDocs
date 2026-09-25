Python Data Processing with Regular Expressions

Regular expressions (regex) are indispensable for pattern-based data processing — extracting, cleaning, validating, and transforming text. Python's re module is the standard tool.

Quick Reference: Core re Functions

Function Purpose
re.match() Match at the start of string
re.search() Find first match anywhere
re.findall() Return all matches as list
re.finditer() Return iterator of match objects
re.sub() Replace matches
re.split() Split string by pattern
re.compile() Pre-compile pattern for reuse

---

1. Extracting Emails from Text

```python
import re

text = """
Contact us at support@example.com or sales@company.org.
Personal: john.doe123@university.edu, invalid@@nope
"""

pattern = r'[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}'
emails = re.findall(pattern, text)
print(emails)
# ['support@example.com', 'sales@company.org', 'john.doe123@university.edu']
```

Why re.compile() matters when processing large data:

```python
email_re = re.compile(pattern)
results = [email_re.findall(row) for row in large_dataset]
```

---

2. Cleaning Phone Numbers

```python
import re

raw = ["(555) 123-4567", "555.987.6543", "+1-555-222-3333", "5551234567"]

cleaned = []
for num in raw:
    digits = re.sub(r'\D', '', num)   # remove non-digits
    if len(digits) == 11 and digits.startswith('1'):
        digits = digits[1:]
    cleaned.append(digits)

print(cleaned)
# ['5551234567', '5559876543', '5552223333', '5551234567']
```

---

3. Parsing Log Files

```python
import re

log_lines = [
    '192.168.1.1 - - [10/Oct/2023:13:55:36] "GET /index.html HTTP/1.1" 200 1043',
    '10.0.0.42 - admin [10/Oct/2023:13:56:01] "POST /api/login HTTP/1.1" 401 512',
]

# Named groups make extraction readable
log_re = re.compile(
    r'(?P<ip>\d+\.\d+\.\d+\.\d+)\s+-\s+(?P<user>\S+)\s+'
    r'\[(?P<time>[^\]]+)\]\s+"(?P<method>\w+)\s+(?P<path>\S+)\s+[^"]+"\s+'
    r'(?P<status>\d+)\s+(?P<size>\d+)'
)

for line in log_lines:
    m = log_re.search(line)
    if m:
        print(m.groupdict())
# {'ip': '192.168.1.1', 'user': '-', 'time': '10/Oct/2023:13:55:36',
#  'method': 'GET', 'path': '/index.html', 'status': '200', 'size': '1043'}
# {'ip': '10.0.0.42', 'user': 'admin', ...}
```

---

4. Extracting & Normalizing Dates

```python
import re

text = "Meeting on 2023-10-05, deadline 12/31/2023, review on Oct 15, 2023."

# ISO dates
iso = re.findall(r'\d{4}-\d{2}-\d{2}', text)          # ['2023-10-05']

# US dates → reformat to ISO
us = re.findall(r'(\d{2})/(\d{2})/(\d{4})', text)
iso_converted = [f"{y}-{m}-{d}" for m, d, y in us]     # ['2023-12-31']

print(iso, iso_converted)
```

---

5. Text Cleaning & Normalization

```python
import re

dirty = "Hello!!!   This   has  EXTRA   spaces... and $$$ symbols @#$."

# Collapse whitespace
clean = re.sub(r'\s+', ' ', dirty).strip()

# Remove punctuation (keep letters, numbers, spaces)
clean = re.sub(r'[^a-zA-Z0-9\s]', '', clean)

# Collapse multiple spaces again
clean = re.sub(r'\s{2,}', ' ', clean)

print(clean)
# "Hello This has EXTRA spaces and symbols"
```

---

6. Splitting on Multiple Delimiters

```python
import re

data = "apple, banana;orange|grape   mango"
items = re.split(r'[,;|\s]+', data)
print(items)
# ['apple', 'banana', 'orange', 'grape', 'mango']
```

---

7. Lookahead / Lookbehind for Context-Aware Extraction

```python
import re

text = "Price: $45.99, Discount: $5.00, Total: $40.99"

# Extract numbers only when preceded by $
prices = re.findall(r'(?<=\$)\d+\.\d{2}', text)
print(prices)  # ['45.99', '5.00', '40.99']

# Extract keys before ':' using lookahead
keys = re.findall(r'\w+(?=:)', text)
print(keys)    # ['Price', 'Discount', 'Total']
```

---

8. Integration with Pandas

```python
import pandas as pd
import re

df = pd.DataFrame({
    'contact': ['John <john@a.com>', 'Jane <jane@b.org>', 'No email here']
})

# Extract email into new column
df['email'] = df['contact'].str.extract(r'<([^>]+)>')
print(df)
#               contact          email
# 0     John <john@a.com>   john@a.com
# 1     Jane <jane@b.org>   jane@b.org
# 2         No email here          NaN
```

str.extract() and str.replace() accept regex by default — very efficient for columnar cleaning.

---

9. Validating Input

```python
import re

def is_valid_username(s):
    return bool(re.fullmatch(r'[a-zA-Z][a-zA-Z0-9_]{2,15}', s))

print(is_valid_username("alice_99"))   # True
print(is_valid_username("9bob"))       # False (starts with digit)
print(is_valid_username("a"))          # False (too short)
```

Use re.fullmatch() when the entire string must match. re.match() only anchors at the start.

---

10. Substitution with a Function

```python
import re

text = "Errors: 5, Warnings: 12, Info: 30"

def double(match):
    return str(int(match.group()) * 2)

result = re.sub(r'\d+', double, text)
print(result)  # "Errors: 10, Warnings: 24, Info: 60"
```

This is powerful for conditional replacements, masking PII, unit conversion, etc.

---

Best Practices

1. Compile patterns you reuse — re.compile() caches and speeds up matching.
2. Use raw strings (r'...') to avoid escaping backslashes.
3. Prefer named groups (?P<name>...) for readability in complex patterns.
4. Anchor with ^ and $ when validating whole strings.
5. Be specific — \d{4} beats \d+ for years; avoid greedy .* when possible.
6. Test edge cases — use regex101.com with the Python flavor.
7. Consider alternatives — for HTML/JSON, use BeautifulSoup/json; regex is for regular patterns.

---

Common Pattern Cheat Sheet

Pattern Matches
\d Any digit
\w Word char [a-zA-Z0-9_]
\s Whitespace
. Any char (except newline)
* + ? 0+, 1+, 0 or 1
{n,m} Between n and m times
[abc] Any of a, b, c
(a\|b) a or b
^ $ Start / end of string
(?P<name>...) Named capture group
(?=...) (?<=...) Lookahead / Lookbehind


# OXM Language Cheatsheet

A complete single-page reference for OXM v2.

---

## Variables & Types

```ox
let x = 42           # integer
let y = 3.14         # float
let name = "OXM"     # string
let flag = true      # boolean
let items = [1,2,3]  # array
let map = #{"a":1}   # map / dict
let nothing = null   # null / nil / none

# Type annotations (stripped at compile time — documentation only)
let count: int = 0
let ratio: float = 0.5
let label: str = "hello"

# Constants
const PI = 3.14159
const MAX: int = 100
```

---

## Operators

```ox
# Arithmetic
x + y   x - y   x * y   x / y   x % y
pow(2.0, 8.0)   # 256.0 — use pow() for exponentiation

# Comparison
x == y   x != y   x < y   x > y   x <= y   x >= y

# Logic
x and y   x or y   not x
x && y    x || y   !x       # both forms accepted

# String
"hello" + " " + "world"     # concatenation
`Hello, ${name}!`           # interpolation

# Assignment
x = 10
x += 1   x -= 1   x *= 2   x /= 2   x %= 3
```

---

## Strings

```ox
let s = "double quoted"
let t = 'single quoted — useful when string contains "'
let u = `backtick — supports ${interpolation + " here"}`

# Interpolation with any expression
let result = `${x + y} items, avg ${avg_val}`

# Built-in string functions
len(s)                 # length
to_upper(s)            # "HELLO"
to_lower(s)            # "hello"
trim(s)                # strip whitespace
split(s, ",")          # ["a","b","c"]
join(arr, ", ")        # "a, b, c"
replace(s,"old","new") # replace all
starts_with(s, "he")   # true/false
ends_with(s, "lo")     # true/false
str(42)                # number to string
int("42")              # string to int
float("3.14")          # string to float
```

---

## Arrays

```ox
let a = [1, 2, 3, 4, 5]
let b = []               # empty

a[0]                     # index (0-based)
a[len(a) - 1]            # last element
len(a)                   # length
a = a + [6, 7]           # append

# Functional operations
map_array(a, |x| { x * 2 })          # [2,4,6,8,10]
filter_array(a, |x| { x % 2 == 0 })  # [2,4]
reduce_array(a, |acc,x| { acc+x }, 0) # 15
sort_array(a)
unique(a)

# Iteration
for item in a
  say item
end
```

---

## Maps / Dicts

```ox
let m = #{ "name": "Alice", "age": 30 }
m["name"]              # "Alice"
m["age"] = 31          # update
m["city"] = "Tokyo"    # add key
len(m)                 # number of keys

# Iteration (key-value pairs)
for pair in m
  say pair
end

# Nested maps
let config = #{ "db": #{ "host": "localhost", "port": 5432 } }
config["db"]["port"]   # 5432
```

---

## Control Flow

```ox
# if / elif / else
if x > 10
  say "big"
elif x == 10
  say "ten"
else
  say "small"
end

# for — range (exclusive upper)
for i to 5          # 0,1,2,3,4
  say i
end

# for — range with start (inclusive both ends)
for i from 1 to 5   # 1,2,3,4,5
  say i
end

# for — range with step
for i from 0 to 20 by 5   # 0,5,10,15,20
  say i
end

# for — countdown (negative step)
for i from 5 to 1 by -1   # 5,4,3,2,1
  say i
end

# for — collection
for item in [10, 20, 30]
  say item
end

# while
while x > 0
  x -= 1
end

# break / continue
for i to 10
  if i == 3 then continue end
  if i == 7 then break end
  say i
end
```

---

## Match / Switch

```ox
match x
  when 1
    say "one"
  when 2
    say "two"
  else
    say "other"
end

# Match on strings
match status
  when "ok"
    say "success"
  when "error"
    say "failed"
  else
    say "unknown"
end
```

---

## Functions

```ox
# Basic function
fn add(a, b)
  return a + b
end

# With type annotations (documentation only)
fn greet(name: str, times: int)
  for i to times
    say "Hello, " + name + "!"
  end
end

# No explicit return — last expression is returned
fn double(x)
  x * 2
end

# Closures / lambdas
let square = |x| { x * x }
let add5   = |x| { x + 5 }

# Higher-order functions
fn apply(f, val)
  return f(val)
end
say apply(square, 7)   # 49

# Compose
fn compose(f, g)
  return |x| { f(g(x)) }
end
let add5_then_square = compose(square, add5)
say add5_then_square(3)   # 64  = (3+5)^2
```

---

## Classes

```ox
class Dog
  init(name, breed)
    self.name  = name
    self.breed = breed
    self.tricks = []
  end

  fn speak()
    say self.name + " says: woof!"
  end

  fn learn(trick)
    self.tricks = self.tricks + [trick]
  end

  fn describe()
    return self.name + " (" + self.breed + ")"
  end
end

let d = Dog("Rex", "Husky")   # constructor call
d.speak()
d.learn("sit")
say d.describe()
say d.tricks          # ["sit"]
```

---

## Error Handling

```ox
# Basic try/catch
try
  let x = risky_operation()
catch err
  say "Error: " + err
end

# With finally (runs on both success and error)
try
  open_resource()
  do_work()
catch err
  say "Failed: " + err
finally
  close_resource()   # always runs
end

# Throw / raise
fn must_positive(n)
  if n < 0
    throw "value must be positive, got " + str(n)
  end
  return n
end

try
  must_positive(-5)
catch err
  say "caught: " + err
end

# Nested try/catch
try
  try
    throw "inner"
  catch inner_err
    say "inner: " + inner_err
    throw "outer"   # re-throw or new error
  end
catch outer_err
  say "outer: " + outer_err
end
```

---

## Modules / Imports

```ox
# Import another .ox file (inlined at compile time)
import "utils.ox"
import "lib/helpers.ox"

# After import, all functions/variables in the imported file are available
say helper_function(42)
```

---

## Output

```ox
say "message"      # print with newline
show "message"     # alias for say
log "message"      # alias (colored in REPL)
warn "message"     # yellow in terminal
error "message"    # red in terminal
print("message")   # raw print (no extra styling)
```

---

## Standard Library

### JSON
```ox
let obj = json_parse('{"name":"OXM","v":2}')
say obj["name"]
say json_stringify(obj)
```

### YAML
```ox
let data = yaml_parse("name: OXM\nv: 2")
say yaml_stringify(data)
```

### XML
```ox
let root = xml_parse("<root><item>hello</item></root>")
say root["tag"]
say xml_stringify(root)
```

### CSV
```ox
let rows = csv_parse("name,age\nAlice,30\nBob,25")
say rows[1][0]   # "Alice"
say csv_stringify(rows)
```

### HTTP
```ox
let resp = http_get("https://httpbin.org/get")
say resp["status"]
let body = http_post("https://httpbin.org/post", json_stringify(#{"key":"value"}))
```

### SQLite
```ox
let db = db_open("data.sqlite")
db_exec(db, "CREATE TABLE IF NOT EXISTS users (id INTEGER PRIMARY KEY, name TEXT)")
db_exec(db, `INSERT INTO users(name) VALUES('Alice')`)
let rows = db_query(db, "SELECT * FROM users")
for row in rows
  say row["name"]
end
db_close(db)
```

### Regex
```ox
say regex_match("hello123", "\\d+")    # true
let hits = regex_find_all("a1b2c3", "\\d")   # ["1","2","3"]
say regex_replace("foo-bar-baz", "-", "_")   # "foo_bar_baz"
```

### File I/O
```ox
let text = read_file("data.txt")
write_file("out.txt", "content")
append_file("log.txt", "new line\n")
let output = shell("ls -la")
say output
```

### Environment
```ox
say cwd()
say env_get("HOME")
env_set("MY_VAR", "hello")
spawn("background_task")   # run fn in background thread
```

### Date & Time
```ox
let ts = now()             # Unix timestamp as float
say date_format(ts, "%Y-%m-%d %H:%M:%S")
let parsed = parse_date("2024-01-15", "%Y-%m-%d")
```

### Math
```ox
say sqrt(144.0)      # 12.0
say pow(2.0, 10.0)   # 1024.0
say abs(-42)         # 42
say floor(3.9)       # 3
say ceil(3.1)        # 4
say round(3.5)       # 4
say sin(0.0)         # 0.0
say cos(0.0)         # 1.0
let arr = [3,1,4,1,5]
say sum(arr)         # 14
say avg(arr)         # 2.8
```

### Collections
```ox
let a = [3, 1, 4, 1, 5, 9, 2, 6]
say sort_array(a)
say unique(a)
say map_array(a, |x| { x * 2 })
say filter_array(a, |x| { x > 3 })
say reduce_array(a, |acc,x| { acc+x }, 0)
```

### Browser / Clipboard / Notifications
```ox
browser_open("https://example.com")   # open URL
clipboard_write("copied text")
let text = clipboard_read()
notify("Title", "Message body")
```

---

## Testing

```ox
# Define test functions with test_ prefix
fn test_add()
  assert add(2, 3) == 5
  assert add(-1, 1) == 0
end

fn test_string()
  assert to_upper("hello") == "HELLO"
  assert len("abc") == 3
end
```

Run with: `oxm test script.ox`

---

## REPL Commands

```
oxm>  say "hello"        # evaluate expression
oxm>  let x = 42        # define variable (persists in session)
oxm>  fn f(a) … end     # define multi-line function
oxm>  help               # show help
oxm>  exit               # quit (also: quit, :q, Ctrl-D)
oxm>  clear              # clear screen
```

Multi-line blocks are detected automatically — type `end` to close.


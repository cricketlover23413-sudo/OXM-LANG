# OXM Language — Complete Cheatsheet

> OXM is a scripting language for automation, data, web, and AI.
> Comments use `--`. String interpolation: `"Hello {name}"`.

---

## 1. Variables & Types

```oxm
let x = 42
let pi = 3.14
let name = "OXM"
let flag = true
let nothing = nil

-- String interpolation
let msg = "Hello {name}, pi is {pi}"
say msg
```

**Types:** `int`, `float`, `string`, `bool`, `nil`, `list`, `map`

---

## 2. Output

```oxm
say "Hello, World!"           -- prints + newline
print "no newline"            -- no newline
say "value = {1 + 2}"        -- interpolation
```

---

## 3. Arithmetic

```oxm
say 10 + 3      -- 13
say 10 - 3      -- 7
say 10 * 3      -- 30
say 10 / 3      -- 3.333...
say 10 % 3      -- 1
say 2 ^ 8       -- 256
say abs(-5)     -- 5
say sqrt(16)    -- 4.0
say floor(3.7)  -- 3
say ceil(3.2)   -- 4
say round(3.5)  -- 4
say pow(2, 10)  -- 1024
say log(100)    -- 4.605...
say log10(100)  -- 2.0
say sin(0)      -- 0.0
say cos(0)      -- 1.0
say pi()        -- 3.14159...
say random()    -- 0.0..1.0
say rand_int(1, 6)    -- dice roll
say clamp(15, 0, 10)  -- 10
say lerp(0, 100, 0.5) -- 50.0
say sign(-3)          -- -1
say gcd(12, 8)        -- 4
say lcm(4, 6)         -- 12
```

---

## 4. Strings

```oxm
let s = "Hello, World!"
say len(s)                      -- 13
say upper(s)                    -- HELLO, WORLD!
say lower(s)                    -- hello, world!
say trim("  hi  ")              -- "hi"
say trim_start("  hi")          -- "hi"
say trim_end("hi  ")            -- "hi"
say contains(s, "World")        -- true
say starts_with(s, "He")        -- true
say ends_with(s, "!")           -- true
say replace(s, "World", "OXM")  -- Hello, OXM!
say split(s, ", ")              -- ["Hello", "World!"]
say join(["a","b","c"], "-")    -- a-b-c
say substr(s, 0, 5)             -- Hello
say index_of_str(s, "W")        -- 7
say repeat("ab", 3)             -- ababab
say reverse_str(s)              -- !dlroW ,olleH
say char_at(s, 0)               -- H
say char_code("A")              -- 65
say from_char_code(65)          -- A
say pad_left("5", 3, "0")       -- 005
say pad_right("hi", 5, ".")     -- hi...
say count_substr(s, "l")        -- 3

-- String → number
say int("42")       -- 42
say float("3.14")   -- 3.14
say to_str(100)     -- "100"
```

---

## 5. Lists (Arrays)

```oxm
let nums = [1, 2, 3, 4, 5]
say len(nums)               -- 5
say nums[0]                 -- 1
say nums[-1]                -- 5 (last)
push(nums, 6)               -- append 6
let last    = pop(nums)     -- removes last element
let removed = remove(nums, 0)       -- remove by index
say contains(nums, 3)               -- true
say index_of(nums, 3)               -- 2
say reverse(nums)                   -- [5,4,3,2,1]
say sort(nums)                      -- [1,2,3,4,5]
say sort_by(nums, "desc")           -- [5,4,3,2,1]
say flatten([[1,2],[3,[4,5]]])       -- [1,2,3,4,5]
say first(nums)                     -- 1
say last(nums)                      -- 5
say take(nums, 3)                   -- [1,2,3]
say drop(nums, 2)                   -- [3,4,5]
say insert_at(nums, 1, 99)          -- [1,99,2,3,4,5]
say remove_at(nums, 0)              -- [2,3,4,5]
say rotate(nums, 1)                 -- [2,3,4,5,1]
say unique(nums)                    -- deduplicated
say zip([1,2], ["a","b"])           -- [[1,"a"],[2,"b"]]
say unzip([[1,"a"],[2,"b"]])        -- [[1,2],["a","b"]]
say choice(nums)                    -- random element
say shuffle(nums)                   -- random order
say sample(nums, 3)                 -- 3 random elements
say sum(nums)                       -- 15
say product(nums)                   -- 120
say min_in(nums)                    -- 1
say max_in(nums)                    -- 5
say avg(nums)                       -- 3.0

-- Higher-order
let doubled = map(nums, fn(x) { x * 2 })
let evens   = filter(nums, fn(x) { x % 2 == 0 })
let total   = reduce(nums, fn(acc, x) { acc + x }, 0)
```

---

## 6. Maps (Dicts)

```oxm
let person = {"name": "Ali", "age": 30}
say person["name"]                  -- Ali
person["city"] = "Lahore"
say keys(person)                    -- ["name","age","city"]
say values(person)                  -- ["Ali",30,"Lahore"]
say entries(person)                 -- [["name","Ali"],...]
say has_key(person, "age")          -- true
delete(person, "city")
say len(person)                     -- 2
let merged = merge(person, {"lang": "OXM"})
let small  = pick(person, ["name"])         -- {"name":"Ali"}
let rest   = omit(person, ["age"])          -- {"name":"Ali"}
```

---

## 7. Control Flow

### if / elif / else
```oxm
if x > 10 {
    say "big"
} elif x > 5 {
    say "medium"
} else {
    say "small"
}
```

### match
```oxm
match x {
    1 { say "one" }
    2 { say "two" }
    _ { say "other" }
}
```

### Ternary
```oxm
let result = if x > 0 { "positive" } else { "negative" }
```

---

## 8. Loops

```oxm
-- Range loop
for i in 0..5 {
    say i
}

-- Step
for i from 0 to 10 step 2 {
    say i
}

-- Array loop
for item in ["a", "b", "c"] {
    say item
}

-- While
let i = 0
while i < 5 {
    say i
    i = i + 1
}

-- Loop control
break       -- exit loop
continue    -- next iteration
```

---

## 9. Functions

```oxm
fn greet(name) {
    return "Hello, {name}!"
}
say greet("OXM")

-- Default argument
fn add(a, b = 0) {
    return a + b
}

-- Lambda / anonymous
let square = fn(x) { x * x }
say square(5)   -- 25

-- Closures
fn counter() {
    let count = 0
    return fn() {
        count = count + 1
        return count
    }
}
let c = counter()
say c()   -- 1
say c()   -- 2
```

---

## 10. Error Handling

```oxm
try {
    let result = 10 / 0
} catch err {
    say "Error: {err}"
}

-- Throw custom error
error("something went wrong")

-- Re-throw
try {
    error("bad input")
} catch e {
    if contains(e, "bad") {
        say "handled: {e}"
    } else {
        throw e
    }
}
```

---

## 11. Classes / OOP

```oxm
class Animal {
    fn init(name, sound) {
        self.name  = name
        self.sound = sound
    }
    fn speak() {
        say "{self.name} says {self.sound}"
    }
}

class Dog extends Animal {
    fn init(name) {
        super.init(name, "Woof")
    }
    fn fetch() {
        say "{self.name} fetches the ball!"
    }
}

let d = Dog("Rex")
d.speak()
d.fetch()
say is_class(d)   -- true
```

---

## 12. Imports

```oxm
import "helpers"            -- loads helpers.ox from same dir
import "./utils/math"       -- relative path
```

---

## 13. File I/O

```oxm
-- Read
let txt   = read_file("data.txt")
let lines = read_lines("data.txt")

-- Write
write_file("out.txt", "Hello\n")
append_file("log.txt", "new line\n")

-- Check / delete / create
say file_exists("data.txt")     -- true/false
say dir_exists("myfolder")
say file_size("data.txt")       -- bytes
delete_file("temp.txt")
create_dir("myfolder")
delete_dir("myfolder")

-- List files
let files = list_dir(".")
let all   = list_dir_all(".")    -- recursive

-- Path helpers
say path_join("home", "user", "file.txt")  -- home/user/file.txt
say path_basename("home/user/file.txt")    -- file.txt
say path_dirname("home/user/file.txt")     -- home/user
say path_ext("file.txt")                   -- .txt
say path_abs("./data")                     -- absolute path
say path_exists("./data")
```

---

## 14. JSON & Data Formats

```oxm
-- JSON
let json_str = to_json({"a": 1, "b": [1,2,3]})
let data     = from_json(json_str)
say data["a"]

-- Save / load (auto-JSON)
save("config.json", {"theme": "dark"})
let cfg = load("config.json")

-- YAML
let y = parse_yaml("key: value\nnum: 42")
let s = to_yaml({"key": "value"})

-- CSV
let rows = parse_csv("a,b,c\n1,2,3")
let csv  = to_csv([["name","age"],["Ali",30]])

-- XML
let xml  = parse_xml("<root><item>1</item></root>")
let xstr = to_xml({"root": {"item": "1"}})
```

---

## 15. HTTP / Web

```oxm
-- GET — returns {status, body}
let r = http.get("https://httpbin.org/get")
say r["status"]   -- 200
say r["body"]

-- GET + auto-parse JSON body
let data = http.get_json("https://httpbin.org/json")
say data["slideshow"]["title"]

-- POST JSON — returns parsed JSON
let result = http.post_json("https://httpbin.org/post", {
    "name": "OXM",
    "version": 2
})
say result

-- PUT / DELETE
let r2 = http.put("https://api.example.com/item/1", {"name": "Updated"})
let r3 = http.delete("https://api.example.com/item/1")

-- Low-level (underscore style also works)
let r4 = http_get("https://example.com")
let r5 = http_post("https://example.com/api", "{\"key\":\"val\"}")
```

---

## 16. Shell & Process

```oxm
-- Fire-and-forget
shell("echo Hello")
shell("python script.py")

-- Capture output + exit code
let res = shell.run("git status")
say res["output"]   -- stdout (trimmed)
say res["stderr"]   -- stderr
say res["code"]     -- exit code (0 = success)

-- Environment
let home = env("HOME")
set_env("MY_VAR", "value")
let all  = env_all()          -- map of all env vars

-- Timing
sleep(1.0)      -- sleep N seconds
sleep(0.5)      -- 500ms
```

---

## 17. Database (SQLite)

```oxm
let db = db_open("app.db")

db_exec(db, "CREATE TABLE IF NOT EXISTS users (
    id   INTEGER PRIMARY KEY,
    name TEXT,
    age  INTEGER
)")

db_exec(db, "INSERT INTO users (name, age) VALUES ('Ali', 30)")

let rows = db_query(db, "SELECT * FROM users")
for row in rows {
    say "{row["name"]} is {row["age"]} years old"
}

db_close(db)
```

---

## 18. Regex

```oxm
let m   = regex_match("Hello World", "W\\w+")
say m          -- World

let all = regex_find_all("a1 b2 c3", "\\d+")
say all        -- ["1","2","3"]

let new = regex_replace("hello world", "o", "0")
say new        -- hell0 w0rld

say regex_test("user@email.com", "[\\w.]+@[\\w.]+\\.[a-z]+")  -- true
```

---

## 19. Date & Time

```oxm
let ts  = timestamp()              -- Unix seconds (float)
let ms  = time_ms()               -- Unix milliseconds (int)
let t   = time()                  -- Unix seconds (float)
let now = now()                   -- datetime string

say date_format(ts, "%Y-%m-%d")   -- 2025-06-16
say date_format(ts, "%H:%M:%S")   -- 14:30:00
say date_add(ts, 86400)           -- +1 day
say date_diff(ts1, ts2)           -- seconds between dates
say parse_date("2025-01-15", "%Y-%m-%d")
```

---

## 20. Hashing & Encoding

```oxm
-- Hash (pure Rust — no external crates)
say hash_md5("hello")             -- 5d41402abc4b2a76b9719d911017c592
say hash_sha1("hello")            -- aaf4c61ddcc5e8a2dabede0f3b482cd9aea9434d
say hash_sha256("hello")          -- 2cf24dba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7...
say hash("fnv1a", "test")         -- fast FNV-1a hash (hex)

-- Base64
say base64("Hello")               -- SGVsbG8=
say base64_decode("SGVsbG8=")     -- Hello

-- URL encoding
say encode_uri("hello world")     -- hello%20world
say decode_uri("hello%20world")   -- hello world
say url_encode("a=1&b=2")         -- a%3D1%26b%3D2
say url_decode("a%3D1%26b%3D2")   -- a=1&b=2
```

---

## 21. Desktop Notifications

```oxm
-- Windows: PowerShell balloon toast
-- macOS:   osascript display notification
-- Linux:   notify-send

notify("Alert", "Something happened!")
notify_send("Title", "Message")
notify_send_timeout("Warning", "Auto-dismisses in 3s", 3000)
```

---

## 22. Clipboard

```oxm
clipboard_write("text to copy")
let text = clipboard_read()
clipboard_clear()
```

---

## 23. Browser

```oxm
browser_open("https://example.com")   -- open in default browser
browser_wait(1.5)                      -- wait N seconds
browser_close()                        -- signal browser close
```

---

## 24. PC Automation

```oxm
mouse_move(500, 300)
mouse_click()
mouse_right_click()
mouse_double_click()
mouse_scroll(0, -3)
keyboard_write("Hello, World!")
keyboard_press("Return")
keyboard_press("Tab")
keyboard_shortcut("ctrl+c")
let sz = screen_size()
say "{sz["width"]}x{sz["height"]}"
```

---

## 25. File Watcher

```oxm
let h = watch_path(".", 500)   -- watch directory, poll every 500ms
sleep(5.0)
watch_stop(h)
```

---

## 26. Telegram Bot

```oxm
let TOKEN   = env("TELEGRAM_BOT_TOKEN")
let CHAT_ID = env("TELEGRAM_CHAT_ID")

-- Send plain text
telegram.send(TOKEN, CHAT_ID, "Hello from OXM!")

-- Send HTML
telegram.send_html(TOKEN, CHAT_ID, "<b>Bold</b> and <i>italic</i>")

-- Get new messages (polling loop)
let offset = 0
let updates = telegram.get_updates_offset(TOKEN, offset)
for u in updates {
    let msg_id = u["update_id"]
    let text   = u["message"]["text"]
    let cid    = to_str(u["message"]["chat"]["id"])
    telegram.send(TOKEN, cid, "You said: {text}")
    offset = msg_id + 1
}

-- Reply to a specific message
telegram.reply(TOKEN, CHAT_ID, message_id, "Replied!")

-- Delete / pin a message
telegram.delete(TOKEN, CHAT_ID, message_id)
telegram.pin(TOKEN, CHAT_ID, message_id)

-- Send a file / document
telegram.send_file(TOKEN, CHAT_ID, "report.pdf")

-- Set webhook URL
telegram.set_webhook(TOKEN, "https://myserver.com/webhook")

-- Answer inline keyboard callback
telegram.answer_callback(TOKEN, callback_query_id, "Done!")
```

---

## 27. Email (SMTP)

```oxm
let cfg = {
    "host":     "smtp.gmail.com",
    "port":     587,
    "user":     env("EMAIL_USER"),
    "password": env("EMAIL_PASS")
}

-- Plain text email
email.send(cfg, "to@example.com", "Subject here", "Body text here")

-- HTML email
email.send_html(cfg, "to@example.com", "Newsletter", "<h1>Hello!</h1><p>Body</p>")
```

**Note for Gmail:** Enable "App Passwords" in your Google account and use that as `EMAIL_PASS`.

---

## 28. Utilities

```oxm
-- Random IDs
say nanoid()       -- "V1StGXR8_Z5jdHi6B-myT"  (21 chars, URL-safe)
say nanoid(10)     -- 10-char ID

-- Random choice from array
say choice(["apple","banana","cherry"])

-- Type checks
say is_nil(nil)        -- true
say is_string("hi")    -- true
say is_int(42)         -- true
say is_float(3.14)     -- true
say is_bool(true)      -- true
say is_array([1,2,3])  -- true
say is_map({"a":1})    -- true
say is_class(MyObj)    -- true
say type_of("hello")   -- "string"

-- Terminal
clear()               -- clear the terminal screen
say time()            -- Unix timestamp as float
say time_ms()         -- milliseconds since epoch
say timestamp()       -- alias for time()
```

---

## 29. Testing

```oxm
fn assert_eq(a, b, label) {
    if a == b {
        say "[PASS] {label}"
    } else {
        say "[FAIL] {label}: expected {b}, got {a}"
    }
}

assert_eq(1 + 1,         2,    "addition")
assert_eq(upper("hi"),  "HI",  "upper case")
assert_eq(len([1,2,3]),  3,    "array length")
```

---

## 30. Quick Reference Card

| Task                    | OXM Code                                         |
|-------------------------|--------------------------------------------------|
| Print                   | `say "Hello {name}"`                             |
| Variable                | `let x = 42`                                     |
| If / else               | `if x > 0 { } else { }`                          |
| For range               | `for i in 0..10 { }`                             |
| For each                | `for item in list { }`                           |
| While                   | `while cond { }`                                 |
| Function                | `fn add(a, b) { return a + b }`                  |
| Lambda                  | `let f = fn(x) { x * 2 }`                        |
| Class                   | `class Foo { fn init(x) { self.x = x } }`        |
| Try / catch             | `try { } catch e { say e }`                       |
| HTTP GET JSON           | `http.get_json("https://api.example.com")`        |
| HTTP POST JSON          | `http.post_json(url, {"key":"val"})`              |
| Shell command           | `shell.run("git status")["output"]`               |
| Read file               | `read_file("data.txt")`                           |
| Write file              | `write_file("out.txt", content)`                  |
| JSON parse              | `from_json(str)`                                  |
| SQL query               | `db_query(db, "SELECT * FROM t")`                 |
| Telegram message        | `telegram.send(token, chat_id, "msg")`            |
| Send email              | `email.send(cfg, to, subject, body)`              |
| Desktop notification    | `notify_send("Title", "Body")`                    |
| Hash SHA-256            | `hash_sha256("data")`                             |
| Generate ID             | `nanoid()`                                        |
| Random choice           | `choice(["a","b","c"])`                           |
| Flatten list            | `flatten([[1,2],[3,4]])`                          |
| Merge maps              | `merge(map1, map2)`                               |
| Filter list             | `filter(list, fn(x) { x > 0 })`                  |
| Map list                | `map(list, fn(x) { x * 2 })`                     |
| Reduce list             | `reduce(list, fn(acc,x) { acc+x }, 0)`            |

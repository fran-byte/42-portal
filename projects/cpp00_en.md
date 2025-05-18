---
layout: default
title: "fran-byte 42 Madrid"
---

## 🔹 CPP00 – Introduction to C++ and Object-Oriented Programming

### 📌 Objective:

Introduce the basic concepts of C++: **classes**, **member functions**, **streams**, **const**, **static**, and initialization lists. Emphasis on object-oriented styles following the C++98 standard.

---

## 📁 ex00 – Megaphone

### 🎯 Goal:

* Write a program that converts input to **uppercase**.

### 📦 Details:

* Files: `megaphone.cpp`, `Makefile`
* Input: command-line arguments
* Output:

  * If no arguments: `* LOUD AND UNBEARABLE FEEDBACK NOISE *`
  * If there are arguments: print them in uppercase

```bash
$> ./megaphone Hello there
HELLO THERE
```

### 🧠 Useful Concepts:

* Using `std::string`, `std::toupper` (cctype)
* Iterating through strings with `for` loops
* Using `argc` and `argv[]`

---

## 📁 ex01 – My Awesome PhoneBook

### 🎯 Goal:

Create an interactive **contact book** with a maximum of 8 contacts, allowing the user to:

* Add (`ADD`)
* Search (`SEARCH`)
* Exit (`EXIT`)

### 📦 Details:

* Files: `*.cpp`, `*.hpp`, `Makefile`
* Two classes:

  * `PhoneBook`: manages contacts (static array of 8)
  * `Contact`: stores info for each contact

### 🧠 Considerations:

* If a 9th contact is added, it replaces the oldest one
* Fields: first name, last name, nickname, phone number, darkest secret
* Output table should truncate strings >10 characters with a trailing `.`

```bash
$> ./phonebook
ADD
SEARCH
EXIT
```

### 🔧 Useful Resources for Implementation:

* `std::string`, `std::getline()`
* `std::setw`, `std::right`, `std::left`, `std::cout`
* `stringstream` for formatting and truncating strings
* Basic input validation and `while` loops to keep the program running

### 🧩 Design Suggestion:

* `Contact` class: simple setters and getters for each field
* `PhoneBook` class: array of 8 contacts + cyclic index for replacement
* `displayTable()` method for SEARCH format and `displayDetails()` to show full contact info

---

## 📊 General Tips

* Always compile with:

```bash
c++ -Wall -Wextra -Werror -std=c++98
```

* Use meaningful names and UpperCamelCase format for classes
* Do not implement functions in headers (except for templates)
* Avoid memory leaks: use `delete` correctly (although this module doesn’t use `new`/`delete`)

---

## 📚 Resources

* [cplusplus.com](https://cplusplus.com/)
* [cppreference.com](https://en.cppreference.com/)
* `man string`, `man iomanip`, `man ctime`

---

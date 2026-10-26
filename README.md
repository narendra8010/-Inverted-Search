# Inverted Search

A command-line **inverted index** search tool written in **C**. It reads a set of text files, builds a database that maps every word to the files it appears in (and how many times), and lets you search, display, update and save that database.

An inverted index is the core idea behind search engines: instead of asking "which words are in this file?", it answers "which files contain this word?" quickly.

---

## Features

- Validate input files (existence, extension, non-empty, no duplicates)
- **Create** the database from one or more text files
- **Display** the full database
- **Search** for a word and see which files contain it and how many times
- **Update** the database by adding new files
- **Save** the database to a file so it can be reloaded later
- Hash table with linked lists for fast lookups

---

## Project Structure

```
.
├── inverted.h            # Structures, macros and function prototypes
├── main.c                # Entry point, menu and program flow
├── read_and_validate.c   # Command-line argument and file validation
├── create_database.c     # Builds the inverted index from the files
├── display_database.c    # Prints the database
├── search_database.c     # Searches for a word
├── update_database.c     # Adds new files to an existing database
├── save_database.c      # Writes the database to a file
├── file1.txt             # Sample input file
├── file3.txt             # Sample input file
└── README.md
```

---

## How It Works

1. Input files are passed as command-line arguments and validated.
2. Valid file names are stored in a linked list.
3. Each file is read word by word. Every word is hashed (by its first character) into a hash table.
4. Each table entry holds a linked list of **main nodes** (one per unique word), and each main node points to a list of **sub nodes** (one per file containing that word, with a word count).
5. Searching a word jumps straight to its bucket, then walks that short list.

```
Hash index → [ word | file_count ] → [ file1.txt | 2 ] → [ file3.txt | 1 ]
```

---

## Getting Started

### Prerequisites

- GCC (or any C compiler)
- Linux, macOS, or Windows with MinGW/WSL

### Build

```bash
git clone https://github.com/narendra8010/-Inverted-Search.git
cd -- -Inverted-Search
gcc *.c -o main
```

### Run

```bash
./main file1.txt file3.txt
```

---

## Usage

After launching, choose from the menu:

| Option | Operation        | Description                                   |
|--------|------------------|-----------------------------------------------|
| 1      | Create Database  | Build the index from the validated files      |
| 2      | Display Database | Show every word with its files and counts     |
| 3      | Search Database  | Enter a word to find which files contain it   |
| 4      | Update Database  | Add more files to the existing database       |
| 5      | Save Database    | Store the database in a file                  |
| 6      | Exit             | Quit the program                              |

### Example

```
$ ./main file1.txt file3.txt
Enter your choice: 1
Database created successfully.

Enter your choice: 3
Enter the word to search: hello
Word "hello" is present in 2 file(s):
  file1.txt : 3 time(s)
  file3.txt : 1 time(s)
```

---

## Concepts Used

- Hash tables
- Singly linked lists (nested main-node / sub-node structure)
- File handling in C
- Command-line arguments
- Dynamic memory allocation
- Multi-file C projects and header files

---

## Possible Improvements

- Case-insensitive search
- Phrase and multi-word queries
- Load a previously saved database on startup
- Add a `makefile`
- Free all allocated memory on exit

---

## Author

**Narendra**
GitHub: [@narendra8010](https://github.com/narendra8010)

---

## License

This project is open source and available for learning and educational use.

# Day 06 - Linux File I/O Practice

## What I Practiced

Today I practiced basic Linux file read and write commands.
I learned how to create a file, write text, append text, and read the file.

## 1. Create a File

I created an empty file named `notes.txt`.

```bash
touch notes.txt
```

## 2. Write the First Line

I used `>` to write the first line to the file.

```bash
echo "Line 1" > notes.txt
```

The `>` operator writes to the file and replaces existing content.

## 3. Append the Second Line

I used `>>` to add another line without deleting the existing content.

```bash
echo "Line 2" >> notes.txt
```

The `>>` operator appends text to the end of the file.

## 4. Use tee

I used `tee` to display the text and append it to the file.

```bash
echo "Line 3" | tee -a notes.txt
```

The `-a` option appends the text to the file.

## 5. Read the File

I used `cat` to read the complete file.

```bash
cat notes.txt
```

This displayed all the lines stored in `notes.txt`.

## 6. Read the First Two Lines

I used `head` to view the beginning of the file.

```bash
head -n 2 notes.txt
```

This displayed the first two lines.

## 7. Read the Last Two Lines

I used `tail` to view the end of the file.

```bash
tail -n 2 notes.txt
```

This displayed the last two lines.

## What I Learned

- `touch` creates an empty file.
- `>` writes or replaces file content.
- `>>` appends content to a file.
- `tee` can display and write text at the same time.
- `cat` reads the complete file.
- `head` reads the beginning of a file.
- `tail` reads the end of a file.

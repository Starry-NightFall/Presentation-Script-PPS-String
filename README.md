# Strings in C — Group Presentation

## Topic Breakdown

| Member       | Subtopic                                                                                        |
| ------------ | ----------------------------------------------------------------------------------------------- |
| **Person 1** | What is a String? — Declaration, Initialization & How Strings Work in Memory                    |
| **Person 2** | Reading & Displaying Strings + Common String Functions (`strlen`, `strcpy`, `strcat`, `strcmp`) |
| **Person 3** | String as Array of Characters + Practical Examples & Common Mistakes                            |

<br>
<br>
<br>

---

<details>
<summary>Person 1 — "What is a String & How It Works"</summary>

Good morning/afternoon, everyone!

Let's start from the very beginning — **what is a String in C?**

In everyday life, whenever we write a name, a sentence, or even a password — that's a string. In C programming, a **string is simply a sequence of characters stored together**. For example, the word _"Hello"_ is a string made up of 5 characters: H, e, l, l, o.

Now, here's something really important that makes C strings unique — **C doesn't have a built-in string data type** like some other languages. Instead, C uses a **character array** to store strings. So when we write a string, we're actually storing it as an array of `char` values.

Let's look at how we **declare and initialize** a string in C:

```c
char name[6] = "Hello";
```

We declared an array of 6 characters — but wait, "Hello" only has 5 letters, right? So why 6?

This is where the magic happens. In C, every string ends with a special character called the **null character**, written as `\0`. This tells the computer: _"Hey, the string ends here."_ Without it, C wouldn't know where the string stops in memory.

So in memory, _"Hello"_ is actually stored as: **H, e, l, l, o, \0** — that's 6 characters total.

You can also initialize a string like this:

```c
char name[] = "Hello";
```

Here, C **automatically calculates** the size and adds the null character for you. This is the most common and convenient way.

Another way — though a bit more manual — is to write each character separately:

```c
char name[] = {'H', 'e', 'l', 'l', 'o', '\0'};
```

Notice that here, we **must** manually add `'\0'` at the end. If we forget it, the string becomes invalid and we might get garbage values when printing it.

So to summarize what I covered:

- A string in C is a **character array**
- It always ends with a **null character `\0`**
- We can initialize it with double quotes or character by character

Now my teammate will show you how to actually **read and display** these strings, and some powerful built-in functions C gives us to work with them. Over to you!

</details>

---

<details>
<summary>Person 2 — "Reading, Displaying & String Functions"</summary>

<details>
<summary>Slide 7</summary>
Thanks! So now that we know what a string is and how it's stored, let's talk about how we actually **use** strings — how to take input, show output, and use some really helpful built-in functions.
</details>

<details>
<summary>Slide 8</summary>

To **print** a string in C, we use `printf` with the `%s` format specifier:

```c
printf("%s", name);
```

Simple enough! But how do we **take a string as input** from the user?

The most basic way is using `scanf`:

```c
scanf("%s", name);
```

But there's a catch — `scanf` **stops reading at a space**. So if you type _"John Doe"_, it will only store _"John"_.

To read a **full line including spaces**, we use `fgets`:

```c
fgets(name, sizeof(name), stdin);
```

This is safer and more practical for real-world input.

</details>

<details>
<summary>Slide 9</summary>

Now let's talk about **string functions** — C gives us a special library called `string.h`. Once we include it at the top, we get access to very powerful tools.

</details>

<details>
<summary>Slide 10</summary>
**First: `strlen()`** — this gives us the **length** of a string, not counting the null character.

```c
strlen("Hello"); // returns 5
```

**Second: `strcpy()`** — this **copies** one string into another.

```c
strcpy(dest, src); // copies src into dest
```

We can't just do `dest = src` with strings in C — that won't work. `strcpy` is the right way.

</details>

<details>
<summary>Slide 11</summary>
**Third: `strcat()`** — this **joins** two strings together, also called concatenation.
```c
strcat(str1, str2); // adds str2 at the end of str1
```

**Fourth: `strcmp()`** — this **compares** two strings. If they're equal, it returns 0. If not, it returns a non-zero value.

```c
strcmp("apple", "apple"); // returns 0 → they are equal
```

</details>

<details>
<summary>Slide 12</summary>
These four functions are the ones we will use most frequently in C string programming.

So to recap:

- Use `printf` / `scanf` / `fgets` to display and read strings
- `strlen`, `strcpy`, `strcat`, `strcmp` — these are your **best friends** from `string.h`

Next, my teammate will walk you through strings as arrays in more depth, some hands-on examples, and the most common mistakes beginners make. Take it away!

</details>

</details>

---

<details>
<summary>Person 3 — "Strings as Arrays, Examples & Common Mistakes"</summary>

Thanks! Let's now go a little deeper and connect the dots — because understanding strings as **arrays of characters** is what really makes everything click.

We said strings are character arrays. That means we can **access each character individually** using an index, just like a regular array.

```c
char name[] = "Hello";
printf("%c", name[0]); // prints 'H'
printf("%c", name[4]); // prints 'o'
```

Indexing starts at 0, so `name[0]` is the first character, `name[1]` is the second, and so on.

We can also **loop through a string** to process it character by character:

```c
for (int i = 0; name[i] != '\0'; i++) {
    printf("%c\n", name[i]);
}
```

This loop goes through each character **until it hits the null character** — which is exactly how C knows the string is over. This is a very common and useful pattern.

Now, let me show you a **practical example** — counting how many vowels are in a string:

```c
int count = 0;
for (int i = 0; name[i] != '\0'; i++) {
    char c = name[i];
    if (c=='a' || c=='e' || c=='i' || c=='o' || c=='u')
        count++;
}
printf("Vowels: %d", count);
```

Simple, clean, and very practical!

Now let's talk about **common mistakes** — because these trip up almost every beginner:

**Mistake 1: Forgetting `\0` when initializing manually.**
If you don't add the null character at the end, `printf` will keep reading memory beyond your string and print garbage or crash.

**Mistake 2: Array too small.**
If you declare `char name[5]` and try to store `"Hello"` — that's 5 letters + 1 null = 6 characters — you'll overflow the array. Always make your array **at least one size bigger** than your string.

**Mistake 3: Using `==` to compare strings.**

```c
if (str1 == str2)      // ❌ WRONG — compares memory addresses, not content
if (strcmp(str1, str2) == 0)  // ✅ CORRECT
```

Always use `strcmp()` for comparing strings. This is one of the most common bugs beginners write.

**Mistake 4: Using `=` to copy strings.**

```c
str1 = str2;           // ❌ WRONG
strcpy(str1, str2);    // ✅ CORRECT
```

So to wrap up our entire presentation:

- Strings are **character arrays** ending with `\0`
- We can read, print, and manipulate them with `scanf`, `fgets`, `printf`
- `string.h` gives us powerful functions like `strlen`, `strcpy`, `strcat`, `strcmp`
- And always watch out for the **common mistakes** — null terminator, array size, and never use `==` or `=` directly on strings

Thank you so much for listening! We hope this gave you a solid understanding of Strings in C.

</details>

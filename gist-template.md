# Regex Tutorial - Matching an Email

In this tutorial we will go over regular expressions (also known as regex). You may have encountered regex before and it can appear intimidating to look at. This is because at first glance it doesn't follow any specific pattern but as you will soon learn there is not need to panic and next time you encounter regex you'll know exactly what the code is trying to accomplish.

## Summary

The code below will be used as an example and is used to find Email addresses. In this tutorial we will also go over the following topics: Anchors, Quantifiers, OR Operators, Character Classes, Flags, Grouping and Capturing, Bracket Expressions, Greedy and Lazy Match, Boundries, Back-references, as well as Look-ahead and Look-behind.

**Example Code**

```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```

The above code is used to check for emails.

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)

## Regex Components

Regex is considered a literal and must be wrapped in `/`.

```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```

Notice how the first and last characters are both `\`.

Now let's take a look at the components that make up regular expressions.

### Anchors

These two characters are considered anchors.

```
^ and $
```

Firstly we will go over the `^` anchor. The `^` anchor looks for matching characters that appear **after** the anchor. However, it is important to remember that Regex is case sensitve. This means the string "Bird" and the string "bird" will not match. Of Course words or phrases that contain "Bird" such as "Bird brain" will also be considered a match.

Next we will go over `$`. The `$` anchor checks for matches that come before it. Once again Regex is case sensitive so please be mindful when attempting to check for matches utilizing either anchors.

Let's take a look at our example code.

```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```

We can see both achors being used at the beginning and end of the code respectivly.

### Quantifiers

With qunatifiers we can set the minimum length and maximum length of the string.
Quantifies are considered **"greedy"** meaning they will match as many occurences as possible.

- `*` Matches the pattern zero or more times.
- `?` Mathces the pattern zero or more times.
- `+` Matches the pattern one or more times.

With curly brackets (`{}`) we have three different ways to set limits for a match.

- `{ n }` Matches **exaclty** n times.
- `{ n, }` Matches **at least** n times.
- `{ n, x }` Matches **at least** n times and a maximum of x times.

Looking at our Email example.

```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```

We can see the the quantifiers towards the end of our example `{2,6}` is looking for a minimum string length of two and a maximum length of six.

### OR Operator

When using bracket expressions (`[]`) a string does not need to fit **all** the contraights, it only needs to comply to **at least** one. We will go over bracket expressions more in a bit. However, we are also able to match a string based on multiple patterns (such as `this` or `that`). We are able to accomplish this with the OR operator (`|`).

While our Email example does not use the OR operator here is another example to help demonstraight the uses for the OR operator.

```
hi|hello
```

The above example will match strings with either `hi` or `hello` within them.

### Character Classes

Character classes define the characters that can occur within a givin match.
Below are some character classes.

- `.` Matches all characters with the exception of characters on a newline (`\n`)
- `\d` Matches any number and is equivalent to bracket expression `[0-9]`.
- `\w` Matches any alphanumeric character including the underscore (`_`). and is the same as saying `[a-zA-z0-9]`.
- `\s` Matches a single whitespace character (including tabs and line breaks).

If you change any of the last three options to a capital letter instead you can match the inverse character. For example, `\W` will match a non-alphanumeric character.

Our Email example utilizes `\d` specifically.

```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```

After the `@` the lines `([\da-z\.-])` are using `\d` to say we will accept any number.

### Flags

While regex is a literal and must be wrapped in slash characters, the only exception to this rule are known as **flags**.

- `g` is a **global search**. The regex should test all possible matches in given string.
- `i` represents **case-insenitive** meaning it will not discreminate based on uppercase or lowercase.
- `m` is a **multi-line** search and the string will be treated as multiple lines.

Even though our Email example does not contain any flags to demonstraight these concepts they are still important to know incase you encounter them on another project.

### Grouping and Capturing

The two main categories of grouping are known as **caturing** and **non-capturing**.
**Capturing groups** capture the matches with the intent to re-use them later and **non-capturing** do not.

Often you may need to break up sections of a string to check parts of it individualy that is where grouping comes into play. The most common way to group sections of a string are with parentheses (`()`). The section within each parentheses are known as **subexpressions**.

Our Email example makes use of grouping by creating three subexpressions

```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```

In order they are `([a-z0-9_\.-]+)` , `([\da-z\.-]+)` , and `([a-z\.]{2,6})`.
Since we know that we're looking for an Email we can assume that since each subexpression is broken up with an `@` and a `.` respectivly that each subexpression is looking for various valid ways to define an Email.

### Bracket Expressions

Bracket Expressions are denoted by brackets (`[]`) and are also refered to as **Positive Character Group**.

The `[]` represent a range of characters that we would like to include in our match.

- `[0-9]` Will seach for any **number** between 0 and 9 within a string.
- `[a-z]` Will search for any **letter** that is **lowercase only**.
- `[A-Z]` Will search for any **letter** that is **Uppercase only**.
- `[_-]` Will allow the strings to contain **underscores** as well as **hyphens**.
  It is worth noting that the `-` in `[_-]` does not represent a range like it does in any of the prior expressions.
- `\` The backslash is known as a **Character Escape**. This allows you to search for characters reserved for other purposes.

In order to find a mix of uppercase and lowercase letters we can simply combine the two expressions like so `[a-zA-z]`. Furthermore, `[a-zA-Z0-9_-]` will be able to find any uppercase or lowercase letter, any number, and can include hyphens as well as underscores. It is important to remember that the string that is matched does **NOT** have to meet all the requirements within the range, it only needs to meet at least one.

For example if we used `[a-z0-9_-]` then `"3p1c g4m3r"` will be considered a match because it contains lowercase letters as well as numbers even though it does not contain either an underscore or a hyphen.

When looking at our Email Example

```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```

The first section `[a-z0-9\.-]` searches for any letter, number, underscore, and also uses `\` to include the character `.` whithin the search.

Here are a few examples for valid searchs.

```
"._."
"123"
"abcABC"
"Se7en"
"H3ll0_W0r1d"
```

### Greedy and Lazy Match

**What does "Greedy" and "Lazy" mean?**

"Greedy" and "Lazy" refer to the amount of occurrences the regex will match.

- `Greedy` will match as many occurrences as possible.
- `Lazy` will match as few as possible.

For further information on greedy and lazy matches refer to the [quantifiers](#quantifiers) section.

### Boundaries

Boundries refer to __where__ relative to the current position can match.

__Word boundries__ (`\b`) are useful when you want to match a sequence of characters on thier own to match sure they occure at either the beginning or at the end of a sequence of characters.

__Not-a-word boundaries__ (`\B`) is less likely to be used as it will match when either neither side is a word character (`$=(@-%+)`) or when both sides are a word character.

### Back-references

Earlier we went over capturing group matching and we mentioned that the matches could be saved for later and `Back-references` are what those saved matches are refered to as. Capturing groups count starting at 1 so the first saved result could be accessed with `\1`.

### Look-ahead and Look-behind

Lastly we will go over __Look-ahead__ and __Look-behind__ assertion. Regex typically will search for matches from left to right (hints the naming of "look-ahead" and "look-behind").

For the following section `pattern` will refer to anything you may use in a regex literal.

- `(?=pattern)` must match the text after the current position and the position cannot be changed.
- `(?!pattern)` negates the assertion, it will succeed if the pattern doesn't match the current position.


## Author

Keep up with me by following my GitHub at [clayguerrero](https://github.com/clayguerrero)

Until next time, take care and see you soon!

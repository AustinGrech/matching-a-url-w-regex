# Regex Tutorial - Matching URLs with Regular Expressions

Welcome to the Regex Tutorial for matching URLs! In this tutorial, we will explore the power of regular expressions in validating and matching URLs. Regular expressions provide a flexible and efficient way to identify and manipulate URLs. Whether you are working with URLs in web development, data extraction, or any other application, this tutorial will guide you in constructing effective regex patterns for URL matching.

## Summary

In this tutorial, we will focus on constructing a regex pattern to match URLs that adhere to specific criteria. The regex pattern we will be using is:

```
/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/
```

We will break down this pattern and explain its components, including protocols, domain names, paths, and more. By the end of this tutorial, you will have a solid understanding of how to use this regex pattern to validate and extract different parts of a URL.

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)
- [Author](#author)

# Regex Components

## Anchors

The characters `^ and $` are both considered to be anchors in regular expressions. In the context of the regex pattern

```
/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/
```

they serve specific purposes.

The `^` anchor, when placed at the beginning of the pattern, signifies that the string being matched must start with the characters that follow it. In our URL matching regex, `^` is used at the very beginning to ensure that the string starts with the specified pattern. This pattern allows for an optional protocol component, denoted by `(https?:\/\/)?`.

On the other hand, the `$` anchor, when placed at the end of the pattern, signifies that the string being matched must end with the characters that precede it. In our URL regex, the `$` anchor is not explicitly used. This is because the pattern does not enforce any specific characters at the end of the URL. Instead, it allows for optional trailing components, such as the path, denoted by `([\/\w \.-]_)_\/?`.

In summary, the regex pattern `/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]_)_\/?$/` ensures that the string being matched starts with an optional protocol component and adheres to the specified structure for URLs. However, it does not enforce any specific characters at the end of the URL.

## Quantifiers

Quantifiers are an important aspect of regular expressions `that allow you to define the number of occurrences of a pattern`. They specify the minimum and maximum number of times a pattern should be matched.

In the given regular expression for matching a URL, let's break it down and examine the quantifiers used:

```
/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]_)_\/?$/
```

The first quantifier we encounter is the `"?"` after the group (https?:\/\/). This makes the preceding pattern, `"s?"`, match zero or one time. It indicates that the `"s"` character is optional and allows for URLs starting with `"http://"` or `"https://"`.

The next quantifier appears after the bracket expression `([\da-z\.-]+)`. The `"+"` symbol means that the preceding pattern should be matched one or more times. This pattern matches any combination of digits, lowercase letters, dots, and hyphens in the domain name.

After that, we have the quantifier `{2,6}` following the bracket expression `([a-z\.])`. This quantifier specifies that the preceding pattern should match between 2 and 6 times. This pattern matches the top-level domain (TLD) of the URL, which consists of lowercase letters and dots.

Moving on, we find another quantifier `([\/\w \.-]\_)_` after the TLD. The `"_"` symbol denotes that the preceding pattern can match zero or more times. This pattern matches any combination of forward slashes, word characters, spaces, dots, and hyphens, which could represent additional path or query parameters in the URL.

Finally, we have the `"?"` after the forward slash `(/)` at the end of the regex. This makes the preceding pattern, `"\/?"`, match zero or one time, allowing for URLs with or without a trailing slash.

To summarize, this regular expression aims to match URLs with various components. Here are some examples to illustrate its usage:

- `"http://example.com"` is a match because it starts with `"http://"` (where the `"s"` is optional), followed by `"example"` in the domain name and `".com"` as the TLD.
- `"https://www.example.com/page"` is a match because it starts with `"https://"`, includes `"www"` in the domain name, `".example"` as the TLD, and `"/page"` as an additional path.
- `"ftp://ftp.example.com"` is not a match because the `"ftp://"` protocol is not included in the regex pattern.
- `"https://example.com/file.html?param=value"` is a match because it starts with `"https://"`, has `"example"` in the domain name, `".com"` as the TLD, `"/file.html"` as the path, and `"?param=value"` as query parameters.

Regular expressions offer numerous possibilities and advanced features beyond what we've covered here. This introduction should provide you with a foundation for understanding how quantifiers are used in the context of matching URLs.

## Grouping Constructs

Grouping constructs are used in regular expressions to break down the expression into subexpressions, allowing you to evaluate different sections of a string separately. In the context of matching a URL, grouping constructs can be helpful to handle different components of the URL.

Let's consider the original regular expression for matching a URL:

```
/^(https?://)?([\da-z.-]+).([a-z.]{2,6})([/\w .-])/?$/
```

To add grouping constructs for better organization and handling of different URL components, we can modify the expression as follows:

```
/^(https?://)?([\da-z.-]+).([a-z.]{2,6})([/\w .-]\_)?/?$/
```

Now, let's break down the modified expression:

- `(https?://)?` This grouping construct captures the optional part of the URL that starts with `"http://"` or `"https://"`. The `"?"` quantifier makes the preceding pattern match zero or one time, allowing URLs to have or omit the `"https://"` prefix.

- `([\da-z.-]+)` This grouping construct captures the domain name section of the URL. It matches any combination of alphanumeric characters, dots, and hyphens in the domain name.

- `([a-z.]{2,6})` This grouping construct captures the top-level domain (TLD) of the URL. It matches between 2 and 6 lowercase letters or dots, representing TLDs like `".com"`, `".org"`, or `".co.uk"`.

- `([/\w .-]\_)?` This grouping construct captures the optional additional path or query parameters in the URL. It matches any combination of forward slashes, word characters, spaces, dots, and hyphens. The `"?"` quantifier makes this section match zero or one time, allowing URLs with or without additional path/query parameters.

- `/?$` This part of the expression matches the trailing slash at the end of the URL, if present. The `"/?"` pattern matches zero or one forward slash, and `"$"` denotes the end of the string.

By using grouping constructs, we can better organize and handle different parts of the URL within the regular expression, allowing for more flexible URL matching patterns.

## Bracket Expressions

In the context of the URL matching pattern, let's break down the bracket expressions used:

- `[\da-z.-]` Matches any digit (\d), lowercase letter (a-z), dot (.), or hyphen (-).

- `[a-z.]` Matches any lowercase letter (a-z) or dot (.) character.

- `[/\w .-]` Matches a forward slash `(/)`, word character `(\w)`, space `( )`, dot `(.)`, or hyphen `(-)`.

These bracket expressions define the valid characters that can occur at specific positions within the URL pattern. By combining these expressions with other components of the regex, we can construct a pattern that matches URLs with specific characteristics.

For example, the expression `[a-z.]` allows lowercase letters and dots to appear in the domain name. The expression `[/\w .-]` allows for a combination of forward slashes, word characters, spaces, dots, and hyphens to appear in the path or query part of the URL.

Remember that these bracket expressions specify the characters we want to include, and they can be customized or expanded as needed to match the desired pattern.

## Character Classes

A character class in a regex defines a set of characters, any one of which can occur in an input string to fulfill a match. In the given regex expression `/^(https?://)?([\da-z.-]+).([a-z.]{2,6})([/\w .-])/?$/`, we can observe the usage of character classes as follows:

- `\d` - Matches any Arabic numeral digit. In the regex, `[\da-z.-]+` matches one or more occurrences of digits, lowercase letters, dots, and hyphens in the domain name.
- `\w` - Matches any alphanumeric character from the basic Latin alphabet, including the underscore `(\_)`. In the regex, `[/\w .-]\*` matches zero or more occurrences of forward slashes, word characters, spaces, dots, and hyphens, representing additional path or query parameters in the URL.
- `\s` - Matches a single whitespace character, including tabs and line breaks. However, this character class is not utilized in the given regex expression.

## The OR Operator

The OR operator `|` is used to specify alternatives. In the URL pattern, the OR operator is used in `(https?:\/\/)` to match either `http://` or `https://`. We will discuss how the OR operator expands the matching options in the pattern.

## Flags

Flags in a regex provide additional functionality or limits. In the given regex expression `/^(https?://)?([\da-z.-]+).([a-z.]{2,6})([/\w .-])/?$/`, we don't have any flags specified at the end of the regex.

However, flags can be added after the closing slash `(/)` to modify the regex behavior. Commonly used flags include:

- `g:` Global search - Tests the regex against all possible matches in a string, not just the first match.
- `i:` Case-insensitive search - Ignores case sensitivity while attempting a match in a string.
- `m:` Multi-line search - Treats a multi-line input string as multiple lines, affecting the behavior of anchors like `^` and `$`.
  You can add these flags after the closing slash `(/)` if you need these specific functionalities in your regex.

## Character Escapes

In regular expressions, the backslash `(\)` serves as an escape character that changes the interpretation of the following character. It allows you to match special characters literally instead of their usual regex interpretation. Let's consider a few examples:

The open curly brace `({)` is a special character used to define quantifiers. However, if you want to search for an actual open curly brace character, you can escape it by adding a backslash before it, like this: `\{`. This ensures that the regex treats it as a literal character instead of a quantifier.

Similarly, if you want to search for a literal backslash character `(\)`, you need to escape it by adding another backslash before it, like this: `\\`. Otherwise, the backslash would be interpreted as an escape character itself.

It's important to note that within bracket expressions (character classes), such as `[abc]`, most special characters lose their special significance and are matched literally. So, inside bracket expressions, you don't need to escape characters like the backslash `(\)` or the open curly brace `({)`.

In the given URL matching regular expression `/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`, you can see the use of character escapes. For example, the forward slashes `(/)` in `https?:\/\/` are escaped as `\/` to match them literally. Similarly, the dot `(.)` in `[\da-z\.-]` is escaped as `\`. to match a dot character.

By understanding character escapes, you can control the interpretation of special characters and search for them literally within a regular expression.

## Author

This tutorial is authored by Austin Grech, visit [Author's GitHub Profile](https://github.com/AustinGrech?ocid=AIDcmmofjgdhvp_SEM_9ea367851483185b0bb5041a2c50f282:G:s).

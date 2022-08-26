Hello, my name is Nikolay Kovzik, and today i will tell you about regular expressions.
Regular expressions are a powerful tool for searching and replacing within a string or file, and for validation.
You can use them when writing code, in tests, when working on the command line, even when searching in your code editor, IDE or file manager.
A regular expression (aka "regexp", "regular" or just "reg", sometimes referred to as rational expression) consists of a search pattern and optional flags. Here are examples of some of them
pattern is a formula by which the regular expression engine will look for matches in a string. It is a sequence of characters between slashes.
flags are characters after the last slash that allow you to change the behavior of regular expressions and search rules in a string.
using the first regex we can count how many times Marie's name appears in a text
using the second regular expression, we can find this number in the number series
using the third regular expression, we can find time-like templates
with this regular expression we can validate emails
and using last regular expression we can validate the phone numbers
Regexp is notoriously difficult to read because its syntax looks like a bunch of unrelated characters. the last examples look complicated and confusing, but a little later you will better understand what is happening here.

Let's start with easy examples to get an idea of what regular expressions are. The wonderful site regexp.com will help us, you can easily find analogues of it on the Internet. I will leave the link in the sources. It’s super useful, because it highlights text you are looking for with specific regular expression.
I remind you that regexp allow you to search through a text in a really advanced way. We have text here, and at the top we have regular expression between two slashes. After forward slash at the end, we specify various flags, there is not a single flag here yet. And the main one that you need to know about is “g” or “global”. Since it is missing here, only one match was found in the text. 
But if we add it, then the regular expression engine will find not only the first, but also all matches in the text. 
Note that now engine mathes characters literally. Our search is case-sensitive. And words that begin with a capital letter are not highlighted.

In order to fix this, we will add another flag “i”, which means case-insensitive. And now, as you can see, both uppercase and lowercase matches are highlighted. 
There are many characters in the regular expression syntax that have special meaning. Some of them even have more than one meaning. Examples of such symbols are the caret and the dollar. The caret matches at the beginning of the text, and the dollar – at the end. 
The pattern “caret he” means: we are looking for a match with the word “he”, which is at the very beginning of the string.
The pattern “he dollar” means: we are looking for a match with the word “he”, which is at the very end of the string.
Both anchors together are often used to test whether or not a string fully matches the pattern. For instance, to check if the user input is in the right format.

Note that, by default, anchors only match at the beginning and end of text.
To get matches at the start/end of a line, we must enable multiline mode. To do this, we must add the flag “m”.

Next let's take a look at the word boundary. When the regexp engine comes across \b, it checks that the position in the string is a word boundary.
There are three different positions that qualify as word boundaries:
- At string start, if the first string character is a word character such as digit, letter or underscore
- Between two characters in the string, where one is a word character and the other is not.
- At string end, if the last string character is a word character
So far, nothing supernatural right? Let's go further.
For example, we have a list of similar words: cat, hat, fat, mat etc. And we want to highlight each of them. This is where sets and ranges come in.

Several characters inside square brackets mean to “search for any character among given”.  For instance, c and b in square brackets mean “I’d like to match either c in the first position or  b”. That’s called a set. 
The more characters we put in square brackets, the more matches we get.

Please note that although there are multiple characters in the set, they correspond to exactly one character in the match.

What if we want to get every word except bat and rat? One way to complete this task – is to simply enter all the letters except b and r into square brackets. 
But there is a shorter way with excluding  ranges. They are denoted by a caret character at the start of line inside square brackets  and match any character except the given ones. The caret must immediately follow open square bracket, or else it stands for just itself. Instead of writing down all the characters we want to match, this syntax allows us to write down the ones we don't want to match, and then anything else will be included. Sometimes this way is much easier.
What if we want to find all words that end with AT and start with any letter of the alphabet? We can solve the problem head-on. Just list all letters in square brackets.

We can also cheat and say that we are looking for all characters except 0 (or any other digit or symbol, it doesn’t matter).

But the correct way to solve our problem is to use the character range. For instance, “a” dash “z” is a character in range from “a” to “z”. So we can find all words that start with a letter in the range from “a” to “z”. 
We can easily change the width of our range. For example, we can find all words that start with a letter in the range from “c” to “m”.

We also can add caret and create excluding  range.

Or we can combine two ranges in the same square brackets.

We can create ranges not only for letters, but also for numbers

For example, we want to find any three digit number, we can use this pattern. 

Some ranges are so commonly used that there are special shortcuts. They are called character classes. A character class is a special notation that matches any symbol from a particular set. 
Here is a list of the main character classes. The list is a little longer, you can see the full one on mdn, and we will focus on the main ones.

For the start, let’s explore the “digit” class. It’s written as \d and corresponds to “any single digit”.
If we enter one character, you can see that we have six matches - digits 4, 5, 9, 1, 2, 3. Note that we have the “g” flag here, which means we are looking for all matches, not just the first one.

If we enter two characters, you can see that we have two matches

And if we enter three characters in a row, there will be only one match. Pretty simple, isn’t it?

the next class we will learn is \D (backslash capital letter D). It’s non-digit class, which includes any character except digits, as you can see on the screen.

the next class is \s (backslash s, s is from “space”) .Includes spaces, tabs, newlines and few other rare characters, such as vertical tab and carriage return.

 By analogy with the number class, there is an inverse class \S (backslash capilal s) that includes all characters except space-like.

One of the most commonly used classes is the \w (backslash w, w is from word). It includes either a letter of Latin alphabet or a digit or an underscore. Non-Latin letters (like cyrillic or hindi) do not belong to \w.

And, as you may have guessed, the inverse of this class is (backslash capital w), and it includes all characters except latin letters, numbers and underscores.
The last class we'll look at today is the dot class. It is a special character class that matches “any character except a newline”. 

But if we add special “s” flag, dot will literally mean “any character”, including newline.

Let's play a bit with character classes. For example, we want to find all words that are five letters long. Therefore, we will use five word class characters. As you can see, we got what we wanted, but with side effects. The result is not only five-character words, but any combination of five letters, even from the middle of a word. Let fix this.

We will add two space class characters at the beginning and at the end of the word.
Now we got what we wanted. But let's assume we are interested in combinations of five-letter words with three-digit numbers. 

We'll just add three numeric class characters at the end of the pattern. It is that simple. Cheap and cheerful.

Final expression is long-winded. Imagine if we are looking not for three-digit numbers, but for huge ones. To avoid repeating the same character in a pattern, regular expressions have such powerful tools as quantifiers.

The simplest quantifier is a number in curly braces. A quantifier is appended to a character, or a character class, or a range, or set, etc.,  and specifies how many we need. 
This template is completely identical to the previous one, but much shorter.

In addition to specifying the exact value, we can specify the range in curly braces.
Note that we got matches with all numbers longer than 5 digits and less than 9 digits. If the number is less than the lower limit, it does not appear in the search results, if the number is greater than the upper limit, then it is split into matches, the first of which has the maximum length, and the length of the rest does not exceed the specified range.

If you remove the upper limit, then all numbers from 5 and more will fit the pattern.
There are shorthands for most used quantifiers. One of them is a plus sign. 
This pattern will match any number greater than 1.

The plus quantifier is equivalent to quantifier in curly braces with a lower limit of one and no upper limit.

The next quantifier you should be aware of is the asterisk quantifier. This pattern will match any number greater than 1 or none. Thus, the absence of a number will also be a match.

The asterisk quantifier is equivalent to quantifier in curly braces with a lower limit of zero and no upper limit. Note that even the absence of a symbol is a match (such matches are marked with a vertical pink line).

And the last quantifier we'll talk about is the question mark quantifier. It means “zero or one”.  In other words, it makes the symbol optional.

The question mark quantifier is equivalent to quantifier in curly braces with a lower limit of zero and upper limit of one.

There are also nuances with greedy and lazy quantifiers, but the time limits of the presentation does not allow dwelling on this topic in detail.

The next regex tool we'll look at is called capturing groups. Capturing groups help a lot when using quantifiers. Imagine that we want to find a string of any length, consisting of repeated words. The plus quantifier is great for our task, but there's a problem: it only applies to the last character. So, the pattern “go+” means “g” character, followed by “o” repeated one or more times. Note there are five matches on the screen. But we only need one - the entire first line "gogogo".

To solve this problem, we can enclose the word "go" in parentheses. This is called a capturing group. And now we get the full string "gogogo". 
The capturing groups  enhances another regular expression tool called alternation. Alternation is the term in regular expression that is actually a simple “OR”. In a regular expression it is denoted with a vertical line character.


At first sight, We already saw a similar thing – square brackets. They allow to choose between multiple characters. But there is a difference: Square brackets allow only characters or character classes. Alternation allows any expressions.
For example, here in the first case we choose between two characters: "a" or "e". In the second case, we choose between whole words.

And with capturing groups, we can apply alternation much more flexibly, creating our own improved sets and ranges.

Group capturing is a powerful tool when combined with Javascript methods. But more on that later.



in javascript you can create a regex in two ways: 
using the built-in object (first we pass the string which is the pattern, then we pass the optional flags(флАгс) as the second argument) 
We can also create a regular expression using the slash syntax.
in both cases it is an object of the built-in class RegExp. 



The difference between these two methods is as follows:

1) We cannot insert template string into slashes. Therefore, if we want to dynamically create a regular expression, the option with an built-in object is suitable for us.
2) screening

In javascript, regular expressions are used in the “exec” and “test” methods of the RegExp object, and in the “match”, “replace”, “matchAll”, “replaceAll”, “search”, and “split” methods of the String object. Let's take a quick look at the most popular of them.
The match method returns matches against a regular expression pattern.
here we call the match method on the str string, and pass it a regular expression without flags.
If there’s no “g”  flag, match method returns only the first match in the form of an array, with the full match at index 0 and some additional details in properties: index, source string and groups. Like any array, it also has a length property, which is not shown here. Note that we got a word that starts with a small letter, like in our pattern, not a capital one.

if I add the “i” flag, we get a word that starts with a capital letter, because with “i”  flag the search is case-insensitive, as you remember. Note that although the search result is an array, it contains only one value - the first matching one it encountered in the string, as in the previous slide
if I add the “g”  flag we get three words in the form of array, because with “g” flag the search looks for all matches, without it – only the first match is returned. And as you learned in the previous slide, since we have the “i” flag, our search returns both the capitalized words and the lowercase word.

If I remove the “i” flag, and change the first letter in the search pattern to capital one, we get an array of two elements, since the lowercase word is no longer suitable for us. Note that with the “g” flag, our array does not contain additional properties (like index, input and groups), since the “g”  flag changes the principle of the search - we are looking for an array of words, not just one.

 And finally, if there are no matches, we don’t receive an empty array, but instead receive null.

The method  “replace” replaces match or matches found using regexp in string with replacement, and returns a new string. Note that only the first match in the example was replaced because without the “g” flag, only the first match would be replaced. 

We can use all the same flags that we used with the match method. 
For example, if I change the first letter in the pattern to uppercase, the result of the method execution will be the original string – “ never say never ”. But if I add a “i” flag (which means case-insensitive), the method will replace first match in the string. 

If I add a “g”  flag (which means global), the method will replace both matches in the string.
We can use special character combinations in replacement string to insert fragments of the match. Here is their list:
This inserts the whole match
This inserts a part of the string before the match
This inserts a part of the string after the match
about these symbols we will talk little later
And a double dollar for a dollar insert

Here we are using a special combination "dollar and ampersand" to replace a word “you” with the same word and the addition.
Here we are using a special combination "dollar and backquote" to replace a word “you” with part of the string before the match and the addition.
Here we are using a special combination "dollar and single quote" to replace a word “love” with part of the string after the match and the addition.
The next method we are talking about - is the “test” method. This method looks for at least one match, if found, returns true, otherwise false.
Note that the “test” method is a Regexp object method, not a string method. 
All flags are still relevant here.

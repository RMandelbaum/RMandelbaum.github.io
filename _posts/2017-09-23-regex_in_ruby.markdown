---
layout: post
title:  "Regex in Ruby"
date:   2017-09-23 15:08:44 -0400
---


As I’m working my way through the Sinatra section of the program, I came across a lab where I had to write an application that took in a word, and translated it into, none other than, Pig Latin. Now, this was something I haven’t thought about in a long time. When I was a kid, I barely understood how to speak Pig Latin, so to write the code for it felt like an homage to my past self who wished she could join in on all that secret language fun.  

I needed to code a method that incorporated logic to break down a word and translate it. Now, what ruby method allowed me to target certain data based on patterns? I flipped through my Procedural Ruby section of my notes, and landed on the answer. Regular Expressions, aka Regex. 


**What is Regex in Ruby?**

Regex is used to encode specific patterns for matching, searching, and substitution. 

Let’s say I have a long string and I only want to have the vowels returned to me. My regex would be /[aeiou]/, and I’d pair this regular expression with a ruby method in order to get my desired return value. 

Some common methods that are used with regex:

#scan
```
"hocus pocus".scan(/[aeiou]/)
 => ["o", "u", "o", "u"] 
```

This returns an array of all items in your string that match a given regex. 

#match

```
 "hocus pocus".match(/[aeiou]/)
 => #<MatchData "o"> 
```

This returns the first item in your string that matches a given regex as a Match Data object. 



#grep

```
array = ["hocus pocus", "abacadabra", "pshhh"]
 => ["hocus pocus", "abacadabra", "pshhh"] 
 
array.grep(/[aeiou]/)
 => ["hocus pocus", "abacadabra"] 
```
 
 This returns an array of matching items from an array. 

 

**Regex meets the Piglatinizer**

Thanks to Wikipedia, I learned how Pig Latin works (a mere 10 years late), and wrote out my logic step by step for my Pig Latin method. 

1. Check to see if my word starts with a vowel.
2. If it does, add “way” to the end of the word.
3. If it doesn’t, I need to split the word at the first vowel, and add the beginning consonants to the end of the word, along with “ay”.

Luckily there is a split method that works well with regex. Let’s say my word was “shampoo”, and I wanted to split it into “sh” and “ampoo”. 

```
word = "shampoo"
 => "shampoo" 
word.split(/[aeiou]/)
 => ["sh", "mp"] 
```

But I'd only want the first set of consonants, so I'd add  ".first”  

```
word.split(/[aeiou]/).first 
 => "sh" 
```

 
Pretty awesome. Regex has an extraordinary long list of possible patterns, and [www.Rubular.com](http://) is a great site to easily play around with an expression to see what it can do with your data. 



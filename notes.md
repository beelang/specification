A sample of syntactical delights from my notes on Dragon:

Number
=======
A simple number value:

    2
    # => 2::NUMBER

Text
====
A simple text value:

    "Hello, World!"
    # => "This is text"::TEXT

List
====
A list value, with number values:

    ( 1, 2, 3 )
    # => ( 1, 2, 3 )::LIST

A list value, with text values:

    ( "Hello", "Beautiful", "World" )
    # => ( "Hello", 2, "World )::LIST

Combination of number and text values in a list value:

    ( "Hello", 2, "World" )
    # => ( "Hello", 2, "World )::LIST

Pair
====

A simple pair value, with keys and text & number values:

    ( Name: "Kurtis", Age: 23, Likes: "Pie")
    # => ( Name: "Kurtis", Age: 23, Likes: "Pie")::PAIR

Verbs
=====

A simple verb that takes two number values:

    add:( 2, 2 )
    # => 4::NUMBER

Chaining verbs, to turn one value into another type of value:

    add:( 2, 2).as_text
    # => "4"::TEXT

Chaining verbs, with an error:

    add:( 2, 2.as_text )
    # => Incorrect Type Error (line 1): for verb `add`:
    #      value: 2
    #      value: "2"
    #      error_message: "value #2 type wasn't a NUMBER"

Words
=====

Defining a simple word, with a text value:

    Name: "Kurtis Rainbolt-Greene"
    # => Name:TEXT

Defining a simple word with a number value:

    Age: 23
    # => Age::NUMBER

And now a list value:

    Likes: ("Magic: The gathering", "Ruby", "Writing")
    # => Likes::LIST

Using verbs on words:

    Name.reverse
    # => "eneerG-tlobniaR sitruK"::TEXT
    Name
    # => "Kurtis Rainbolt-Greene"::TEXT

Bang Verbs change the Word's value:

    Age.up!
    # => 24::NUMBER
    Age
    # => 24::NUMBER

Here's a word, with a verb, and an argument:

    Likes.sort_by:("length", "ascending")
    # => ("Ruby", "Writing", "Magic: The gathering")::LIST

You can, of course, reference pairs with words:

    Person1: (
               Name:  "Kurtis Rainbolt-Greene",
               Age:   23,
               Likes: ("Magic: The gathering","Ruby","Writing")
             )
    # => Person1::PAIR

And then extract values by providing the keys of the pair:

    Person1:Name
    # => "Kurtis Rainbolt-Greene"::TEXT

And then chain verbs off that returned value!

    Person1.Name.reverse
    # => "eneerG-tlobniaR sitruK"::TEXT


number:
  1
  -1
  1.0
  1.5e10
  400_000.40
string:
  "Hello, world!"
list:
  ( 1, 2, 3, 4, 5 )
  ( "Hello!", "World!", "I", "Am", "Bob!" )
  ( "And", "A", 1, "Three", 3, "Four!" )
table:
  ( key: "value", key2: "value2" )
  ( name: "Kurtis", age: 23, job: "Unemployed", friends: ("John", "Wiliam", "Kitty" ) )
  ( ( name: "Jackie Chan", age: 42, job: "Martial Artist" ), ( name: "Michael Jackson", age: 400_000, job: "Dancer" ) )
work:
  [ a b + ]
  [ "String" capitalize ]
comment:
  # This is a comment.
definfing words:
  word_name: 4
  my_rent: 400.00
  name: "Kurtis Rainbolt-Greene"
defining verbs: |
  verb_name: ( list, of, arguments ) => #logic here#
  add: ( a, b ) => a + b
  |
    add: ( a, b ) do
      a + b
    end
types:
  Number       # Standard integer class
  String       # Standard string class, no '' strings though. Always interpolated.
  List         # A list of things.
  Table        # A list of things with keys.
  Array        # An immutable list of things, a list with {} instead of ()
  Hash         # Same as Array, but with keys.
  Word         # A function.
  Work         # Code.
  Type         # Regular old class class.
example 1: |
  talk: ( name ) => "Hello, " + name
  talk "Kurtis" # Result: "Hello, Kurtis"
example 2: |
  first_name: "Kurtis"
  last_name: "Rainbolt-Greene"
  first_name + uppercase last_name
  # Result: "Kurtis RAINBOLT-GREENE"

2                                                  # => 2::NUMBER

"Hello, World!"                                    # => "This is text"::TEXT

( 1, 2, 3 )                                        # => ( 1, 2, 3 )::LIST

( "Hello", 2, "World" )                            # => ( "Hello", 2, "World )::LIST

( Name: "Kurtis", Age: "23", Likes: "Pie")         # => ( Name: "Kurtis", Age: "23", Likes: "Pie")::PAIR

2 + 2                                              # => 4::NUMBER
add:( 2, 2 )                                       # => 4::NUMBER

|2 + 2|.as_text                                    # => "4"::TEXT
add:( 2, 2).as_text                                # => "4"::TEXT

|    2  +  2    | . as_text                        # => "4"::TEXT

2 + 2.as_text                                      # => Incorrect Type Error (line 1): for verb `+`:
                                                   #      word: 2
                                                   #      word: "2"
                                                   #      error_message: "second word type wasn't a NUMBER"
add:( 2, 2.as_text )                               # => Incorrect Type Error (line 1): for verb `add`:
                                                   #      word: 2
                                                   #      word: "2"
                                                   #      error_message: "word #2 type wasn't a NUMBER"

Name: "Kurtis Rainbolt-Greene"                     # => Name:TEXT
Age: 23                                            # => Age::NUMBER
Likes: ("Magic: The gathering", "Ruby", "Writing") # => Likes::LIST

Name.reverse                                       # => "eneerG-tlobniaR sitruK"::TEXT
Age.up                                             # => 24::NUMBER
Likes.sort_by:"length"                             # => (Ruby", "Writing", "Magic: The gathering")::LIST

Person1: (
           Name:  "Kurtis Rainbolt-Greene"
           Age:   23
           Likes: ("Magic: The gathering","Ruby","Writing")
         )                                         # => Person1::PAIR

Person1:Name                                       # => "Kurtis Rainbolt-Greene"::TEXT
Person1:Name.reverse                               # => "eneerG-tlobniaR sitruK"::TEXT

# To pull in external libraries simply add the library names to the `Library` word.
# The `Libraries` word is a list of strings, which are the names of different libraries.
# Normally the `Libraries` word only has the 5 core libraries.
# The `add` verb is just an alias for `append`.

Libraries.add:"rss-reader"
Libraries.add:("http-parser", "uri-extras")

detailed_display:Libraries       # => ("red-dragon", "green-dragon", "blue-dragon", "white-dragon", "black-dragon", "rss-reader", "http-parser", "uri-extras")

Feed: RSS.create("http://news.google.com/rss".encode_to_uri)

if: |Feed.is_rss? & Feed.is_alive?| > Articles: Feed.pull.parse_xml  # Not so sure about the >

display: Articles.first:Title        # => "President Obama announces Anti-Tea Party Machine gun turrets..."

Articles.each: Article >             # Ugh, should I go with white-space sensitive "action" blocks?
  display: Article:Title.as_text

.... more later.

Red Dragon: The Syntax & Use Of
-------------------------------

As you may have heard Red Dragon is a simple procedural imperative DSL programming language. What does that mean? It means that RD is particularly good at being a learning language. It can, with practice, do some pretty smart things but prides itself on being easy to learn.


Basic Values: Numbers & Text
============================

Red Dragon has two basic values:

**Numbers** which are integers, and pretty self explanatory.

### Example 1:
    1
### Example 2:
    -1
### Example 3:
    2.0
### Example 4:
    3.5e+42

And **Text**, which are even simpler, as they're just your basic string.

    Example 1: "Hello, World!"
    Example 2: "Count down, 3, 2, 1!"

These types of values are used in every day life and will make absolute sense to most students, as they've been crammed with this sort of stuff for years.

Your student will likely understand exactly what these are, and understanding gives a foothold for future context.


Grouped Values: Lists & Pairs
=============================
The second two types of values are a little more complex, yet still presented in an easily digested manner:

**Lists** are groups of values like Numbers, Texts, and even other Lists, plus more. List values can be referenced by an index, a Number.

    Example 1: ( 1, 42, 23, 11, 200000 )
    Example 2: ( "High", "Five", "Jesus!" )
    Example 3: ( 1, 2.0, -3, 4e+50, "word", "heaven", "demigod" )

**Pairs** are like Lists in a lot of ways, except each item consists of a key/value pairing. Instead of referencing the value by an index number, you gather it through the key. Both Pairs and Lists use the same syntax, so the student has an easier time understanding the context.

    Example 1: ( rent: 400.00, utilities: 75.00, food: 35.00 )
    Example 1:
        (
            name: "Kurtis Rainbolt-Greene",
            age: 42,
            likes: ( "Pizza", "Hacking", "Women" )
        )

By now you've probably noticed how each new value type, from Number to Pair, we've stacked on. You're using Numbers and Texts in Lists, and all three in Tables. Students catch onto this, and they tend to learn faster.

By keeping the syntax similar it's easy to remember how it's used, which is probably the biggest hurdle for learning developers.

Basic assignments: Words & Verbs
================================

Ok, so now that we've gone over all the important value types I think it's time to get to logic. First up to bat is a Word.

Words are your every day variables from other languages. Words are immutable, because in real communication once you define something it's generally a bad idea to change the assignment mid-conversation. This connection is something the student should be made aware of: Words are like language words. You define them, and then use them later on as a way of shortcutting to a meaning.

    Example 1:
        my_name: "Kurtis Rainbolt-Greene"
    Example 2:
        my_age: 42
    Example 3:
        groceries: ( "Pizza", "Hamburgers", "Green things" )
    Example 4:
        profile: ( name: "Jack", age: 32, likes: ( "Oceans" ) )

Words get defined and then can be used later. The student will probably best understand this as "Saving". An observant reader will notice how Words look strangely similar to the keys in Pairs. That's correct! Pairs are lists with items that are just variable assignments. Neat, huh?

In fact, lets see it in use:

    my_name: "Kurtis Rainbolt-Greene"
    my_age: 23
    my_likes: ( "Pizza", "Hacking", "Women" )

    profile: ( name: my_name, age: my_age, likes: my_likes )

**Verbs** however, are a bit more complex (as usual). Verbs, as I've explained to my students are things you *do* to values. Verbs are your standard Function, Method, or Operation in other languages. Verbs take Nouns, commonly called Arguments.

    Example 1:
        add: ( a, b ) => a + b

    Example 2:
        remove_tld: ( url ) do
           new_url: remove url, ( ".com", ".net", ".org" )
           print new_url
        end

Alright, so now you've seen two types of verbs. Short and long. Each has it's own uses. Notice how we continue to use syntax from previous things. Nouns are inside of a List. You have a list of Arguments being used inside the Verb. Some new things, however, are the Means (=>) and Do/End blocks.


Boolean: True & False
=====================


Thing vs World
--------------

There are two important objects that exist in Dragon for all runtimes.
The first is `Thing` which is the basic object.
All objects initially have the behavior of `Thing`.
The other object is `World`, which is the default context of the first line of any code.
wq

-> vs =>
--------

In Dragon there are 2 types of anonymous function symbols.
They do roughly the same thing with one exception.

Consider the following code:

    open("README.mdown") ->
      mode("write")
      write("Hello, World")

As you know the above context becomes the object returned by `open()`.
It is lexically equivelent to writing `self mode(...)` and `self write(...)`.
You can always access the bindings of the open call scope by using doing it like this:


    name: "Kurtis"
    open("README.mdown") ->
      mode("write")
      write("Hello, World")
      write(_context name)

In that example `self _context()` returns the `self` that `open()` is being called on.
That object has the assignment `name` binded to it.
This is very clunky, however and so we've provided you the context arrow!
Here's an example of using it correctly:

    name: "Kurtis"
    open("README.mdown") =>
      mode("write")
      write("Hello, World")
      write(name)

Now `self` recieves the assignments of the context that `open()` was called on.
This can be slightly dangerous as in the below example:

  Profile: Object clone ->
    first_name: function(name split)


  first_name: "John"
  Profile new =>
    name: "Jane Public"
    first_name

What does the last line return?
Does it return the output of the function above?
Does it return the assignment?
With a simple `->` this would be an answer as the assignment would be out of context.
With the fat arrow the result would be `"John"`.
While the function `first_name()` was defined for Profile the fat arrow brings in the bindings into the `new` Profile object.
It then overwrites the function with the text value.

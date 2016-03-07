# Ruby Enumerables

[![Build Status](https://travis-ci.org/ga-wdi-lessons/ruby-enumerables.svg?branch=master)](https://travis-ci.org/ga-wdi-lessons/ruby-enumerables)

## Learning Objectives

- Review Ruby arrays and hashes
- Use Ruby loops to iterate over code blocks.
- Define what a Ruby enumerable method is.
- Use enumerables to traverse, sort and modify collections.
- Identify useful Ruby enumerables, including `.each`, `.map` and `.select`.

## Framing (10 / 10)

Today we will be going over enumerables in Ruby, one of the most powerful modules that comes included in the language out of the box.

We will get into how to use enumerables later on this lesson, but first just know that enumerables essentially are a more readable, expressive way to work with collections of data in Ruby.

Whenever we talk about data in Ruby, its important to review how Ruby handles groups of data.

## Review: Ruby Collections

**Q**: What are the different types of collections in Ruby?

### [Arrays](http://ruby-doc.org/core-2.3.0/Array.html)

```rb
fruits = ["apple", "banana", "cherry"]

fruits.length # 3
fruits.push("date")
fruits.length # 4

fruits[0] # apple
fruits[3] # date

fruits[3] = "mango"
fruits[3] # mango

fruits.join(" ") # "apple banana cherry mango"
fruits.join(", ") # "apple, banana, cherry, mango"
fruits.join(" and ") # "apple and banana and cherry and mango "
```

**Q**: What's another "rubyist" way to add items to an array?
---
> A: using `<<`, or the shovel operator: e.g. `fruits << "peach"`

### [Hashes](http://ruby-doc.org/core-2.3.0/Hash.html)

Hashes are like Javascript Object Literals, but they are a bit more limited:

```ruby
instructor = {
  name: "Bob",
  age: 30,
  favorite_foods: ["Tater Tots", "Cheese Steaks", "Kale Salad"]
}

# Access values from a hash
instructor[:name] # "Bob"
instructor[:age]  # 30
instructor[:favorite_foods] # ["Tater Tots", "Cheese Steaks", "Kale Salad"]

# Set values to an existing key
instructor[:name] = "Robert"
instructor[:name] # "Robert"

# Add new key-value pairs
instructor[:favorite_color] = "red"
instructor[:favorite_color] # "red"
```

#### Quick Quiz

-  What's another "rubyist" way to add items to an array?
-  What is one main difference between Ruby's `hashes` and Javascript's `object literals`?
-  What are some useful methods we can call on collections?
-  Where would I go look if I wanted to find more methods?

## Loops (20 / 30)

Another similarity Ruby shares with Javascript is base support for various types of loops.

### Review JS Loops

**Q**: What loops did we use in Javascript?
---
> A: `while`, `do-while`, `for`, `for-in`, `forEach`

Let's start by reviewing JS `for` loops.

Say we had our `fruits` example from earlier and we wanted to print each individual fruit in the console

```js
var fruits = ["apple", "banana", "cherry"];
for (var i = 0; i < fruits.length; i++) {
  console.log(fruits[i]);
}
```

### Looping with Ruby

The closest equivalent to Javascript's `for` loop is Ruby's `for-in` loop

```rb
fruits = ["apple", "banana", "cherry"]
for fruit in fruits do
  puts fruit
end
```

Ruby also has a plethora of other types of loops including:

* `loop`
  * loop runs uninterrupted until stopped
* `while`
  * runs the loop while the condition is true
* `until`
  * runs the loop while the condition is false
* `.times` (called on a number)
  * runs the loop a specific of times

> [Further Reading on Ruby loops](http://www.tutorialspoint.com/ruby/ruby_loops.htm)

### `break`

`break` lets us end -- or "break" out of -- a loop.

**Q**: What numbers do you expect to see printed to the console when we run this loop?
---

```ruby
10.times do |i|
  if i == 5
    break
  end
  puts i
end
```

### `next`

`next` lets us skip to the next iteration of a loop.

**Q**: What numbers do you expect to see to see printed to the console when we run this loop?
---

```ruby
10.times do |i|
  if i == 5
    next
  end
  puts i
end
```

## Exercise: Club Code (20 / 50)

As the new manager of GA's Club Code, you been tasked with creating an automated bouncing system.

The club's rules state:
- Only people 18 and over are allowed in the door
- No more than 8 people should be inside the club at any time

Given a line of people:
```ruby
people = [
  { name: "Jack", age: 16 },
  { name: "Sam", age: 21 },
  { name: "Jill", age: 23 },
  { name: "Paul", age: 20 },
  { name: "Mike", age: 16 },
  { name: "Stan", age: 70 },
  { name: "Chris", age: 17 },
  { name: "Julie", age: 45 },
  { name: "Suzy", age: 65 },
  { name: "Eli", age: 28 },
  { name: "Katie", age: 50 },
  { name: "Ben", age: 33 }
]
```
and using what you know about loops and collections in Ruby, write a program that:
- Creates a new array of people inside the club
- Allows the appropriate people into the club
- Stops once 8 people have been admitted

**Hints:**
- How could you use `next` and/or `break` to alter the behavior of a loop?

**Bonus**
- Determine whether or not a person is to be served
  - Anyone over 18, but under 21 can come in, but they are not to be served adult beverages
  - Create a new key-value pair for each `person` with `served` as a `boolean`

**Double Bonus**
- Write a function that takes 3 arguments: a list of people, an age limit, and capacity limit.
- It should return a hash that looks like this:
  ```ruby
  {
    accepted:
      [ {name: "Jack", age: 22},  {name: "Jill", age: 31}, ...],
    rejected:
      [ {name: "Billy", age: 18},  {name: "Nancy", age: 31}, ...]
  }
  ```

[A Solution](https://gist.github.com/nolds9/9f62c6f10740de8a9b8e)

## Break (10 / 60)

## Enumerables

### What Are Enumerables? (5 / 65)

The Enumerable module provides a set of methods to traverse, search, sort and manipulate collections.

So how are enumerables different than loops you might ask? In general, loops just execute a certain block of code for a given amount of time, while enumerables are used in relation to data collections to more easily control and transform values in data sets.

Since we already have a base understanding of loops and arrays and hashes, there's nothing new conceptually here. But you'll learn to do more with prettier, fewer lines of code.
- [Documentation](http://ruby-doc.org/core-2.2.3/Enumerable.html)

### Useful Enumerables

#### Each (20 / 85)

The king (or queen) of enumerables, and the one you will most likely be using the most.
- Iterates through and performs an action(s) on a collection.
- **Note**: Does not permanently modify the collection.

If we were to emulate `.each` using plain ol' Ruby, it would look something like this...

```ruby
# A loop that prints out the doubled value of each item in an array
numbers = [ 1, 2, 3, 4, 5 ]
i = 0

while(i <= numbers.length) do
  puts numbers[i] * 2
  i = i + 1
end
```

But using `.each` looks like this, with the code block format...

```ruby
numbers = [ 1, 2, 3, 4, 5 ]
numbers.each do |number|
  puts number * 2
end

# Alternate syntax
numbers = [ 1, 2, 3, 4, 5 ]
numbers.each { |number| puts number * 2 }
```

**Visualize:** EACH: using this [code visualizer](http://pythontutor.com/ruby.html#mode=edit) let's look at how `each` operates under the hood

> The `each` method yields a reference to **each element** in the collection, rather than a reference to the element's numerical index in the array.

##### Code Block Format

**WHITEBOARD:** You'll notice we wrote out the `.each` example in two ways: multi-line and single-line.

Multi-line
- `.each` - method name
- `do` - keyword that begins block of code
- `|number|` - iteration variable; represents an individual value in the array
  - Common syntax is to name the variable the singular version of the collection. In this case, use `number` for `numbers`.
  - Some enumerables may have more than one of these.
- `end` - closes code block

Single-line
- `.each` - method name
- { } - replaces `do` and `end`; contains the iteration variable and code block
- `|number|` - iteration variable

### Exercise: Practice Each (10 / 95)

Use `each` to do the following...  

- Say hello to everybody in the below array of names (sample output: `Hello Donald!`).

  ```ruby
  names = [ "Donald", "Daisy", "Huey", "Duey", "Luey" ]
  ```

- Print out the squared values of every number in this numbers array.

  ```ruby
  numbers = [ 1, 3, 9, 11, 100 ]
  ```

- Print out the Celsius values for an array containing Fahrenheit values.

  ```ruby
  fahrenheit_temps = [ -128.6, 0, 32, 140, 212 ]
  ```

- Insert all the values in the `artists` array into the `ninja_turtles` array.

  ```ruby
  artists = [ "Leonardo", "Donatello", "Raphael", "Michelangelo" ]
  ninja_turtles = []
  ```

- **Bonus:** Print out every possible combination of the below ice cream flavors and toppings.

  ```ruby
  flavors = [ "vanilla", "chocolate", "strawberry", "butter pecan", "cookies and cream", "rainbow" ]
  toppings = [ "gummi bears", "hot fudge", "butterscotch", "rainbow sprinkles", "chocolate sprinkles" ]
  ```

Let's get a quick **Fist-of-Five** on how we feel about `each` and enumerables so far?
- There are many enumerable methods.  All of them look and feel similar to `each`.

#### Map (10 / 105)

Map is similar to `each`.  It iterates through each element in the collection,  but `map` generates a **new collection** with values based on the code block. Say we want to double our `numbers` array and store it in a new array...

```ruby
numbers = [ 1, 2, 3, 4, 5 ]
doubles = numbers.map do |number|
  number * 2
end
doubles
# => [ 2, 4, 6, 8, 10 ]

# Alternate syntax
numbers = [ 1, 2, 3, 4, 5 ]
doubles = numbers.map { |number| number * 2 }
doubles
```

**NOTE:** We did not have to type out any variable assignment in the code block!

**VISUALIZE:** MAP: using this [code visualizer](http://pythontutor.com/ruby.html#mode=edit) let's look at how `map` operates under the hood

### Exercise: Practice Map (5 / 120)

Use `map` to do the following...  

1. Create an array that appends "Duck" to everybody in this array of first names

  ```ruby
  first_names = [ "Donald", "Daisy", "Daffy" ]

  #=> ["Donald Duck", "Daisy Duck"]
  ```

2. Create an array containing the squared values of every number in this array.

  ```ruby
  numbers = [ 1, 3, 9, 11, 100 ]

  # => [1, 9, 81, 121, 10000]
  ```

3. Create an array with the Celsius values for these Fahrenheit values.

  ```ruby
  fahrenheit_temps = [ -128.6, 0, 32, 140, 212 ]

  #=> [-89.2, -17.8, 0, 60, 100]
  ```

## Break (10 / 130)

## Group Exercise: Documentation Dive (20 / 150)

Instructions: Each group will spend **10 minutes** using Ruby documentation to look up an assigned enumerable. Prepare your own definition of what it does and whiteboard an example.
- You can test your example in IRB/Pry.
- [Documentation](http://ruby-doc.org/core-2.2.3/Enumerable.html)

Groups
- **Group 1:** Each With Index
- **Group 2:** Reject
- **Group 3:** Find
- **Group 4:** Select
- **Group 5:** Sort By
- **Group 6:** Inject/Reduce

**Bonus:** If you find yourself with extra time, you can:
- Pick out another enumerable that wasn't assigned to a group.
- ...and/or think of another example for your assigned enumerable.

## Homework: High Card

Combine your knowledge of Ruby basics and enumerables to make our old nemesis a piece of cake...

[High Card](https://github.com/ga-wdi-exercises/high_card)

## Sample quiz questions

1. What is the difference between `loops` and `enumerables` in Ruby?
1. What are some examples of loops in Ruby that are not in JS?
2. Differentiate between Ruby's `each` and `map` methods
3. What is an `iteration` variable?
4. List 5 useful Ruby enumerable methods

## Resources

- [Intro to Ruby Enumerables](http://jamesgolick.com/2008/1/5/an-introduction-to-ruby-s-enumerable-module.html)
- [Ruby Monk on Enumerables](https://rubymonk.com/learning/books/4-ruby-primer-ascent/chapters/44-collections/lessons/96-enumerators-and-enumerables)
- [Ruby Explained: Awesome Enumerables](http://www.eriktrautman.com/posts/ruby-explained-map-select-and-other-enumerable-methods)
- [Ruby Magic](http://ruby.bastardsbook.com/chapters/enumerables/)

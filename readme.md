# Ruby Enumerables

<!-- [![Build Status](https://travis-ci.org/ga-wdi-lessons/ruby-enumerables.svg?branch=master)](https://travis-ci.org/ga-wdi-lessons/ruby-enumerables) -->

## Learning Objectives

- Review Ruby arrays and hashes
- Use Ruby loops to iterate over code blocks.
- Define what a Ruby enumerable method is.
- Use enumerables to traverse, sort and modify collections.
- Identify useful Ruby enumerables, including `.each`, `.map` and `.select`.

## Framing (10 / 10)

One of the most common things we do as developers is to iterate through data structures.

Whenever we talk about data in Ruby, its important to review how Ruby handles groups of data.

We learned how to loop through data in Javascript. Now we're going to learn how to do them in Ruby. We'll start with the basics, but then...

We will be going over enumerables in Ruby, one of the most powerful modules that comes included in the language out-of-the-box.

## Review: Ruby Collections

<details>
<summary>What are the different types of collections in Ruby?</summary>
Arrays `[]` and hashes `{}`
</details>

### [Arrays](http://ruby-doc.org/core-2.3.0/Array.html)

Consider:

```rb
users = ["Alice", "Bob", "Carol"]
```

#### What do each of the following do?

- `users.length`
- `users.push("David")`
- `users[0]`
- `users[2]`
- `users.join(" ")`
- `users.join(", ")`
- `users.join(" and ")`

<details>
<summary>What are the two ways of adding items to the end of an array of unknown length in Ruby?</summary>
`.push` and `<<`
</details>

<!-- Specifying "unknown length" because users[n] should not be one of the methods. -->

### [Hashes](http://ruby-doc.org/core-2.3.0/Hash.html)

Hashes are like Javascript Object Literals, but with a somewhat different syntax.

Consider:

```ruby
user = {
  name: "Alice",
  age: 30,
  skills: ["development", "public speaking", "physics"]
}
```

#### What do each of the following do?

- `user[:name]`
- `user[:age]`
- `user[:name] = "Bob"`
- `user[:zip] = 55408`
- `user[:skills].last`
- `user[:skills] << "design"`

#### Quick Quiz

-  What's another "rubyist" way to add items to an array?
-  What is one main difference between Ruby's `hashes` and Javascript's `object literals`?
-  What are some useful methods we can call on collections?
-  Where would I go look if I wanted to find more methods?

## Loops (20 / 30)

Another similarity Ruby shares with Javascript is base support for various types of loops.

### Review JS Loops

<details>
<summary>What loops did we use in Javascript?</summary>
`while`, `do...while`, `for`, `for...in`, `.forEach`
</details>

### Looping with Ruby

The closest equivalent to Javascript's `for` loop is Ruby's `for...in` loop

```rb
users = ["Alice", "Bob", "Carol"]
for user in users do
  puts user
end
```

<details>
<summary>What happens if you change it to `for person in users do`? What other change will you need to make?</summary>
`puts person` instead of `puts user`
</details>

#### *In English*, describe the differences between `while`, `until`, `loop`, and `.times`.

All the snippets below have the exact same result:

```
Alice
Bob
Carol
```

If you would like to test them out, you might try this:

1. Create a new file in your "in-class" directory called `loops.rb`
- Copy and paste **one** of the snippets into the file
- Run the file with `$ ruby loops.rb`
- Observe the result
- Delete the contents of the file
- Replace the contents with the next snippet
- Repeat

#### while

```rb
users = ["Alice", "Bob", "Carol"]
index = 0
while index < users.length
  puts users[index]
  index += 1
end
```

#### until

```rb
users = ["Alice", "Bob", "Carol"]
index = 0
until index == users.length
  puts users[index]
  index += 1
end
```

#### loop

```rb
users = ["Alice", "Bob", "Carol"]
index = 0
loop do
  puts users[index]
  index += 1
  break if index == users.length
end
```

#### .times

```rb
users = ["Alice", "Bob", "Carol"]
users.length.times do |index|
  puts users[index]  
end
```

<details>
<summary>If we change `puts users[index]` to `puts index`, what will the result be?</summary>
`1 2 3`
</details>

<details>
<summary>What is the purpose of `break`? What loops can you use it inside?</summary>
`break` halts the current iteration of the loop. It can be used with any loop.
</details>

#### next

Try this code:

```rb
10.times do |i|
  if i % 2 == 0
    next
  end
  puts i
end
```

<details>
<summary>What is `next`, and how is it different from `break`?</summary>
`next` tells the computer to skip the rest of the code inside the loop for this iteration, and go to the next iteration of the loop. `break` stops the loop iterating altogether.
</details>

> [Further Reading on Ruby loops](http://www.tutorialspoint.com/ruby/ruby_loops.htm)

## Exercise: [Club Ruby](https://github.com/ga-wdi-exercises/club_ruby) (20 / 50)

## Break (10 / 60)

## Enumerables

### What Are Enumerables? (5 / 65)

Loops execute a certain block of code a certain number of times.

**Enumerables** are loops *used specifically to do something to or with each item in an collection.*

Enumerables are great at traversing, searching, filtering, and modifying collections of data in Ruby.

Ruby enumerables are **very** similar to higher order functions in Javascript, with a slightly different syntax.

Enumerables **DRY** up your code considerably. Consider:

#### `while` is a loop

```rb
users = ["Alice", "Bob", "Carol"]
index = 0
while index < users.length
  puts users[index]
  index += 1
end
```

#### `each` is an enumerable

```rb
users = ["Alice", "Bob", "Carol"]
users.each do |user|
  puts user
end
```

- [Documentation](http://ruby-doc.org/core-2.2.3/Enumerable.html)

### Syntax

Try running these two code snippets:

> This one is copied from above

```rb
users = ["Alice", "Bob", "Carol"]
users.each do |user|
  puts user
end
```

```rb
users = ["Alice", "Bob", "Carol"]
users.each{|user| puts user}
```

<details>
<summary>What is the difference in the result of these two snippets?</summary>
There's no difference: they're two ways of writing the exact same thing.
</details>

<details>
<summary>What happens if you change `users.each do |user|` to `users.each do |person|`? What else needs to change?</summary>
`puts user` needs to become `puts person`.
</details>

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
Hint: Use nested enumerables or check out [product](http://apidock.com/ruby/Array/product)

### Map (10 / 105)

#### Explore 1

Run these two snippets separately:

```rb
cart = ["shoes", "watch", "computer"]
uppercase = cart.each{|product| product.upcase }
puts uppercase.join(", ")
```

```rb
cart = ["shoes", "watch", "computer"]
uppercase = cart.map{|product| product.upcase }
puts uppercase.join(", ")
```

<details>
<summary>How would you explain the difference in the result?</summary>
`.each` returns the original array on which it was performed. `.map` returns a new array with the changes in the block applied to each element.
</details>

#### Explore 2

Consider:

```ruby
cart = ["shoes", "watch", "computer"]
uppercase = []
cart.each{|product| uppercase.push(product.upcase) }
puts uppercase.join(", ")
```

```rb
cart = ["shoes", "watch", "computer"]
uppercase = cart.map{|product| product.upcase }
puts uppercase.join(", ")
```

<details>
<summary>What is the difference in the result of these two snippets?</summary>
Nothing: they have the same result. They are two ways of doing the same thing.
</details>

#### Explore 3: Bang

Consider:

```rb
cart = ["shoes", "watch", "computer"]
uppercase = cart.map{|product| product.upcase }
puts cart
puts uppercase
```

Below is the same snippet, but with `.map!` instead of `.map`.

<details>
<summary>What does `!` often indicate in Ruby?</summary>
That this method is "dangerous", usually because it will modify the object upon which it was called.
</details>

```rb
cart = ["shoes", "watch", "computer"]
uppercase = cart.map!{|product| product.upcase }
puts cart
puts uppercase
```

<details>
<summary>What's the difference between `.map` and `.map!`?</summary>
`.map` leaves the original array alone, whereas `.map!` changes it.
</details>

### Exercise: Practice Map (5 / 120)

Use `map` to do the following...  

1. Create an array that appends "Duck" to everybody in this array of first names

  ```ruby
  first_names = [ "Donald", "Daisy", "Daffy" ]

  #=> ["Donald Duck", "Daisy Duck", "Daffy Duck"]
  ```

2. Create an array containing the squared values of every number in this array.

  ```ruby
  numbers = [ 1, 3, 9, 11, 100 ]

  # => [1, 9, 81, 121, 10000]
  ```

3. Create an array with the Celsius values for these Fahrenheit values. Hint: C = (F &minus; 32) &times; (5 &divide; 9)

  ```ruby
  fahrenheit_temps = [ -128.6, 0, 32, 140, 212 ]

  #=> [-89.2, -17.8, 0, 60, 100]
  ```

## Break (10 / 130)

## Group Exercise: Documentation Dive (20 / 150)

Instructions: Each group will spend **10 minutes** using Ruby documentation to look up an assigned enumerable. Prepare the following for your demo:

- Your own definition of what it does
- An example
- At a high level, try to find/think of a use case of this enumerable in the wild. It doesn't have to be the actual code, just conceptually similar.

The enumerables are:

- **[Each With Index](http://ruby-doc.org/core-2.4.0/Enumerable.html#method-i-each_with_index)**
- **[Reject](http://ruby-doc.org/core-2.4.0/Enumerable.html#method-i-reject)**
- **[Find](http://ruby-doc.org/core-2.4.0/Enumerable.html#method-i-find)**
- **[Select](http://ruby-doc.org/core-2.4.0/Enumerable.html#method-i-select)**
- **[Sort By](http://ruby-doc.org/core-2.4.0/Enumerable.html#method-i-sort_by)**
- **[Inject/Reduce](http://ruby-doc.org/core-2.4.0/Enumerable.html#method-i-inject)**

**Bonus:** If you find yourself with extra time, please:

- Pick out another enumerable that wasn't assigned to a group.
- ...and/or think of another example for your assigned enumerable.


## Homework: High Card

Combine your knowledge of Ruby basics and enumerables to make a simple card game. 

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
- [Ruby Loops and Iterators](https://launchschool.com/books/ruby/read/loops_iterators)

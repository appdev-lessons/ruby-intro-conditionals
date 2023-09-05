# If statements

Now that we can get input from our users, we can start to make our programs smart, by behaving differently based on different conditions.

To add conditions based on user input, we need to add a new grammar to our toolbox: the `if`/`end` **keywords**. Here's how it looks:

```ruby
lucky_number = rand(100)

pp "Your lucky number is " + lucky_number.to_s + "."

if lucky_number.odd?
  pp "The number is odd."
end
```
{: .repl #lucky_number title="Lucky number conditional" points="1"}

Try running this program a few times and see how it behaves. These expressions, which _conditonally_ run some code based on the truth or falseness of some condition, are known as **conditionals** or **if statements**.

## The basic anatomy of if statements

The anatomy of an `if` statement is:

```ruby
if condition
  # code that runs if the condition is true
end
```

 1. First comes the `if` keyword.
 1. After the `if`, on the same line, comes any Ruby expression, which is evaluated until only one piece of data is left.
 1. If that final return value of `condition` is "truthy", then the code on the lines between the `if` and `end` keywords is executed.
 1. If the final return value of `condition` is "falsy", then the code on the lines between the `if` and `end` keywords is ignored.
 1. Either way, the program picks up execution on the next line after the `end` keyword and continues on.

### Don't forget the end 

Every `if` requires a matching `end`, and forgetting it is a _very_ common mistake.

My advice: type the `end` _immediately_ after typing the `if` so that you don't forget it; _then_ worry about typing the condition, and the code that comes on the lines between the `if` and the `end`.

(While you're at it, indent the code on the lines between by two spaces, or by pressing <kbd>Tab</kbd> so that it is visually clear what's inside the `if` statement.)

Write a program in the graded code block below that checks if the sample from the array is even, and prints:

"The number X is even!" 

if the condition is met. 

Please note that the test for this graded code block has to deal with randomness of the sample, so if you think your code is working, but the test isn't passing, **try to run the test again.**

```ruby
the_array = [12, 23, 42, 73, 6]
the_sample = the_array.sample
# write your program here
```
{: .repl #is_even title="Is it even?" readonly_lines="[1,2]"}

```ruby
describe "Is it even?" do
  it "should print 'The number 10 is even!' given the input 10" do
    path = "/tmp/code.rb"

    # specify a player move
    file = File.read(path)
    new_content = file.split("\n")
    new_content = new_content.map { |line| line == 'the_sample = the_array.sample' ? 'the_sample = 10' : line }.join("\n")
    File.open(path, 'w') { |line| line.puts new_content }

    File.foreach(path) do |line|
      if line.match(/^p.*"The number 10 is even!"/)
        expect(line).to_not match(/The number 10 is even!/),
          "Expected graded code block to NOT print the String literal 'The number 10 is even!', but did."
      end
    end

    expect { require_relative(path) }.to output(/The number 10 is even!/).to_stdout
  end
end
```
{: .repl-test #is_even_test_1 for="is_even" title="Is it even? should print 'The number 10 is even!' given the input 10" points="1"}

## Multibranch if statements

We can also have **multibranch** `if` statements, where we specify fallback conditions to check and code to execute if the first condition is falsy:

```ruby
the_temp = rand(100)

pp the_temp

if the_temp > 75
  pp "It's going to be a great day today"
else
  pp "Don't leave home today"
end
```
{: .repl #multibranch_1 title="Multibranch with else" points="1"}

Or you can have multiple conditions that get checked, one after the other:

```ruby
the_temp = rand(100)

pp the_temp

if the_temp > 75
  pp "It's going to be a great day today"
elsif the_temp > 32
  pp "It'll be an okay day today"
else
  pp "Don't leave home today"
end
```
{: .repl #multibranch_2 title="Multibranch with elsif and else" points="1"}

 - Note that there is **no space** in the `elsif` keyword, and that there is **no `e` in the middle** of the `elsif` keyword. (In other languages, this construct is `elseif`, `else if`, etc; but in Ruby it's just `elsif`.)
 - The conditions are checked in top-down priority, so even if more than one is true, whichever one is first has its branch executed; the rest are ignored.
 - If none are true, the final `else` fallback branch is executed; but you don't have to have one if you don't want one.
 - Inside a branch of an `if` statement, you can have as many lines of code as you want — and you can even have whole other multi-branch if statements, if that's what you need.
 - Try to indent the code within each branch by two spaces, especially if you have multiple nested `if` statements within one another.

Consider this small program, and answer the quiz question:

```ruby
n = 15

if n < 12
  s = "first part"
elsif n > 20
  s = "second part"
elsif n < 18
  s = "third part"
else
  s = "fourth part"
end

pp "It picked the " + s
```

- In the above code, what would the full printed out statement be? Try to _think_ through it, and then experiment in the previous runnable code block if you need to!
- It picked the third part
    - Yes!
{: .free_text #multibranch_picks title="Think through it!" points="1" answer="1" }

## truthiness and falsiness

Why did I say "truthy" and "falsy" instead of just `true` and `false`? Because many — most — Ruby expressions return values other than `true` or `false`. _Any_ expression can appear next to an `if`, and some will cause the code inside the `if` statement to execute (these values are known as "truthy") and some will not (these are "falsy").

In the runnable code block below, replace `true` with each of the following. Before clicking "Run" for each one, ask yourself, do you expect to see the output `"The expression is truthy."` or not?

 - `0`
 - `"false"`
 - `[]`
 - `nil`
 - `1 == 1`
 - `""`
 - `false`

```ruby
if true # Replace this with each expression.
  pp "The expression is truthy."
else
  pp "The expression is falsy."
end
```
{: .repl #truthy_falsy title="Truthy or Falsy" points="1"}

For how many of the above did you correctly predict the output? What did you learn about what objects count as truthy and what objects count as falsy in Ruby?

- Which of the expressions is "falsy"? Choose all that apply.
 - `0`
    - Nope.
 - `"false"`
    - Nope.
 - `[]`
    - Nope.
 - `nil`
    - Yes!
 - `1 == 1`
    - Nope.
 - `""`
    - Nope
 - `false`
    - Yes!
{: .choose_all #falsy title="Which are falsy?" points="2" answer="[4,7]" }

----

<p style="height: 200px"></p>

----

## Comparisons

It turns out that **only `false` and `nil` are falsy**. _All_ other objects in Ruby are truthy — even `0`, `""`, and `[]`.

That said, we'll mostly use expressions after `if` that return `true` or `false`. There are a lot of methods that are designed to do this; we've seen `Integer`'s `.odd?` and `.even?`, but there are a lot more.

For example, most classes have ways to compare _instances_ of the class to one another:

```ruby
1 < 2          # "1 is less than 2"
2 < 1          # "2 is less than 1"
24*365 > 10000 # There are more than 10,000 hours in a year
1 == 1         # "1 is equivalent to 1"
1 == 2         # "1 is equivalent to 2"
1 <= 2         # "1 is less than or equal to 2"
1 >= 2         # "1 is greater than or equal to 2"
1 != 1         # "1 is NOT equivalent to 1"
1 != 2         # "1 is NOT equivalent to 2"
"apple" == "apple"
"apple" != "banana"
```

### Equivalence vs assignment 

Note the difference between the **equivalence operator** — two equals signs, `==` — and the variable assignment operator — one equals sign, `=`. Mixing up the two of them is probably _the_ most common typo programmers make:

```ruby
x = 2

if x = 3
  pp "x is 3"
else
  pp "x is not 3"
end
```
{: .repl #equivalence_vs_assignment title="Equivalence vs assignment" points="1"}

When you ran the code above, what was printed? Why?

We accidentally used the assignment operator instead of the equivalence comparison, and in doing so, we _set_ `x = 3` when we meant to check `if x == 3`.

You will 💯 make this typo, we all do at some point — when your conditional always is going into the `true` branch inexplicably, let this ring a bell!

- The equivalence operator is (and does)...
- `=`, and it checks if two things are the same
    - No, that's the variable assignment operator, and it assigns objects into variables
- `=`, and it assigns objects into variables
    - No, that's the variable assignment operator.
- `==`, and it assigns objects into variables
    - Not quite, look above at the previous section.
- `==`, and it checks if two things are the same
    - Yes! `==` is not the same as `=`
{: .choose_best #equivalence title="The equivalence operator" points="1" answer="4" }

Consider this program:

```ruby
n = "giraffe"

if n != "giraffe"
  s = "first part"
elsif n == "Giraffe"
  s = "second part"
else
  s = "third part"
end

p "It picked the " + s
```

**Think carefully,** after each `if` or `elsif` ask yourself: is this expression resulting in a `true` or a `false`?

- In the above code, what would the full printed out statement be?
- It picked the third part
    - Yes!
{: .free_text #multibranch_conditional title="Pick the giraffe part 1" points="1" answer="1" }

- In the above code, what `String` method could you use to modify `n` and have it print `It picked the second part`? (Hint: have a look at [the `String` lesson](https://learn.firstdraft.com/lessons/69).)
- capitalize
    - Yes! 
- n = n.capitalize
    - Yes!
- n.capitalize
    - Yes!
{: .free_text #multibranch_conditional_v2 title="Pick the giraffe part 2" points="1" answer="[1,2,3]" }

## Get some practice

Here are a couple of graded code blocks for you to work on. Practice is crucial!

### RPS

Write a program below for a simple [rock, paper, scissors](https://en.wikipedia.org/wiki/Rock%E2%80%93paper%E2%80%93scissors) game, with a silly computer that always plays "scissors". Based on the randomly `sample`d `player_move`, write a conditional that prints one of:

* "You won!"
* "You lost!"
* "You tied!"

Remember: `rock` beats `scissors`, `scissors` beats `paper`, and `scissors` ties `scissors`. Get all three tests to pass before you move on.

```ruby
player_move = ["rock", "paper", "scissors"].sample
computer_move = "scissors"
# write your program here
```
{: .repl #rps title="RPS" readonly_lines="[1,2]"}

```ruby
describe "RPS" do
  it "should print 'You won!' if the player move is rock" do
    path = "/tmp/code.rb"

    # specify a player move
    file = File.read(path)
    new_content = file.split("\n")
    new_content = new_content.map { |line| line == 'player_move = ["rock", "paper", "scissors"].sample' ? 'player_move = "rock"' : line }.join("\n")
    File.open(path, 'w') { |line| line.puts new_content }

    expect { require_relative(path) }.to output(/You won!/).to_stdout
  end
end
```
{: .repl-test #rps_test_1 for="rps" title="RPS should print 'You won!' if the player move is rock" points="1"}

```ruby
describe "RPS" do
  it "should print 'You lost!' if the player move is paper" do
    path = "/tmp/code.rb"

    # specify a player move
    file = File.read(path)
    new_content = file.split("\n")
    new_content = new_content.map { |line| line == 'player_move = ["rock", "paper", "scissors"].sample' ? 'player_move = "paper"' : line }.join("\n")
    File.open(path, 'w') { |line| line.puts new_content }

    expect { require_relative(path) }.to output(/You lost!/).to_stdout
  end
end
```
{: .repl-test #rps_test_2 for="rps" title="RPS should print 'You lost!' if the player move is paper" points="1"}

```ruby
describe "RPS" do
  it "should print 'You tied!' if the player move is scissors" do
    path = "/tmp/code.rb"

    # specify a player move
    file = File.read(path)
    new_content = file.split("\n")
    new_content = new_content.map { |line| line == 'player_move = ["rock", "paper", "scissors"].sample' ? 'player_move = "scissors"' : line }.join("\n")
    File.open(path, 'w') { |line| line.puts new_content }

    expect { require_relative(path) }.to output(/You tied!/).to_stdout
  end
end
```
{: .repl-test #rps_test_3 for="rps" title="RPS should print 'You tied!' if the player move is scissors" points="1"}

### Palindrome

Write a program to decide if the randomly `sample`d `word` from the array is a palindrome, meaning that it reads the same backwards as forwards (e.g. "madam"). 

Simply display `true` if it is a palindrome and `false` if it isn't. Do not display `"true"` or `"false"` (as `String`s), display the result of a conditional (`true` or `false`).

(Hint: you will need a couple of methods from the [`String` lesson](https://learn.firstdraft.com/lessons/69). Specifically, one of the `case` methods and `reverse`.)

```ruby
word = ["HanNah", "racecars", "racecar"].sample
# write your program here
```
{: .repl #palindrome title="Palindrome" readonly_lines="[1]"}

```ruby
describe "Palindrome" do
  it "should print 'true' if the input is 'RaDAr'" do
    path = "/tmp/code.rb"

    # specify a word
    file = File.read(path)
    new_content = file.split("\n")
    new_content = new_content.map { |line| line == 'word = ["HanNah", "racecars", "racecar"].sample' ? 'word = "RaDAr"' : line }.join("\n")
    File.open(path, 'w') { |line| line.puts new_content }

    expect { require_relative(path) }.to output(/true/).to_stdout
  end
end
```
{: .repl-test #palindrome_test_1 for="palindrome" title="Palindrome should print 'true' if the input is 'RaDAr'" points="1"}

## Combining conditions with AND and OR

Finally, another handy thing to have in your toolbelt are the **logical operators** `&&` (AND) and `||` (OR). These allow you to combine expressions; try these combined expressions out below:

```ruby
pp 3.odd? && 4.even?
pp 3.odd? && 4.odd?
pp 3.even? && 4.odd?
pp 3.odd? || 4.even?
pp 3.odd? || 4.odd?
pp 3.even? || 4.odd?
```
{: .repl #and_or title="AND OR" points="1"}

When used with `if` statements, this ability is very powerful:

```ruby
pp 3.odd?
pp 4.even?

if 3.odd? && 4.even?
  pp "The combined expression is truthy."
end

pp 3.even?
pp 4.even?

if 3.even? || 4.even?
  pp "The combined expression is truthy."
end
```
{: .repl #and_or_truthy title="AND OR truthy" points="1"}

Basically, `&&` is stricter than `||`; both comparisons have to be true in order for the whole statement to be true when combined with `&&`; either one being true is sufficient for `||`.

Consider the code below:

```ruby
number1 = 10 
number2 = 15
sum = number1 + number2

if sum > 10 && sum < 20
  pp sum
elsif number1 >= 10 || number2 > 20
  if number1 > number2
    pp number1
  else
    pp number2
  end
else
  pp "skipping"
end
```

**Think carefully,** after each `if` or `elsif` ask yourself: is this expression resulting in a `true` or a `false`? Move through the branches until you hit a `pp` statement.

- The above code will print...
- 10
    - Nope.
- 15
    - Yes!
- 25
    - Nope.
- `"skipping"`
    - Nope.
{: .choose_best #branching_and_or title="Branching with AND OR" points="1" answer="2" }

##  Conclusion

That's it for `if` statements. Now we'll have a look at **loops** for iterating.

- Approximately how long (in minutes) did this lesson take you to complete?
{: .free_text_number #time_taken title="Time taken" points="1" answer="any" }

<span style="font-size: large">**When you are done here, close the window and return to Canvas for the next lesson in the series.**</span>

----

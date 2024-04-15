+++
title = "Pyramid how-to"
date = 2022-03-21

[taxonomies]
categories = ["CS1"]
tags = ["python"]
+++

# The Road To Counting Pyramid:
When I was TAing an intro CS course, this was often a hard exercise for folks.
Fortunately, we can do hard things! Once you've seen some examples, I have
faith you can make pyramids up there with the [best of
them](https://en.wikipedia.org/wiki/Sneferu#Building_projects).

We want procedure `def number_pyramid(height)` that takes a positive
integer height and then prints a series of lines that form a pyramid of digits, like so (with dots instead of spaces for clarity):
```
....0.
...1.2.
..3.4.5.
.6.7.8.9.
0.1.2.3.4.
```
We're going to build up to it by solving 3 smaller problems.

1. Star Grid

```
*****
*****
*****
*****
*****
```

2. Counting Grid

```
0.1.2.3.4.
5.6.7.8.9.
0.1.2.3.4.
5.6.7.8.9.
0.1.2.3.4.
```

3. Star Pyramid

```
....*. 	     # line 1
...*.*.      # line 2
..*.*.*.     # line 3
.*.*.*.*.    # line 4
*.*.*.*.*.   # line 5
```

Combining the lessons from each, we'll have no trouble with a counting pyramid

## Star Grid
- Make a line of stars with a loop. 
- Nest line-making inside a second loop to repeat line-making many
  times!

We want many lines of stars.
```
*****
*****
*****
*****
*****
```
Making a line of stars is best done with a loop. You want to print a star *many
times*. Whenever you do something *many times* you should think to make a loop. 
```python
### Line-Maker
line_length = 5 # number of stars in line.
line = ""
n_stars_added = 0
while n_stars_added < line_length:
    line += "*"
print(line)
```
We could run this code and get a line of 5 stars: 
```
*****
```
If we want several lines of stars, we can nest this line-maker code inside a
second loop to repeat its execution.
```python
### Grid-Maker
line_length = 5 # number of stars in line.
total_lines = 6 # number of lines.
n_lines_added = 0
while n_lines_added < total_lines: # outer loop
    ### Line-Maker Code
    line = ""
    n_stars_added = 0
    while n_stars_added < line_length: # inner loop
        line += "*"
        n_stars_added += 1
    print(line)
    n_lines_added += 1
```
We start from the top, defining `line_length, total_lines, and
n_lines_added`. Reaching the outer loop, we see that `n_lines_added=0 < total
lines=6`, and continue to the nested line-maker code. The line-maker code starts a new empty string with `line=""`. We fill the line with stars using the inner loop, and print the completed line. 
```
*****
```
Then, we return to the outer loop (since we've finished the nested bit), check
the condition `n_lines_added=1 < total_lines=6`, and proceed again into the
line-maker code! We start a new empty line, fill it with stars, and print. Now,
the line-maker code has been run twice, so we've printed:
```
*****
*****
```
But the outer loop isn't done! We return to the outer loop, check the
condition, start a new empty line, fill it with stars, print, return to
the outer loop, start a new empty line,... you get the idea. Now, we can run it and get a grid of stars. With `line_length=5` and `total_lines=6`, we get:
```
*****
*****
*****
*****
*****
*****
```
Great! We've seen we can make a line with a loop, and repeat line-making by
nesting one loop inside another loop!
## Star Pyramid
### *Insight: a pyramid is just a grid with some blank spaces*
```
....*. 	     # line 1
...*.*.      # line 2
..*.*.*.     # line 3
.*.*.*.*.    # line 4
*.*.*.*.*.   # line 5
```
#### How many spaces should we add?

For this 5-line pyramid, there are 4 spaces before the first line, 3 before the second line, and so on, all the way down to 0 spaces before the last line. We don't ever need any spaces before the first star at the bottom. But at each higher line, we need an extra space before the stars to make a triangle. So, you can find the number of spaces for a given line by thinking about how many lines must be beneath it.

Say there are `N` lines in the pyramid. At the top, there are `N-1` spaces before the first star, one for each of the `N-1` lines beneath it. In general, there are `N-line_number` spaces before the first star on each line, one for every line below.

```python
def star_pyramid(height):
	line_number = 1
	while line_number <= height:
		line = "" # new line
		spaces_added = 0
		while spaces_added < height-line_number: # add spaces
			line += "."
		stars_added = 0
		while stars_added < line_number: # add as many stars as line-number
			line += "* "
	print(line)
```

## Counting Grid
### *Insight: Add a counter. Instead of stars, add the counter value when filling-out lines*
We're gonna go back to the grid, so we don't spoil the final counting pyramid problem. But the idea is that since we build out the lines with a loop, one symbol at a time, we can change whatever symbol we're adding.

Our old grid-maker code changes in only three places, marked with #'s.
```python
### Grid-Maker
line_length = 5
total_lines = 6
n_lines_added = 0
while n_lines_added < total_lines:
    ### Line-Maker Code
    line = ""
    digit = 0 # we add a variable for which digit to print
    n_digits_added = 0
    while n_digits_added < line_length:
        line += str(digit) # we put a digit in the line instead of a star
        digit = (digit + 1) % 10 # we increase the digit
    print(line)
```
The `% 10` turns `10` into `0`so we can count up again, always adding a single
digit `0-9` and never disrupting our symmetry by printing a two-digit number.

```
0.1.2.3.4.
5.6.7.8.9.
0.1.2.3.4.
5.6.7.8.9.
0.1.2.3.4.
```

tada!

# **now scroll to the top and go build a counting pyramid.**

---


## Same thing but less-edited and with Helper Functions
Everything below this is just the same code as above, styled as helper functions instead of one snippet. Unlcear if it's more or less confusing.

### Star-Grid:
#### *Insight: make a line with a loop, run many times with another loop*
Notice that we can make a line with a loop.
```python
def line_printer(line_length):
	line = ""
	position_in_line = 0
	while position_in_line < line_length:
		line += "*."
	print(line)
```
produces `*.*.*.*.*`
Using another loop lets us repeat that line-making, producing a grid!
```python
number_of_lines = 5
line_length = 5
i = 1
while i <= number_of_lines:
	line_printer(line_length)
```
produces
```
*.*.*.*.*
*.*.*.*.*
*.*.*.*.*
*.*.*.*.*
*.*.*.*.*
```
### Counting Grid:
#### *Insight: Add a counter*
We want to replace those stars with the digits 0-9 in sequence. Since the counting carries-over between lines, like
```
0.1.
2.3.
```
we'll need some way to start a line at a specific number.
So our line_printer needs be told a starting number in addition to line length.
It also needs to let us know what number it ended-on so we can start the next line with the right number.
```python
def line_printer(line_length, starting_num):
	printable_num = starting_num # this makes sure we printing the right number
	line = ""
	position_in_line = 0
	while position_in_line < line_length:
		line += str(printable_num) + "."
		printable_num = (printable_num + 1) % 10 # increments the number we print (%10 turns 10 into 0 again)
		position_in_line += 1
	print(line)
	return printable_num # this lets us track which number it ended with
```
So we can do `line_printer(5,3)` and get `3.4.5.6.7.`
Now, we again do another loop to print multiple lines,
```python
number_of_lines = 5
line_length = 5
i = 1
num_to_print_next = 0
while i <= number_of_lines:
	num_to_print_next = line_printer(line_length, num_to_print_next)
	i += 1
```
and get: 
```
0.1.2.3.4.
5.6.7.8.9.
0.1.2.3.4.
5.6.7.8.9.
0.1.2.3.4.
```

### Star Pyramid:
#### *Insight: A pyramid is just a grid with some blank spaces*
Look at the output; before the stars in each line, there are some number of spaces (dots here for clarity).
```
....*.
...*.*.
..*.*.*.
.*.*.*.*.
*.*.*.*.*.
```
So we're going to want the ability to print some number of spaces before stars in `line_printer`.
```python
def line_printer(line_length, prefix_spaces): # prefix_spaces is the number of spaces before the first digit
    line = ""
    spaces_added = 0
    while spaces_added < prefix_spaces: # first loop, make the spaces/dots.
        line += "."
        spaces_added += 1
    position_in_line = 0
    while position_in_line < line_length: # add the stars to the line like normal
        line += "*."
        position_in_line += 1
    print(line)
```
We can call `line_printer(2, 3, 4)` to print a line with 4 spaces, then 2 digits: `....3.4.`
#### How many spaces should we add?
```
....*. 	     # line 1
...*.*.      # line 2
..*.*.*.     # line 3
.*.*.*.*.    # line 4
*.*.*.*.*.   # line 5
```
Notice that for this height-5 pyramid, there are 4 spaces before the first line, 3 before the second line, and so on, all the way down to 0 spaces before the last line. There are `N-line_number` spaces before the digit on each line.

You find the number of spaces for a given line by thinking about how many lines must be beneath it, (N-line_number).


### Counting Pyramid:
#### *Insight: Same counter trick as last time*
Study the output. There are 4 spaces (replaced with dots for clarity) before the 0.
```
....0.
...1.2.
..3.4.5.
.6.7.8.9.
0.1.2.3.4.
```
So we're going to want the ability to print some number of spaces before digits in `line_printer`.
```python
def line_printer(line_length, starting_num, prefix_spaces): # prefix_spaces is the number of spaces before the first digit
    printable_num = starting_num
    line = ""
    spaces_added = 0
    while spaces_added < prefix_spaces: # first loop, make the spaces/dots.
        line += "."
        spaces_added += 1
    position_in_line = 0
    while position_in_line < line_length: # finish the line printing digits as normal
        line += str(printable_num) + "."
        printable_num = (printable_num + 1) % 10
        position_in_line += 1
    print(line)
    return printable_num
```
We can call `line_printer(2, 3, 4)` to print a line with 4 spaces, then 2 digits: `....3.4.`

And now we just call line_printer a bunch of times.

```python
def counting_pyramid(Height):
	line_number = 1
	printing_digit = 0
	while line_number <= Height:
		num_spaces = Height-line_number
		line_length = line_number
		printing_digit = line_printer(line_length, printing_digit, num_spaces)
		line_number += 1
```
and get:
```
....0.
...1.2.
..3.4.5.
.6.7.8.9.
0.1.2.3.4.
```
tada!








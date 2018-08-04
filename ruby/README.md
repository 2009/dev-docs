# Ruby

[Mastering ruby blocks in less than 5 minutes][4]

## Stuff

### Splat(\*) Operator

[Ruby Splat Manipulation and Destructuring][2]

#### Method Definitions

```ruby
def shout_out(message, *friends)
  friends.each { |f| puts "#{f}: #{message}" }
end

shout_out("Hi there!", "Bob", "Steve", "Dave")
```

```ruby
def shout_out(message, *friends)
  friends.each { |f| puts "#{f}: #{message}" }
end

shout_out("Hi there!", "Bob", "Steve", "Dave")
```

#### Destructuring

[Destructuring Assignment in Ruby][3]

```ruby
letters = ["a", "b", "c", "d", "e"]
first, *second = letters
puts "#{first}, #{second}"
# a, ["b", "c", "d", "e"]
```

This can also be done with block-level arguments:

```ruby
triples = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

triples.each { |(first, second, third)| puts second }
# 2
# 5
# 8

triples.map { |(first, *rest)| rest.join(' ') }
# => ["2 3", "5 6", "8 9"]
```

#### Flattening Arrays

When used on an array the splat operator with split the array into arguments.

```ruby
some_numbers = [1, 2, 3]
up_to_five = [*some_numbers, 4, 5]
p up_to_five
# [1, 2, 3, 4, 5]
```

### Keyword Arguments and Double Splat (\*\*)

Ruby 2.0 introduces keyword arguments, these are essentially replace the common
options hash you see commonly used.

> NOTE: All keyword arguments are required, to have optional keys you must use the
> double splat operator (\*\*).


```ruby
def foo(key:)
  key
end

foo(key: "value") # => "value"
foo({}) # ArgumentError: missing keyword: key
foo(other_key: "other_value") # ArgumentError: missing keyword: key
foo(key: "value", other_key: "other_value") # ArgumentError: unknown keyword: other_key

def bar(key: "default_value")
  key
end

bar(key: "value") # => "value"
bar({}) # => "default_value"
bar(other_key: "other_value") # ArgumentError: unknown keyword: other_key
bar(key: "value", other_key: "other_value") # ArgumentError: unknown keyword: other_key
```

#### With Double Splat (\*\*)

```ruby
def foo(key:, **everything_else)
  [key, everything_else]
end

foo(key: "value", other_key: "other_value") # => ["value", {:other_key=>"other_value"}]
```

## Styleguides

[Rubocop Ruby Styleguide][1]

[1]: https://github.com/github/rubocop-github/blob/master/STYLEGUIDE.md
[2]: http://blog.honeybadger.io/ruby-splat-array-manipulation-destructuring/
[3]: http://po-ru.com/diary/destructuring-assignment-in-ruby/
[4]: https://mixandgo.com/blog/mastering-ruby-blocks-in-less-than-5-minutes

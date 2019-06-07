# Using Symbols For Hash Keys

## Learning Goals

- Review the `Symbol` data type
- Recognize the immutability of symbols
- Compare the use of symbols and strings as hash keys
- Recognize Ruby's alternate syntax for hashes with symbols for keys

## Introduction

We saw that hashes are data structures comprised of key/value pairs. We also saw
that we can create hashes simply by writing out key/value pairs wrapped in curly
braces:

```ruby
dog_one = {
  :name => "Luca",
  :breed => "German Shepherd"
}
#=> {:name=>"Luca", :breed=>"German Shepherd"}

dog_two = {
  :name => "Lola",
  :breed => "Giant Schnauzer"
}
#=> {:name=>"Lola", :breed=>"Giant Schnauzer"}
```

In the previous lessons, we mentioned that hash keys can be any data type. You
also may have noticed, though, that we quickly switched to using
[_symbols_][symbols] for our keys in most of the examples. There is a particular
reason for this.

In this lesson, we're going to discuss symbols and why they are ideal to use as
keys in our hashes. They are so frequently preferred, in fact, that Ruby has an
alternative syntax for writing hashes with symbols for keys.

## Using Symbols for Hash Keys

Just to quickly review, [symbols][symbols] are a scalar data type. They share some
similarities with strings, but instead of being wrapped in quotations, symbols
always start with a colon (`:`):

```ruby
:i_am_a_symbol
```

Every piece of data, including the symbol above, takes up a small amount of
memory on the computer. When we write out a symbol like `:i_am_a_symbol`, Ruby
allocates some memory to that piece of data. If we write out `:i_am_a_symbol`
again somewhere else, Ruby will refer back to that _same allocation in memory_.
We can actually see this by using a method built in to all core data types
called `object_id`:

```ruby
:i_am_a_symbol.object_id
#=> 1525788
:i_am_a_symbol.object_id
#=> 1525788
```

Every time we call `:i_am_a_symbol.object_id` we will get the same integer back.
This integer is Ruby's representation of the location in memory where
`:i_am_a_symbol` is stored.

What happens, though, when we do the same with a string?

```ruby
"I am a string".object_id
#=> 70298611796560
"I am a string".object_id
#=> 70298611847740
```

Different integers are returned. Although these strings are identical when
written, **they take up separate allocations of memory**. Every string we write
is given a **new** allocation. This is because string data can change and Ruby
needs to take this into account.

Symbols, unlike strings, **cannot by changed**. That is to say, symbols are
[_immutable_][immutable]. They are _unique_ in Ruby's eyes, and once created,
always refer to the same point in memory. This works well for hash keys. Once a
key/value pair is defined in a hash, we might change the _value_ of the pair,
but we will likely never need to change the _key_.

Let's look back at the first example in this lesson:

```ruby
dog_one = {
  :name => "Luca",
  :breed => "German Shepherd"
}
#=> {:name=>"Luca", :breed=>"German Shepherd"}

dog_two = {
  :name => "Lola",
  :breed => "Giant Schnauzer"
}
#=> {:name=>"Lola", :breed=>"Giant Schnauzer"}
```

The symbols `:name` and `:breed` are used multiple times in separate hashes, but
refer to the **same allocation in memory**. As we'll see soon, we sometimes deal
with many, many hashes, all with the same keys pointing to different values. If
we use strings, in this case, we would create many, many allocations of
memory. By using _symbols_ for our keys, we only use one! For this reason,
symbols are almost always the best choice for keys when creating hashes.

## Using the Alternate Hash Syntax

When using symbols for keys, we have the option of using an alternative syntax
when defining a hash:

```ruby
dog_one = {
  name: "Luca",
  breed: "German Shepherd"
}
#=> {:name=>"Luca", :breed=>"German Shepherd"}

dog_two = {
  name: "Lola",
  breed: "Giant Schnauzer"
}
#=> {:name=>"Lola", :breed=>"Giant Schnauzer"}
```

A few things have changed. For starters, the symbols `:name` and `:breed` no
longer have a colon before them. Instead, they have a colon immediately _after_,
in place of the hash-rocket.

This syntax only works for keys that are symbols but is similar in syntax to
how other languages like JavaScript write their key/value pairs.

When displaying a hash, Ruby will still display the old hash-rocket format.

You might be wondering, why does this even exist? With the rise in popularity
of JavaScript, full-stack developers got used to writing the following in
JavaScript (what JavaScript developers call "JSON," pronounced like "Jay-sawn"):

```JS
dog_two = {
  name: "Lola",
  breed: "Giant Schnauzer"
};
```

Yep, that's valid JavaScript **and** valid Ruby! In recent times, when defining
a Hash, it has become more common to use this "alternate" format. You'll
definitely see a lot of the old "hash-rocket" syntax. Neither is better or
worse. They're just different ways of expressing the idea of key/value pairs
within a collection.

## Conclusion

Symbols are a great choice to use for keys when constructing hashes. Although
keys can be made from whatever data type we feel is best, symbols come with
some advantages. No matter how many times a symbol is written in your code, Ruby
will consider it to be the same thing, allocating just one location in memory
for the symbol.

## Resources

[Symbols][symbols]

[immutable]: https://en.wikipedia.org/wiki/Immutable_object
[symbols]: https://ruby-doc.org/core-2.6.3/Symbol.html


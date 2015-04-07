#Coding Conventions

**THIS IS NOT A FULL GUIDE. JUST A GENERAL GUIDE FOR PURE BEGINNERS**

A full set of coding conventions can be found at [bbatsov's writeup on Github here](https://github.com/bbatsov/ruby-style-guide)


##Curly Braces vs do...end

Most style guides and best practices state that:

* curly braces {} should be used for one liners
* and do...end should be used for multiline statements

There is also a subtle difference between the two:

**Braces have a high precedence; do has a low precedence. If the method invocation has parameters that are not enclosed in parentheses, the brace form of a block will bind to the last parameter, not to the overall invocation. The do form will bind to the invocation**

The examples below make it more clear:

This:

```
task :rake => pre_rake_task do
  something
end
```
Really means:

```
task(:rake => pre_rake_task){ something }
```

And this with curly braces:

```
task :rake => pre_rake_task {
  something
}
```

really means:

```
task :rake => (pre_rake_task { something })
```

See [Stackoverflow](http://stackoverflow.com/questions/5587264/do-end-vs-curly-braces-for-blocks-in-ruby)  here for more details


##Naming convention
Unlike JS where many developers use ```CamelCase``` for their variable naming conventions, in Ruby:

* For plain variable names: use the ```snake_case``` convention.
* For file and directory names, use the ```snake_case``` convention as well.
* For constants, use the ```SCREAMING_SNAKE_CASE``` convention.
* For Classes and Modules, use the ```CamelCase``` convention.

###Naming functions

For functions that return a boolean value, the name should be suffixed with a ```?```. For example:

```
str.include? "substring"
```

##Strings

###String Concatenation vs String Formatting and Interpolation

```
#bad
email_with_name = user.name + ' <' + user.email + '> '
```
```
#good (with string interpolation)
email_with_name = "#{user.name} <#{user.email}>"
```
```
#good (with string formatting)
email_with_name = format('%s <%s>', user.name, user.email)
```

##Parentheses<a name="parentheses"></a>

In Ruby, parentheses are technically optional but there are times when it should be used to make the code more readable.

According to the [unofficial Ruby style guide](https://github.com/bbatsov/ruby-style-guide), you **do NOT** use parentheses when:

* It involves control flow statements (if-then, unless etc.)
* Its a class, function or uses any language specific "keywords" words like ```puts``` or ```attr_reader```

**You use parentheses for all other method invocations.**

From the aforementioned style guide:

```
class Person
  attr_reader :name, :age

  # omitted
end

temperance = Person.new('Temperance', 30)
temperance.name

puts temperance.age

x = Math.sin(y)
array.delete(e)

bowling.score.should == 0
```
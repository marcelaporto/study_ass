# Assesment Phase 1 - DBC


## Enumerables

1) **#find**
One common task when working with a collection is to find a particular item: find the phone number ending in 8916, find the job applicant with the id 353687559, etc ... To help us perform the task of finding an item in a collection, Ruby's Enumerable module provides the #find method, which we're going to use.
It returns the first one that matches a specific condition.

```
numbers = [1, 2, 4, 5, 3, 9]

numbers.find { |number| number > 4 }
# => 5
nubmers.find { |number| number.even? }
# => 2
```

2) **#select and #reject**

Sometimes we want to find one specific item in a collection. At other times we want to find all the items that meet a condition. Or, that do not meet a condition. This is often referred to as filtering. We create a filter that describes how we'll decide which elements were interested in.
It returns ALL the ones that matches a specific condition.

 #select returns a new array containing the items for which the filter returned a truthy value. #reject does the opposite. It returns a new array containing the items for which the filter returned a falsey value.

```
numbers = [1, 5, 3, 8, 2]

numbers.select { |number| number < 5 }
# => [1, 3, 2]
numbers.select { |number| number.even? }
# => [8, 2]
numbers.reject { |number| number.even? }
# => [1, 5, 3]
```

3) #map

Another common task is transforming items into something based on the items. Ruby provides the #map method to help with this task. The method returns a new array. The new array contains the transformed version of each of the original items. The block passed to the method describes how to perform the transformation.

```
numbers = [1, 4, 7, 3, 9]

numbers.map { |number| number ** 3 }
# => [1, 64, 343, 27, 729]
numbers.map { |number| number * -1 }
# => [-1, -4, -7, -3, -9]
numbers.map { |number| Math.sqrt(number) }
# => [1.0, 2.0, 2.6457513110645907, 1.7320508075688772, 3.0]
```

4) **#reduce**

The final task we'll explore is aggregating the items in a collection. In other words, using the items to build an object or value. If we had an array of prices, we could aggregate them into their total. If we had an array of strings, we could aggregate them into one large string.

One aggregating method that Ruby provides is #reduce. There are different ways to call #reduce. One way is to pass in the starting point for the object that will be built up. So, if we're going to sum an array of numbers, we might pass in zero as the starting value. This value is often referred to as the memo. We also pass a block. Our block will need to take two arguments. When the block is run for each item in the collection, both the item and the memo are passed to the block.


```
numbers = [1, 3, 6, 3, 9]

numbers.reduce(0) { |sum, number| sum + number }
# => 22
numbers.reduce(100) { |sum, number| sum + number }
# => 122
numbers.reduce("Digits: ") { |digits, number| digits + number.to_s }
#=> "Digits: 13639"
numbers.reduce(Hash.new(0)) do |counts, number|
  counts[number] += 1
  counts
end
# => { 1 => 1, 3 => 2, 6 => 1, 9 => 1 }
```

## OOP

The basic programming concepts in OOP are four: The abstraction is simplifying complex reality by modeling classes appropriate to the problem. The polymorphism is the process of using an operator or function in different ways for different data input. The encapsulation hides the implementation details of a class from other objects. The inheritance is a way to form new classes using classes that have already been defined.
Objects are basic building blocks of a Ruby OOP program. An object is a combination of data and methods.  These objects communicate together through methods. Each object can receive messages, send messages and process data.

There are two steps in creating an object. First, we define a class. A class is a template for an object. It is a blueprint that describes the state and behavior that the objects of the class all share. A class can be used to create many objects. Objects created at runtime from a class are called instances of that particular class.

## SQL

* [Good For Keyword Order](https://dev.mysql.com/doc/refman/5.7/en/select.html)
* [Cheat Sheet](http://3.bp.blogspot.com/-_ffTBsyELsM/TfZZOGQf5jI/AAAAAAAAAVc/tdDvI5tuT1Q/s1600/sqlauthority.JPG)


## Nested Data Structures

1) **Convert a Nested Array of Table Data to a Hash**

```
def convert_table (array)
  values = array[1..-1]
  result = []

  values.each do |value|
    i = 0
    values_hash = Hash.new {}

    while i < value.length
      values_hash[array[0][i]] = value[i]
      i += 1
    end

    result << values_hash
  end

  result

end
```


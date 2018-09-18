---
layout: post
title:  "Hash Tables"
categories: jekyll update
---

## Hash Tables ##
One of the data structures that I often found myself using when tackling
coding challenges is the **hash table**, an associative data structure
that can be thought of as a collection of (key, value) pairs. Each key is 
unique and can only be used up to one time in a hash table.

Hash tables allow us to lookup data associated with a key in O(1) time, 
which is highly efficient.  A lot of programming languages provide data structures
with this sort of "dictionary" functionality, such as the object in Javascript,
the Hash class in Ruby, and the Dictionary in Python.

Below is one example of a coding problem where a hash table is highly useful - 
searching for unique terms. In the problem below, the input nums is an array of numbers.
Only one number appears one time.

{% highlight javascript %}
  let singleNumber = (nums) => {
    let store = {};
    for(let i = 0; i < nums.length; i++){
      if(store.hasOwnProperty(nums[i])){
        store[nums[i]] += 1;
      } else{
        store[nums[i]] = 1;
      }
    }


    for(let key in store){
      if(store[key] == 1){
        return parseInt(key);
      }
    }
    return -1;
  };
{% endhighlight %}

In the above problem, we iterate through the array O(N) to
create key, value pairs on the hash table. We then
search through the hash table, with each lookup taking O(1) 
potentially N times, for an O(N) runtime.

One way to create out own hash table is to use a hash code function to manage
lookus in an array of linked lists. Each string "key" is mapped to a 
numeric value using this hash code function, and the resulting code is then mapped
to an index in an array. At this index in the array is a linked list of keys and values,
where we can look up a key.

There are a couple of things to note about this. The hash code can be calculated any way
desired, and the mapping of the hash code to an index can be done however desired.
Nevertheless, it is optimal to avoid **collisions**, cases where keys are mapped to the
same index. If this happens, the index at the array has many elements in its associated linked list.

In the worst case, the runtime for lookup can become O(N)
if collisions are too high. If you were to have 1000 keys that all mapped
to the same index A[1], for instance, lookup on this hash table becomes O(N)
because it degrades into looking throuh a linked list.

Below are some examples of how hash codes can be calcualted and how mapping can
be done from a hash code to an index.

### Hash codes and mapping###
The Java programming language has a built-in hashcode function in the overarching Object class.
This computes a hashcode in various ways, depending on the class inheriting it. In the string class,
the formula is as follows:

$$ s.charAt(0) * 31n-1 + s.charAt(1) * 31n-2 + ... + s.charAt(n-1) $$

The resulting numeric value from the string can then be mapped to an index value using
any technique desired. For instance, we could take the hash code and modulo it by the array
length to get our index:

hashcode(key) % array_length 


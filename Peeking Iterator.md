#Peeking Iterator
##Problem:
Given an Iterator class interface with methods: next() and hasNext(), design and implement a PeekingIterator that support the peek() operation -- it essentially peek() at the element that will be returned by the next call to next().

Here is an example. Assume that the iterator is initialized to the beginning of the list: [1, 2, 3].

Call next() gets you 1, the first element in the list.

Now you call peek() and it returns 2, the next element. Calling next() after that still return 2.

You call next() the final time and it returns 3, the last element. Calling hasNext() after that should return false.  
Follow up: How would you extend your design to be generic and work with all types, not just integer?
##Idea:
call next() of a temp Iterator to realize peek()
```cpp
// Below is the interface for Iterator, which is already defined for you.
// **DO NOT** modify the interface for Iterator.
class Iterator {
    struct Data;
	Data* data;
public:
	Iterator(const vector<int>& nums);
	Iterator(const Iterator& iter);
	virtual ~Iterator();
	// Returns the next element in the iteration.
	int next();
	// Returns true if the iteration has more elements.
	bool hasNext() const;
};


class PeekingIterator : public Iterator {
    Iterator parent;
public:
	PeekingIterator(const vector<int>& nums) : Iterator(nums),parent(nums) {
	    // Initialize any member here.
	    // **DO NOT** save a copy of nums and manipulate it directly.
	    // You should only use the Iterator interface methods.
	}

    // Returns the next element in the iteration without advancing the iterator.
	int peek() {
        Iterator temp(parent);
        return temp.next();
	}

	// hasNext() and next() should behave the same as in the Iterator interface.
	// Override them if needed.
	int next() {
	    return parent.next();
	}

	bool hasNext() const {
	    return parent.hasNext();
	}
};
```
##To Study:
1. We can use base class pointer or reference to refer derived class object  
make use of copy constructor
```cpp
class PeekingIterator : public Iterator {
public:
	PeekingIterator(const vector<int>& nums) : Iterator(nums) {
	    // Initialize any member here.
	    // **DO NOT** save a copy of nums and manipulate it directly.
	    // You should only use the Iterator interface methods.
	    
	}

    // Returns the next element in the iteration without advancing the iterator.
	int peek() {
        return Iterator(*this).next();
	}

	// hasNext() and next() should behave the same as in the Iterator interface.
	// Override them if needed.
	int next() {
	    return Iterator::next();
	}

	bool hasNext() const {
	    return Iterator::hasNext();
	}
};
```
2. modify from guava
```cpp
class PeekingIterator : public Iterator {
    bool hasPeeked;
    int peekedElement;
public:
	PeekingIterator(const vector<int>& nums) : Iterator(nums) {
	    // Initialize any member here.
	    // **DO NOT** save a copy of nums and manipulate it directly.
	    // You should only use the Iterator interface methods.
	    hasPeeked=false;
	}

    // Returns the next element in the iteration without advancing the iterator.
	int peek() {
        if(!hasPeeked)
        {
            peekedElement=Iterator::next();
            hasPeeked=true;
        }
        return peekedElement;
	}

	// hasNext() and next() should behave the same as in the Iterator interface.
	// Override them if needed.
	int next() {
	    if(!hasPeeked)
	    {
	        return Iterator::next();
	    }
	    else
	    {
	        hasPeeked=false;
	        return peekedElement;
	    }
	}

	bool hasNext() const {
	    return hasPeeked||Iterator::hasNext();
	}
};
```
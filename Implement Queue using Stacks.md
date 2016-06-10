#Implement Queue using Stacks
##Problem:
Implement the following operations of a queue using stacks.

+ push(x) -- Push element x to the back of queue.
+ pop() -- Removes the element from in front of queue.
+ peek() -- Get the front element.
+ empty() -- Return whether the queue is empty.  

Notes:  
+ You must use only standard operations of a stack -- which means only push to top, peek/pop from top, size, and is empty operations are valid.
+ Depending on your language, stack may not be supported natively. You may simulate a stack by using a list or deque (double-ended queue), as long as you use only standard operations of a stack.
+ You may assume that all operations are valid (for example, no pop or peek operations will be called on an empty queue).

##Idea:
change order when pop and peek
```cpp
class Queue {
public:
    // Push element x to the back of queue.
    void push(int x) {
        innerStack.push(x);
    }

    // Removes the element from in front of queue.
    void pop(void) {
        stack<int> helperStack;
        while(innerStack.size()>1)
        {
            int current=innerStack.top();
            innerStack.pop();
            helperStack.push(current);
        }
        innerStack.pop();
        while(!helperStack.empty())
        {
            int current=helperStack.top();
            helperStack.pop();
            innerStack.push(current);
        }
    }

    // Get the front element.
    int peek(void) {
        stack<int> helperStack;
        while(innerStack.size()>1)
        {
            int current=innerStack.top();
            innerStack.pop();
            helperStack.push(current);
        }
        int result=innerStack.top();
        while(!helperStack.empty())
        {
            int current=helperStack.top();
            helperStack.pop();
            innerStack.push(current);
        }
        return result;
    }

    // Return whether the queue is empty.
    bool empty(void) {
        return innerStack.empty();
    }
private:
    stack<int> innerStack;
};
```
Time Complexity:push->O(1), pop->O(n), peek->O(n), empty->O(1)  
##To Study:
1. change order when push
```cpp
class Queue {
public:
    // Push element x to the back of queue.
    void push(int x) {
        stack<int> helperStack;
        while(!innerStack.empty())
        {
            int current=innerStack.top();
            innerStack.pop();
            helperStack.push(current);
        }
        innerStack.push(x);
        while(!helperStack.empty())
        {
            int current=helperStack.top();
            helperStack.pop();
            innerStack.push(current);
        }        
    }

    // Removes the element from in front of queue.
    void pop(void) {
        innerStack.pop();
    }

    // Get the front element.
    int peek(void) {
        return innerStack.top();
    }

    // Return whether the queue is empty.
    bool empty(void) {
        return innerStack.empty();
    }
private:
    stack<int> innerStack;
};
```
Time Complexity:push->O(n), pop->O(1), peek->O(1), empty->O(1)    
  
2. use 2 stacks: input, output
```cpp
class Queue {
public:
    // Push element x to the back of queue.
    void push(int x) {
        input.push(x);
    }

    // Removes the element from in front of queue.
    void pop(void) {
        peek();
        output.pop();
    }

    // Get the front element.
    int peek(void) {
        if(output.empty())
        {
            while(!input.empty())
            {
                int current=input.top();
                input.pop();
                output.push(current);
            }
        }
        return output.top();
    }

    // Return whether the queue is empty.
    bool empty(void) {
        return input.empty()&&output.empty();
    }
private:
    stack<int> input;
    stack<int> output;
};
```
Time Complexity:push->O(1), pop->Amortized O(1), peek->Amortized O(1), empty->O(1) 
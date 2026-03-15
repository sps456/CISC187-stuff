## Activity 6: Stacks and Queues
1. Stack Demonstration Illustration
2. Queue Demonstration Illustration
3. Under and Overflow checking in Queue

Updated Pseudocode of Enqueue:
```
if (Q.head == Q.tail + 1) or (Q.head == 1 and Q.tail == Q.length)
  print "Unable to enqueue since queue is full"
else
  Q[Q.tail] = x
  if Q.tail == Q.length
      Q.tail = 1
  else Q.tail = Q.tail + 1
```
Updated Pseudocode of Dequeue:
```
if Q.head == Q.tail
  print "Unable to dequeue since queue is empty"
else
  x = Q[Q.head]
  if Q.head == Q.length
      Q.head = 1
  else Q.head = Q.head + 1
  return x
```
4. Pop and Push operations for head and tail of a Deque

The Pop Head and Push Tail methods for a deque will look pretty much identical to the Enqueue and Dequeue methods for a queue:

Pseudocode of PopHead:
```
if Q.head == Q.tail
  print "Unable to pop head since deque is empty"
else
  x = Q[Q.head]
  if Q.head == Q.length
      Q.head = 1
  else Q.head = Q.head + 1
  return x
```
Pseudocode of PushTail:
```
if (Q.head == Q.tail + 1) or (Q.head == 1 and Q.tail == Q.length)
  print "Unable to push tail since deque is full"
else
  Q[Q.tail] = x
  if Q.tail == Q.length
      Q.tail = 1
  else Q.tail = Q.tail + 1
```
The Pop Tail and Push Head methods will look like the inverse of their counterparts:

Pseudocode of PopTail:
```
if Q.head == Q.tail
  print "Unable to pop tail since deque is empty"
else
  if Q.tail == 1
    x = Q[Q.length]
    Q.tail = Q.length
  else
    x = Q[Q.tail-1]
    Q.tail = Q.tail - 1
  return x
```
Pseudocode of PushHead:
```
if (Q.head == Q.tail + 1) or (Q.head == 1 and Q.tail == Q.length)
  print "Unable to push head since deque is full"
else
  if Q.head == 1
    Q.head = Q.length
    Q[Q.head] = x
  else
    Q.head = Q.head - 1
    Q[Q.head] = x
```

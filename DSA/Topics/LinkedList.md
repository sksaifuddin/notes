## Common techniques

## Iterating LinkedList

For almost all LinkedList problems you have to iterate through the list. Its quite simple, but its the first thing that should come to the mind when you see LinkedList problem.
```python
current = head
while current is not None:
	print(current.val)
	current = current.next
```

### Dummy Head

You create a fake/dummy node at the start of your list that doesn't hold any real data. You build your result list starting from this dummy, and at the end you return `dummy.next` as your actual answer.
```python
dummy = ListNode(0)  # fake node, value doesn't matter
curr = dummy          # use curr to build the list

# ... do your work, attaching nodes to curr ...

return dummy.next     # the real result starts here
```

Without a dummy head, you have to handle the **first node as a special case**, which leads to messy `if` checks. The dummy node eliminates that entirely — every node, including the first real one, gets added the same way.

example problem: https://leetcode.com/problems/merge-two-sorted-lists/description/

### Fast and slow pointer 

Also called Floyd's Tortoise and Hare algorithm

if we move two pointer in a LinkedList and make one move by one node and another (fast) by two nodes, and if there is a cycle they will eventually meet each other. Very helpful and easy algorithm to detect cycles.
```python

 def hasCycle(self, head):
        slow, fast = head, head
        while fast and fast.next:
            fast = fast.next.next
            slow = slow.next
            if fast == slow:
                return True
        return False
```
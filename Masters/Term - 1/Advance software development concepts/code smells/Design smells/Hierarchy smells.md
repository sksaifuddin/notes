### 1. Rebellious Hierarchy:

This smell arises when a subtype rejects the methods provided by its supertype.
	Rejection meaning:
		1. Throw an exception
		2. provide an empty method
		3. provide a method definition that just prints "should not implement message".

### 2. Cyclic hierarchy

This smell arises when a supertype in a hierarchy  depends on any of its subtypes.  
This dependency could be in the following forms:  
• a supertype contains an object of one of its subtypes  
• a supertype refers to the type name of one  of its subtypes  
• a supertype accesses data members, or calls methods defined in one of its subtypes.

### 3. Broken hierarchy

This smell arises when a super type and its subtype do not share an "IS-A" relationship
There can be two types of refactorings code wise:
1. Implementation code refactoring
2. Design/architectural refactoring.

They both involves improving the code quality but changes in scope of the refactoring. Implementation involves changes in method or component level, design/architectural involves changes in architecture or design of the system.

## Implementation refactorings:

### 1. Renaming variables:
Making variable more understandable. It should define the behaviour of the method or the variable. It should align with coding styles of the project.

### 2. Extract method:
when the method is doing two separate things it violates SRP. The responsbilities can be split and made into two different methods by passing appropriate parameters. 

Class example:
```java
void printAppObjects(cInvoice *invoiceObj, list<cItem *> itemContainer)  
{  
list<cItem*>::iterator itemItr = itemContainer.begin();  
while(itemItr != itemContainer.end())  
{  
cout<<(*itemItr)->getItemName()<<endl;  
cout<<(*itemItr)->getItemPrice()<<endl;  
cout<<(*itemItr)->getItemTaxes()<<endl;  
}  
cout<<"Total items:"<<invoiceObj.getItemCount()<<endl;  
cout<<"Total amount:"<<invoiceObj.getTotalAmount()<<endl;  
cout<<"Total taxes:"<<invoiceObj.getTotalTaxes()<<endl;  
}  
Two  
separable  
code blocks
```

This can be converted to:
```Java

void printAppObjects(cInvoice *invoiceObj, list<cItem *> itemContainer){  
printAllItems(itemContainer);  
printInvoiceObj(invoiceObj);  
}  
void printAllItems(list<cItem*> itemContainer) {  
list<cItem*>::iterator itemItr = itemContainer.begin();  
while(itemItr != itemContainer.end()) {  
cout<<(*itemItr)->getItemName()<<endl;  
cout<<(*itemItr)->getItemPrice()<<endl;  
cout<<(*itemItr)->getItemTaxes()<<endl;  
}  
}  
void printInvoiceObj(cInvoice *invoiceObj){  
cout<<"Total items:"<<invoiceObj.getItemCount()<<endl;  
cout<<"Total amount:"<<invoiceObj.getTotalAmount()<<endl;  
cout<<"Total taxes:"<<invoiceObj.getTotalTaxes()<<endl;  
}
```

### 3. Split temporary variable:

If there are multiple responsibilites for a single temp variable, meaning a single variable is being used for storing multiple logical values then we should create two variables instead of one.

Better way:
```Java
area = length * width;  
printf(“Area=%f”, area);  
volume = length * width * height ;  
printf(“Volume=%f”, volume );  

```


### 4. Decompose conditional:

This arises when its a complex conditional. Complicated conditional logic with their actions make code harder to read and understand.  The ‘Decompose conditional’ Refactoring introduces another layer of abstraction and encapsulates complex conditional logic and corresponding actions into separate methods.
```Java
if(itemObj.getAvailableUnits() > requiredUnits &&  
itemObj.getExpiryDate()>date() && itemObj.getUnitWeight()==  
requiredUnitWeight){  
...  
}  
else{  
...  
}
```

Better way:
```Java
if(isItemSellable(...)){  
...  
}  
else {  
...  
}  
int isItemSellable(...) {  
return (itemObj.getAvailableUnits() > requiredUnits &&  
itemObj.getExpiryDate()>date() && itemObj.getUnitWeight()==  
requiredUnitWeight);  
}
```

similar refactoring is consolidate conditional expression:
```Java

if (itemObj.getAvailableUnits() < requiredUnits) return 0;  
if (itemObj.getExpiryDate()<=date() ) return 0;  
if (itemObj.getUnitWeight()!= requiredUnitWeight) return 0;  
//sell the item  
if(isItemNotSellable()) return 0;  
```

Better way:
```Java
//sell the item  
int isItemNotSellable(){  
return (itemObj.getAvailableUnits() < requiredUnits ||  
itemObj.getExpiryDate()<=date() ||  
itemObj.getUnitWeight()!= requiredUnitWeight);  
}
```

### 5. Explaining variable:

A complicated expression can be replaced by an explaining variable. Identify a sub-expression from a complicated  expression. Put this sub-expression into a temporary variable which explains the purpose of the sub-expression.

```Java

/**
Bad way of writing code
**/
double calculatePrice(int quantity, float itemPrice) {  
return ((quantity * itemPrice) - (max(0, (quantity - 500)) * itemPrice * 0.05));  
}  

/** 
Good way of add the complicated expression to new variable.
**/
double calculatePrice(int quantity, float itemPrice){  
double discount = max(0, (quantity - 500)) * itemPrice * 0.05;  
return ((quantity * itemPrice) - discount);  
}  
discount
```

### 6. Consolidate duplicate conditional fragments:

if an expression is duplicate in conditional statements like it is present in both if and else, then it should be made outside the if-else block to avoid duplication.
If the block of common code is at the  
beginning, move it to before the conditional.  
• If the block of common code is at the end,  
move it to after the conditional.  
• If the common code is in the middle, consider  
splitting the conditional.  
• If the common block is more than a single  
statement, consider making a method out of  
the common block.

### 7. Parameterized method:

A set of methods implementing variations in a single task.  
Mechanism  
• Create a parameterized method that can be substituted for each repetitive method.  
• Pass appropriate additional parameters.  
• Replace old method calls to new method.  
• Compile and test for all variations.

Class example:
Two methods rotate180() and rotate90() can be made a single method by just passing a parameter of how much you want to rotate instead of making two methods. rotate(int angle);

[[Advance Software development concepts]]


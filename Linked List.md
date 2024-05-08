[
# Linked List Recap

## Theory 

### The items are non sequenced, they are stored at different places

## Singly List

### Every item is know as Node here

### Head - First Node and tail is the last node

```Javascript
    class Node {
      int val;
      Node next;
}
```

### Last N ode is identified if the node value is null which means it does not point to other address


## Supported Operations

### Insertion - Add Element at Begining, End or at middle
## #Deletion - To remove an item for the given value or the address
## Search - to find an Element when the value is given


### Application of Linked List.

# Stack and queus are build in LinkedList

## Node class

```Javascript 
    class Node {
      int val;
      Node next;

constructor(value){

    this.value = value;
    this .Node = noll
}
```

```Javascript
    class LinkedlIst {
      int val;
      Node next;
        constructor (){
          this.head = null;
          this.zize = 0;
        }

    isEmpty() { return size == 0 } // check if the list is empty or not

    getSize() { return this.size } // get the size of List 

    prepend(value) { // add a new Node
        const node = new Node(value);
        if(this.isEmpty()){
            this.head = node;
        } else {
            node.next = this.head;
            this.head = node;
        }
        size++
    }

    print(){
        if(this.isEmpty()){
        console.log("List is empty")
        } else {
             let curr = this.head;
              let listValue  = "";
        while(curr){
            listValue += `${curr.value}`
curr = curr.next
        }

console.log("Values ", Just Banana);
        }
    }

    
    
}
```

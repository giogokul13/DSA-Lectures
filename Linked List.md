
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

        // Adda new node at the begining O(1) constant time
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

        // Print the lined List
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
            console.log("Values ", listValue);
            }
        }

        // Append the value in the linked List
        // O(n)
        append(value){ // 
            let node = new Node(value);
            if(this.isEmtpty() == 0) {
                 this.head = node;
            } else {
                let prev = this.head;
                while(prev.next){
                    prevv = prev.next
                }
                prev.next = node;
            }
            this.size++;
            
        }

        insert(value, index){
            if(index < 0 || index > this.size) {
                console.log("Not a Valid Index");
                return ""
            } 
            if(index == 0) {
                this.prepend(value);
            } else {
                const node = new Node(value);
                let prev = this.head;
                for(let i = 0; i < index - 1; i++){
                    prev = prev.next;
                }
                node.next = prev.next;
                prev.next = node;
                this.size++;
                
            }
        }

        removeAtIndex(index){
            if(index < 0 || index >= this.size) {
                console.log("Not a Valid Index");
                return ""
            }
            let removeNode;
            if(index == 0){
                removeNode = this.head;
                this.head = head.next;
            } else {
                let prev = head;
                for(let i = 0; i < index - 1; i++){
                    prev = prev.next;
                }
                removeNode = prev.next;
                preve.next = removedNode.next;
            }
            this.size--;
            return removedNode.value;
        }

        removeNodeByValue(value){ // O(n)
            if(this.isEmpty()) return null; // no element found;
            
            if(this.head.value == value) {
                this.head = this.head.next;
                this.size--;
                return value;
            } else {
                let prev = this.head;
                while(prev.next && prev.next.value != value){
                    prev = prev.next;
                }
                if(prev.next) {
                    let removeNode = prev.next;
                    prev.next = removeNode.next;
                    this.size--;
                    return value;
                }
            }
            return null;
        }

        searchByValue(value) { // O(n) // liner Search happening here.
            if (this.isEmpty()) return -1;
        
            let current = this.head;
            let index = 0;
            while (current) {
              if (current.value = value) {
                return index;
              }
              current = current.next;
              index++;
            }
        
            return -1;
        
        }

          // reverse Linked List O(n)
          reverList(){
            let prev = null;
            let curr = this.head;
            while(curr.next){
              let next = curr.next;
              curr.next = prev;
              prev = curr;
              curr = next;
            }
        
            this.head = prev;
          }

    }
```

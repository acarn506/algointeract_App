# algointeract_App

### My contributions on the development of algointeract.com

## Purpose of algointeract

- Collaborated with a team to develop an interactive web app featuring and modeling data structures to provide assistance to fellow Computer Science students and professors. 

- Help a student understand the fundamental aspects of basic data structure

- Curious of how your data might work within a certain algorithm

## Algorithm Highlight Feature 

![Highlight Clip](clips/algo_clip.gif)

### Clip Description

Graph Visualizer performs a Breadth-First Search on an undirected graph by simply entering in the start and end destination, selecting the algorithm, and press the start button.  

### Code

The method below would be executed by our algorithms when they moved from one node to the next depending on the selected algorithm where the color of the node would change to produce a visual presentation of the algorithm’s movement.

```javascript
//Highlight Node -> Parameter: Node id
highlightHandler = (id) => {
  //Get index of the node
  const nodeIndex = this.state.data.nodes.findIndex((node) => {
    //return node index that matches the passed id
    return node.id === id;
  });

  const origNode = {
    ...this.state.data.nodes[nodeIndex],
  };

  const newNode = {
    ...this.state.data.nodes[nodeIndex],
  };

  //Set colors for new node
  newNode.color = "gold";
  newNode.strokeColor = "orange"; //node outer color

  //create a copy of the entire nodes state
  const nodes = [...this.state.data.nodes];
  //store newNode updates at the proper index of the copy
  nodes[nodeIndex] = newNode;

  //update original state with the new state
  this.setState({
  data.nodes : nodes
  });
  //call to reset back to original state
  //this.resetState(origNode, nodeIndex);
};
```

Reset nodes back to their original color after algorithm has finished

```javascript
//reset node color back to original
resetState = (counter) => {
  const myP = new Promise(function (resolve, reject) {
    // promise for time delay
    setTimeout(() => resolve("Successful Switch!"), 2000 * (counter - 2));
  });

  this.sucessHandler = (msg) => {
    // If things go well
    console.log(msg); //check console for msg from resolve
    const origNodes = this.state.data.nodes;

    origNodes.forEach((node) => {
      node.color = this.state.nodeColor;
      node.strokeColor = this.state.strokeColor;
    });

    this.setState({
    data.nodes : origNodes
    });
  };
  //calls when promise is resolved
  myP.then(this.sucessHandler);
};
```

## Linked List Interface 

![Linked List Clip](clips/linkedlist.gif)

### Clip Description 

Append and prepend a few extra nodes to the constructed linked list, select algorithm tab, enter target value to search for, and press the start Linear Search button to find the requested node.  

### Code 

Linear Search Algorithm 

```javascript
 linearSearch = () => {

   var counter = 0;
   // listOrder is an array that contains the order of the linked list elements 
   for (let i = 0; i < this.state.listOrder.length; i++) {
   
     // check if keyNode string equals current node's id string
     if (this.state.algoData.keyNode === this.state.listOrder[i]) {
       console.log("found key node");
       
       // if target node is found, node flashes green 5 times 
       for (let j = 0; j < 5; j++) {
         setTimeout(
           () => this.foundTarget(this.state.algoData.keyNode),
           1200 * counter
         );
         counter++;
       }
       break;
     }
     
     // highlight nodes/links as the algorithm traverses
     setTimeout(
       () => this.highlightHandler(this.state.listOrder[i], counter),
       1000 * (counter + 1)
     );
     counter++;
   }
   // Once algo finishes set back to original node color
   this.resetState(counter);
 };
```
The logic I used for appending a node to a linked list is practically the same traditional format compared to any other language.  The difference in the code was having to maintain state management as I had to copy current states and update them with the new state. 

```javascript
appendNode = () => {

  //get link list tail and the newly added node
  let listInfo = this.state.listInfo;
  let newNode = this.getNewNode();
  
  // create copy of listOrder
  let newList = [...this.state.listOrder];
  // push new node's id (a string) onto newList
  newList.push(newNode.id);
  // update listOrder with newList
  this.setState({ listOrder: newList });

  //find the new tail index
  let tailIndex = this.state.data.nodes.findIndex((node) => {
    return node.nodeid === listInfo.tail;
  });
  
  //create instance of the tail node
  const tailNode = {
    ...this.state.data.nodes[tailIndex],
  };
  
  //assign current tail to new node
  tailNode.next = newNode.nodeid;
  //copy array of nodes
  let newNodes = [...this.state.data.nodes];
  //update copy of nodes
  newNodes[tailIndex] = tailNode;
  //update tail to point to the new tail node
  listInfo.tail = newNode.nodeid;
  //update state of nodes and tail state
  this.setState({
    listInfo: listInfo,
  });

  this.setState({
  data.nodes : newNodes
  });

  this.setState({ listOrder: newList });

  //update link state
  this.state.data.links.push({
    source: tailNode.id,
    target: newNode.id,
  });
};
```

# algointeract_App

### My contributions on the development of algointeract.com

## Purpose of algointeract

- Collaborated with a team to develop an interactive web app featuring and modeling data structures to provide assistance to fellow Computer Science students and professors. 

- Help a student understand the fundamental aspects of basic data structure

- Curious of how your data might work within a certain algorithm

## Algorithm Highlight Feature 

![Highlight Clip](clips/algo_clip.gif)

### Code

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

The method our algorithms would call as they move from one node to the next depending on the selected algorithm where the color of the node would change for highlighting presence and update the new state.

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

## Linked List Interface 

![Linked List Clip](clips/linkedlist.gif)

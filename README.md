# algointeract_App

My contributions on the development of algointeract.com

![Highlight Clip](clips/algo_clip.gif)

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
      ...(this.state.data.nodes = origNodes),
    });
  };
  //calls when promise is resolved
  myP.then(this.sucessHandler);
};

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
    ...(this.state.data.nodes = nodes),
  });
  //call to reset back to original state
  //this.resetState(origNode, nodeIndex);
};
```

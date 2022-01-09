<h1 align="center">Introduction to Graph Machine Learning</h1>

<p align="justify">
This is an introductory blog post, where we will cover all the basics, in order to start with GraphML. Later parts will cover details regarding each of the Graph Machine learning topics and hands on experieces with Graph Neural networks in PyTorch Geometric.
</p>

## Why Graph ML is now a days so much popular?
<p align="justify">
The traditional machine learning techniques, like simple linear regression, naive bayes,decision trees,random forests, SVMs, SVRs which are nothing but a blend of statistical Inferences and computational algorithms. But with the rising complexity of the data, w.r.t structural changes and increasing dimensionality, which can be seen in  images, texts, wave-forms, graphs etc, these kind of algorithms started to give less promising and generalised results and facing the classic problems like curse of dimensionality, easy underfitting or overfitting of the models. 
</p>

<br>
<p align="justify">
So, when traditional machine learning algorithms seemed to getting failed with increasing complexity of data, that time a new subset of Machine learning called deep learning emerged out. And all deep learning algorithms from oldest to the latest one, revolves around the foundations of the architecture called Neural Networks. Based on those two more fundamental architectures, CNN for images and RNN for sequential data emerged out, and were very much successful in learning and generalising universal approximation functions for complex data like images and sequential data like texts, waveforms etc. 
</p>

<br>
<p align="justify">
But here comes the twist. Till now, we were discussing were all falling under a category of structured data. These all types of data, like tabular data, image, texts etc are all some kind of ecluidian data. And this ecluidian origin makes their learning/optimization easy and stable. But what about the Graphical data. Graphical data are actually so much ubiqutous in nature, that it can be seen everywehere. Some of the examples are:
</p>

1. The internet itself.
2. The facebook network of friends
3. Molecular structures
4. Our Brain (combination of millions of neurons)
5. 3D shapes, etc.

<p align="justify">
Even the images and texts or the waveforms can be seen and translated as a graphical data. But those type of graphical data are kind of trivial. As those are structured, unlike general graphical data. So predicting something which is based on non-ecluidian subspace is difficult for traditional deep learning or machine learning models. Because, we all know that graphs do not have any certain length or shape. And how we should represent the edges. How to represent the connections. Now here anyone comes with the answer that we can use adjacency matrices. But then think of we are talking at a scale, where we have to compute giant graphs, like facebook's network of users and their friends. So for all these un-certainities, we can not use simple MLP or MLP based models to figure out an optimized solutions. And so for this a new subset of Machine Learning comes into play, which are known as Graph Machine Learning. 
</P>

## So, what are Graphs.
<p align="justify">
A graph is nothing but a collection of different nodes, which are connected with some links called as edges. Mathematically we can define a graph as :
</p>

```
                                                G = (V, E, A)
```
<p align="justify">

Where `G` represents a graph, and `V` represents a collection of nodes: `{ v1, v2 …. vn}` and `E` represents collections of edges: `{e1, e2, ….. em}`  and `A` represent the topological structure by defining the adjacency matrix.
</p>

<p align="justify">
So this is how we generally represent a graph structure. Now we might have read in some courses like data structures, that graphs are one of the essential data structures for path finding algorithms. This is true. But if we see, then we generally deal with nodes, which are often represeneted as some numbers like 1,2,3 ... or some letters like A,B,C, ... But in Machine learning, the nodes we see, do not contains some single numbers or letters. We represent each of the nodes and sometimes the edges as vectors. And so, these nodes containing some vectors within them are known to be as node features. If edges are also represented as some vectors, then we define that as edge features. Now, sometime people gets confused, by considering edge features representing the connections of the graphs. This is wrong assumption. Edge features are some kind of optional features, we use in graph ML other than node features, which helps us to learn the underlined reprsentation in a more clear way. But these edge features are not the reprentatives of the connection within the nodes. Connections are represented as Adjacency matrix. For example, we can think a chemical molecule as a graph. The nodes represent the atoms, and the edges represents the different types of the bonds, like single bond, double bond etc. So for representing the types of the bond, we require some features, that is represented through edge features. Edge features are not important as node features everytime. Also we will discuss more on details in the later parts.
</p>

## Node features
<img src= 
"https://www.researchgate.net/profile/Hongyang-Gao/publication/326496656/figure/fig1/AS:652202121109508@1532508511971/An-illustration-of-graph-data-There-are-7-nodes-in-this-graph-and-each-node-has-3.png" 
         alt="Node features image" 
         align="right"
         width="300" height="200"> 
         
<p align="justify">
Node features are the fundamental input for graph machine learning models. This is simply the feature vector a node of a graph is carrying. Mathematically a graph `G = (V, E)` where, `V` is the set of nodes. All the nodes v those belongs to `V` are a `d-dimensional` vector. Those d-dimensional vectors are the node feature vectors. So if there are N Nodes and every nodes is having d-dimensional features, so the input matrix X is a N x d matrix. Some simple example might include, suppose in a molecular graph, the nodes are the atoms, and each atoms may have several properties like:
```
 atomic number, 
 mass num, atomicity, 
 hybridization of the atom
```
All these are some numerical value features, and when stacked together turns out to be a vector.
  
</P>

## Edge Features

<img src= 
"https://user-images.githubusercontent.com/58508471/148685249-358ee95a-9753-4113-b9d6-53f871daee48.png" 
         alt="Node features image" 
         align="left"
         width="400" height="300"> 
         
<p align="justify">
Edge features are similar to edge features, but **Edge features do not represent the connection in between the nodes of the graphs** As mentioned in the earlier example, we already know that atoms can be considered some sort of small graphs, and these atoms have different types of bonds, which can be considered as edges of the graphs. So different kinds of properties like:
  ```
  Type of the bond (single, double, triple),
  Bond angle,
  Other some sort of chemical properties of the bonds, which have some sort of numerical/boolean values
 ```
  All of these when stacked upon each others forms a vectors of suppose `m` dimension. This vector formed is known as edge features of the graphs. In most of the scenerios, edge features are generally been ignored, as they are sometimes less significant then node features. 
</p>

 ## Graph Features
 
<p align="justify">
These are the features, that represents the whole graphs. Now, we can not aquire the features of graphs directly. We indirectly get that from the node and/or the edge features. For sake of simplicity, suppose our graphs has only node features. Now we process these node features, by passing them into some black box, called GNN layers. And we get some more refined representation of the nodes (also known as embeddings, more about embeddings would be discussed in the leter part). Now those embeddings are also nothing but a matrix (stacked vectors of different node embeddings). And we do some kind of an operation, such that we convert this `(N x D)` (where N = number of nodes, D = number of features of each node), into an N dimensional vector, such that each element of the vector represents a collective feature of each node. All togather forming a representation of the graph. The operation done generally in this vase is called `global graph pooling.` More will be covered in later blogs.
 </p>
 
 
## Adjacency matrix and Adjacency lists
<img src= 
"https://user-images.githubusercontent.com/58508471/148685786-2f81bfff-d760-46a8-985c-4709e8c7c79c.png" 
         alt="Node features image" 
         align="left"
         width="400" height="300"> 

<p align="justify">
Adjacency matrix is the one way in which we store the connections between the graphs. An element will  be 1 (or a value in case of a weighted graph) if there exists some kind of connection between the nodes else it will be 0. But here is a problem. Consider a giant graph, which is as big as facebook social network. In this case, most of the entries are zeros, making the graph a highly sparse matrix. Algorithms based on that would be highly in-efficient based on space. An alternative to the adjacency matrix is adjacency list or coordinate format. There are different ways to represent adjacency list. For e.g taking a group of tuples, where each tuple represent the nodes source and target node connection.
</p>

<img src= 
"https://user-images.githubusercontent.com/58508471/148686002-7dbc66f2-3425-4fd1-858a-f51392558c26.png" 
         alt="Node features image" 
         align="right"
         width="500" height="200"> 
<br>
<p align="justify">

  
  
   We can take two list or a 2d matrix of 2 rows and m-columns, where m is the total number of valid connections, where the first row is the source and the other is the target. The figure shows the connections in COO format of the same graph.
</p>

#
## Embeddings
<img src= 
"https://user-images.githubusercontent.com/58508471/148686294-159b762e-ea7c-4837-af41-21ae4e5762ec.png" 
         alt="Node features image" 
         align="left"
         width="400" height="300"> 

This is the one of the most important concept which is not only important in GraphML but also in general. We generally hear this word from NLP field the most. But we know that embedding is everywhere. 
Defining an embedding is easy, its simply we initially get a high dimensional input data (such as word from corpuses) , and we make a method such that it is translated into low dimensional representations. And this representations learns the schementics of the given input, such that we get to observer that similar kind of input are similar to each others. 
For example, if we get three words `{“king”, “queen”, “hello”}`. Here `king` and `queen` haver quite a similar kind of embeddings as both represents `persons, elite classes, something based on history etc`. Where as the word `Hello` is a `greetings`, which does not share the similar kind of schementics.

**So What are embeddings in Graphs**
<p align="justify">
  Now if we know what embeddings are, then it's easy to know what embeddings in graphs would mean. Suppose we are given a graph, and let us considers, we have node and/or edge features. Initially we have some kind of values of this features, and we can not find any kind of relations of different nodes and/or edges by just examining those features. So we do some kind of operations on graphs, such that we transforms those input features into some kind of representations, and those representations group the similar kind of nodes and/or edges together. If you see in this example figure, then  we will see that initially the nodes of the graph, do have kind of similar kind of values, but we apply some function f such that it captures some kind of schementaics from the neighbours and you can see from the blend of the colour. After some time, we can see that nodes with similar kind of representations stays together with lesser distances, where as nodes with relative less similar representations tends to stay far from each other spatially.  The example picture below to the first one shows an example of the before and after learnimg the  representation of a real world knowledge graphs. 
</p>


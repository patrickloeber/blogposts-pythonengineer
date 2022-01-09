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
<p align="justify">
<img src= 
"Assets/Anindya/node_feat.png" 
         alt="Food and Computer Image" 
         align="right"
         width="300" height="300"> 

Node features are the fundamental input for graph machine learning models. This is simply the feature vector a node of a graph is carrying. Mathematically a graph `G = (V, E)` where, `V` is the set of nodes. All the nodes v those belongs to `V` are a `d-dimensional` vector. Those d-dimensional vectors are the node feature vectors. So if there are N Nodes and every nodes is having d-dimensional features, so the input matrix X is a N x d matrix. Some simple example might include, suppose in a molecular graph, the nodes are the atoms, and each atoms may have several properties like:
{atomic num, mass num, atomicity, hybridization …}, these are some numerical value, and when stacked together turns out to be a vector.
</P>
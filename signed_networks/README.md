
# Community detection in regular an signed networks

Due to the general concept of what a network is they have become one of the most common tools while studying complex systems, and are used in a number of fields of statistical physics and data science. In many cases, nodes of the network can be grouped into different communities in such way that nodes from the same communities have similar topological features suggesting that these partition exists in the real system too. Hence, finding communities in efficient ways is an important problem in network science.

In the last few decades several community detection method has been published with a different ideas and implementations, but their effectiveness highly depends on the circumstances of the original problem. However, the notion of modularity is a widely used measure to quantify how good is a given partition of a network, because it captures the basic features of what is thought to be a community.

This project provides an opportunity to become familiar with community detection using modularity optimisation, and to apply the usual methods in the less mainstream problem of signed networks. The suggested steps of the project are the following, but students deviation from them is allowed, if their creativity or prior knowledge leads to elsewhere.

1. Familiarise with python's [networkx](https://networkx.github.io/) module that can help to handle networks (Other network manipulation tools are also acceptable.). Try to do basic operations on small network and find a way to present them. The use of graphical softwares are recommended e.g. [cytoscape](http://www.cytoscape.org), [plotly](https://plotly.com/), etc...

2. Understand the notion of modularity and find some community detecting methods using it. Try to implement them (or find implemented versions), and experiment with using them on some real networks. Collect your experiences.

3. Though using modularity for finding communities in undirected, unweighted networks is very popular, its generalisation to different directions is not trivial. Based on the knowledge and interpretation gained in the previous tasks, try to modify (or find some modification) the previously tried methods in such way that they can find communities in signed networks i.e. in the case where there are also "negative edges" in the network.
More precisely: In a regular network connection between two nodes expresses the desire of being in the same community. But what if there are another type of connection that expresses the desire of being in separate communities? How can modularity be used in such a network?

Recommended literature:
* [GN's original paper](https://arxiv.org/pdf/cond-mat/0308217.pdf)
* [About modularity](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=4358966&casa_token=ZxWx_aeng2oAAAAA:akUu0zzTw4JfudtAxmZvuTsuQvk2BcTos0vIHhCa4MSHaKHA2rs0UECD1aib0bXrphTWML2-9eGOzg&tag=1)
* Some other

Regular networks to experiment with:
* Karate club
* Football
* Trade nodes from EU4
* Rosenfeld crime
* Others?

Signed networks to experiment with:
* Alliance and rivalry relation from EU4
* Others?

Network repositories:
* [The Colorado Index of Complex Networks (ICON)](https://icon.colorado.edu/#!/)
* [brain, OpenConnectome](http://openconnecto.me/graph-services/download/)
* [movies, Netflix](http://academictorrents.com/details/9b13183dc4d60676b773c9e2cd6de5e5542cee9a)
* [Internet, DIMES](http://www.netdimes.org/new/)
* [Genomics, co-expression](https://en.wikipedia.org/wiki/Gene_co-expression_network) and [GEO](http://www.ncbi.nlm.nih.gov/geo/)
* [SNAP collection of networks](https://snap.stanford.edu/data/)


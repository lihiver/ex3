# ex 3 – Data collection & Network Analysis #
### Lihi Verchik - 308089333 , Aviram Adiri - 302991468
---

## Question 1:

First of all, we will load the relevnt packages and data:

```{r}
setwd("C:/Personal/dataWorkshop/ex3/ex3/ex3")
library(igraph)

ga_edgelist <- read.csv("sources/ga_edgelist.csv")

ga_graph <- graph.data.frame(ga_edgelist, directed = F)
V(ga_graph)$size = degree(ga_graph) * 2
plot(ga_graph)
```
We got a graph with the relationships of the characters in Gray Anatomi:

![image](/images/ga_graph.png)

### part a:

#### i. Betweeness

```{r}
betweenness = betweenness(ga_graph)
max_betweenness <- as.numeric(which(max(betweenness) == betweenness))
betweenness
V(ga_graph)[max_betweenness]
```

![image](/images/ga_betweenness.PNG)

Answer: sloan

#### ii. Closeness

```{r}
closeness = closeness(ga_graph)
max_closeness <- as.numeric(which(max(closeness) == closeness))
closeness
V(ga_graph)[max_closeness]
```

![image](/images/ga_closeness.PNG)

Answer: torres

#### iii. Eigencetor

```{r}
evcent <- evcent(ga_graph)$vector
evcent
max_evcent <- as.numeric(which(max(evcent) == evcent))
V(ga_graph)[max_evcent]
```

![image](/images/ga_evcent.PNG)

Answer: karev

### part b:

### Algorithm fastGreedy (Clauset-Newman-Moore algorithm)

Deviding the vertexs to communities following the algorithm:

```{r}
fastgreedy_com <- fastgreedy.community(ga_graph)
```

#### i.

Creating a graph:

```{r}
plot(ga_graph, vertex.color=fastgreedy_com$membership)
```

![image](/images/ga_fastgreedy_graph.png)

#### ii.

```{r}
sizes(fastgreedy_com)
```

Answer: there are 6 communities, with the sizes: 10, 5, 4, 5, 5, 3. (see the image above).

![image](/images/ga_fastgreedy_size_modularity.PNG)

#### iii.

```{r}
modularity(fastgreedy_com)
```

Answer: modularity = 0.5774221


### Algorithm "Walktrap"

Deviding the vertexs to communities following the algorithm:

```{r}
walktrap_com <- walktrap.community(ga_graph)
```

#### i.

Creating a graph:

```{r}
plot(ga_graph, vertex.color=walktrap_com$membership)
```

![image](/images/ga_walktrap_graph.png)

#### ii.

```{r}
sizes(walktrap_com)
```

Answer: there are 7 communities, with the sizes: 5, 13, 3, 3, 2, 3, 3. (see the image above).

#### iii.

```{r}
modularity(walktrap_com)
```

Answer: modularity = 0.5147059 (see the image above).

![image](/images/ga_walktrap_size_modularity.PNG)

---

## Question 2:

Again, we will load the relevnt packages and data:

```{r}
# install.packages('Rfacebook')
library('Rfacebook')
```

Note: the token for Facebook API is temporary, so we wrote the data on an attached file, called sources/fb_network.csv.
The next code is for getting the data from Facebook, and we put it in comments since the tolken is probably not abailable anymore.

We used the method "getNetwork" which returns all of our members on Facebook and the relationships between them.
Also, we removed all the "single" members (members that doesn't have any relationship between any other member).

```{r}
fb_token = "EAACEdEose0cBADdzf40ZAJPO3gwSkPor5NBAB7mvAbh56LkvbISyjIj2DExEfZCFtnYSSbY8juZBsZBdoavJEW5zDIPh3ZClKkEZAhx0tfjm84sKonC4iZAyiYyVynuvVyjZBVExH548e0xBOK2kZCN6AgMitZCuyeZAT1UZCDkDU1kDfKkF7iZBaWF5d"

# fb_network <- getNetwork(fb_token, format="adj.matrix")
# singletons <- rowSums(fb_network)==0
# fb_network <- fb_network[!singletons,!singletons]

# write.csv(fb_network, "sources/fb_network.csv")

# fb_graph <- graph.adjacency(fb_network)
# V(fb_graph)$size = degree(fb_graph) * 2
# plot(fb_graph,edge.arrow.size=0)

```

We made a csv file with the data from Facebook, and we load it.

```{r}
fb_network <- read.csv("sources/fb_network.csv")
fb_graph <- graph.data.frame(fb_network, directed = F)
V(fb_graph)$size = degree(fb_graph) * 2
fb_graph <- simplify(fb_graph)
plot(fb_graph)

```

We got a graph with the relationships of our friends on facebook:

![image](/images/fb_graph.png)

each member is a vertex in the graph.
the connections between the members is friendship on Facebook (two members have a connection (edge) iff they are friends on Facebook).

### part a:

#### i. Betweeness

```{r}
fb_betweenness = betweenness(fb_graph)
fb_betweenness
max_fb_betweenness <- as.numeric(which(max(fb_betweenness) == fb_betweenness))
V(fb_graph)[max_fb_betweenness]
```

![image](/images/fb_betweenness.PNG)

Answer: Barak Yaari

#### ii. Closeness

```{r}
fb_closeness = closeness(fb_graph)
fb_closeness
max_fb_closeness <- as.numeric(which(max(fb_closeness) == fb_closeness))
V(fb_graph)[max_fb_closeness]
```

![image](/images/fb_closeness.PNG)

Answer: Barak Yaari

#### iii. Eigencetor

```{r}
fb_evcent <- evcent(fb_graph)$vector
fb_evcent
max_fb_evcent <- as.numeric(which(max(fb_evcent) == fb_evcent))
V(fb_graph)[max_fb_evcent]
```

![image](/images/fb_evcent.PNG)

Answer: Barak Yaari

### part b:

### Algorithm fastGreedy (Clauset-Newman-Moore algorithm)

Deviding the vertexs to communities following the algorithm:

```{r}
fb_fastgreedy_com <- fastgreedy.community(fb_graph)
```

#### i.

Creating a graph:

```{r}
plot(fb_graph, vertex.color=fb_fastgreedy_com$membership, edge.arrow.size=0)
```

![image](/images/fb_fastgreedy_graph.png)

#### ii.

```{r}
sizes(fb_fastgreedy_com)
```

Answer: there are 4 communities, with the sizes: 5, 5, 2, 2. (see the image above).

![image](/images/fb_fastgreedy_size_modularity.PNG)

#### iii.

```{r}
modularity(fastgreedy_com)
```

Answer: modularity = 0.5947232

### Algorithm "Walktrap"

Deviding the vertexs to communities following the algorithm:

```{r}
fb_walktrap_com <- walktrap.community(fb_graph)
```

#### i.

Creating a graph:

```{r}
plot(fb_graph, vertex.color=fb_walktrap_com$membership, edge.arrow.size=0)
```

![image](/images/fb_walktrap_graph.png)

#### ii.

```{r}
sizes(fb_walktrap_com)
```

Answer: there are 4 communities, with the sizes: 2, 8, 2, 2. (see the image above).

![image](/images/fb_walktrap_size_modularity.PNG)

#### iii.

```{r}
modularity(fb_walktrap_com)
```

Answer: modularity = 0.25875 

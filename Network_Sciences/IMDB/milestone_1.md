## Checkpoint 1
### Nick Reeder - Network Generation
### 4/13/2023


## Sumary of week
This week I developped the perliminary test network. Due to the feature film problem in the extraction I only built the code to build the netowork for JJ Abrams; this code was generalized and made into a function but that portion remains untested. The netowork is presently a bipartite network of dircetors and crew. This netowork was written as a .gexf file and sent to rest of group. I also began developlement of a function to add features to each node. Code to build netowrk is posted below. Thus far code has only been devlopped in notebooks, but I plan to soon move it to a .py file

---


### Pre-function development code
```{python}
import json

# Opening JSON file
f = open('dir_data.json')
  
# returns JSON object as 
# a dictionary
data = json.load(f)

data['nm0009190']['Name']
jj_data = data['nm0009190']

list_of_names = []
for movie in jj_data['Movies']:
  for role in jj_data['Movies'][movie]['roles']:
    for person in jj_data['Movies'][movie]['roles'][role]:
      list_of_names.append(jj_data['Movies'][movie]['roles'][role][person]['name'])
      
len(list_of_names) #printed 15985      
len(set(list_of_names)) #printed 12335

from collections import Counter

weights = dict(Counter(list_of_names))
len(weights)
weights["J.J. Abrams"]
del weights['J.J. Abrams']
len(weights)

import networkx as nx
from networkx.algorithms import bipartite

jja_graph = nx.Graph()

#two types of nodes
crew_nodes = list(weights.keys())
jja_graph.add_node(director, bipartite = 0)
jja_graph.add_nodes_from(crew_nodes, bipartite = 1)

#adding edges with weights from dictionary called weights
for name in weights:
  jja_graph.add_edge(director, name, weight = weights[name])
  
from networkx.algorithms.wiener import is_connected
print('num nodes', jja_graph.number_of_nodes()) #12335, this is consitent
print('num edges', jja_graph.number_of_edges()) #12334, this is consitent
is_connected(jja_graph) #printed true, this is consistent
```

### Function version of code above that is generalized to build a netowrk for all directors

```{python}
def build_netorok(file):
  imdb_network = nx.Graph()
  f = open('dir_data.json')
  data = json.load(f)
  for id in data:
    for director in data[id]['Name']:
      break #stopping it from running for now
      list_of_names = [] #list of all crew members, cleared for each director
      for movie in jj_data['Movies']:
        for role in jj_data['Movies'][movie]['roles']:
          for person in jj_data['Movies'][movie]['roles'][role]:
            list_of_names.append(jj_data['Movies'][movie]['roles'][role][person]['name'])
            #filling out list of crew members, containts repears
      weights = dict(Counter(list_of_names)) #creates a dict of crew members, key is name and value is count (weight)
      if director in weights.keys():
        del weights[director] #removes director from dict
    #Data processing complete, building network below
    #################################################
    crew_nodes = list(weights.keys())
    imdb_network.add_node(director, bipartite = 0) #adds the director node
    #I can add features to the director node here, or in a seperate function
    imdb_network.add_nodes_from(crew_nodes, bipartite = 1) #adds all crew nodes
    for name in weights:
      imdb_network.add_edge(director, name, weight = weights[name])

  return(imdb_network)


```
---

### Very early stage label adding code

```{pyton}
label_set = set()
eth_set = set()
sex_set = set()
name_set = set()
for id in data:
  for dir in data[id]:
    name_set.add(data[id]['Name'])
    sex_set.add(data[id]['Sex'])
    eth_set.add(data[id]['Ethnicity_Race'])
    label_set.add(data[id]['Labels'])
```

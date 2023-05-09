## Checkpoint 2
### Nick Reeder - Network Generation
### 4/20/2023


## Summary of prior-progress
Last week I developlmend a perliminary test network for just JJ Abrams and began functionizing the code.

## Sumary of week
This week I made corrections to the perliminary network, adding features to director nodes and made node names the id as opposed to their name. This code has now been fully functionized and collated into a .py file. I also worked with Skylar, the visualization lead, to go over requirments/needs of the network.

## Next Steps 
Working with Mac to get the data for a couple other directors to build a fuller test network, but will need to figure out how to do that on a school computer as I do not think my laptop will have the power to handle too much more data. Will be implementing failure safe features with Try and Except blocks as well as improving perfomance becauce this is currently at least in $O(n^7)$.


---
File is in the GitHub Repo.

Below is the functionized version of the JJA network builder.

```{pyton}
def build_network_jja(file, self_loops = False, only_oscar_roles = False):
  imdb_network = nx.Graph()
  f = open(file)
  data = json.load(f)
  data = data['nm0009190']
  #for id in data:
  imdb_network.add_node('nm0009190', bipartite = 0, sex = data['Sex'], eth = data['Ethnicity_Race'], label = data['Labels'])  
  #for director in data[id]:
  for director in data:
    #break #stopping it from running for now
    list_of_names = [] #list of all crew members, cleared for each director
    for movie in data['Movies']:
      print('Loading data for movie:', movie)
      for role in data['Movies'][movie]['roles']:
        for crew_id in data['Movies'][movie]['roles'][role]:
          list_of_names.append(crew_id)
          #if crew_id not in imdb_network.nodes():
            #imdb_network.add_node(crew_id, bipartite = 1, name = data['Movies'][movie]['roles'][role][crew_id]['name'])
          #filling out list of crew members, containts repeats
    weights = dict(Counter(list_of_names)) #creates a dict of crew members, key is name and value is count (weight)
    for crew_id in weights.keys():
      imdb_network.add_node(crew_id, bipartite = 1)
    for crew_id in weights:
      imdb_network.add_edge('nm0009190', crew_id, weight = weights[crew_id])
  f.close()
  if not self_loops:
    imdb_network.remove_edges_from(nx.selfloop_edges(imdb_network))
  return(imdb_network)
```

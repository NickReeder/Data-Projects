## Checkpoint 3
### Nick Reeder - Network Generation
### 4/27/2023


## Summary of prior-progress
Last week I developed and corrected a perliminary test network for just JJ Abrams and began 'functionizing' the code. Network was redessigned to make node if the name of the node and added name as a feature. 

## Sumary of week
This week I made serious progress. This data came in a different format than the previous data so I reworked my code to work with this, and after this developed what would be nearly the final network. This was developed into a .py file and the network was generated through commmand line calls. I also added a feature where the user can include list of roles to NOT include in the network. I then also improved the time-perfomance of the code from ~$O(n&7)$ to what apears to be $O(n^4)$. This is still not great, but is a major improvement. I also developped a try and except block that ensure that the netowrk is failure tollerant in the case of errors.

## Next Steps 
My next tasks will be working with Skylar and Ani to confirm the accuracy of the network and ensure it has all the features that they will need to develop the visualiztions and analysis. Primarily I expect this to consist of adding a "most common role" to each crew node, potentially adding a "total movies" feature to directors, and reconsidering the weights. How I handle the weights will be as directed by anu and skyler. 


---
py, data, and gexf files in the GitHub Repo.

Below is the network generation function and the main section

```{python}
def add_director(network, dir_id, self_loops = False, do_not_include = []):
  cwd = os.getcwd()
  os.chdir(cwd + '\\' + dir_id)
  cwd = os.getcwd()
  f = open('dir_info.json')
  data = json.load(f)
  network.add_node(dir_id, bipartite = 0, sex = data['Sex'], eth = data['Ethnicity_Race'], label = data['Labels'])
  f.close()
  os.chdir(cwd + '\\movies')
  #print(os.getcwd())
  cwd = os.getcwd()
  movies = os.listdir(cwd)

  list_of_c_ids = [] 
  id_name_dict = {}

  for movie in movies:
    #print(movie)
    f = open(movie)
    data = json.load(f)
    for role in data['roles']:
      if role not in dni: #if role not in list of those not to include, add add crew ids to listp; otherwise skip.
        for crew_id in data['roles'][role]:
          list_of_c_ids.append(crew_id)
          id_name_dict[crew_id]= data['roles'][role][crew_id]['name']
          #print(data['roles'][role][crew_id])
    f.close()
  weights = dict(Counter(list_of_c_ids))
  for crew_id in weights.keys():
    if crew_id not in network.nodes():
      network.add_node(crew_id, bipartite = 1, name = id_name_dict[crew_id])
  for crew_id in weights:
    network.add_edge(dir_id, crew_id, weight = weights[crew_id])

  if not self_loops:
    network.remove_edges_from(nx.selfloop_edges(network))
```

```{python}
if __name__ == '__main__':
  if len(sys.argv) < 2:
    # This means the user did not provide the filename to check.
    # Show the correct usage.
    print('Did not detect folder. Please include folder containing data.')
  else:
    imdb_network = nx.Graph()
    print('File recieved, building netowrk')
    if sys.argv[2] != None:
      dni = sys.argv[2]
      print('Roles chosen not to indlude are:', str(dni))
    else:
      print('All roles will be included')
    path_to_data = sys.argv[1]
    cwd = os.getcwd()
    os.chdir(cwd + '\\' + path_to_data)
    cwd = os.getcwd()
    entries = os.listdir(cwd)[1:]
    for folder in entries:
      try:
        print("Attemping to add director_id:", folder)
        add_director(imdb_network, folder)
        os.chdir(cwd)
        print('Success')
      except:
        print("Failed to add to add director_id:", folder)
    print('Network Built')
    print('num nodes', imdb_network.number_of_nodes())
    print('num edges', imdb_network.number_of_edges())
    print(is_connected(imdb_network))

    print('Writing gexf file')
    os.chdir('C:\\Users\\Nick\\desktop\\Network_Sciences')
    cwd = os.getcwd()
    print(cwd)
    nx.write_gexf(imdb_network, cwd + '\\Network_v1.gexf')

```

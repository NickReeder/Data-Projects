# Data-Projects
A small repository for some personal interest projects regarding data science



- IMDB Director Network
  - Scraped data from IMDB to build a bipartite newtwork of directors and crew members. Edges are created when a crew member worked for a director. Only data from feature length films was extracted.
  - Weights for edges were calculated with the below formula. Each edge additionally has a feature for the primary role of that crew-director pair.
    - $\text{weight} = \frac{\text{number of this crew members has worked for this director in their primary role for this director}}{\text{number of times this director has employed this role}}$
  - Each director node has the following features
    - 
  - Each crew node has the following features
    - Name
  - 
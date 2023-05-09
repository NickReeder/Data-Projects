## Checkpoint 4
### Nick Reeder - Network Generation
### 5/4/2023


## Summary of prior-progress
Last week I built the complete network on the full data set and began bug fixing and problem solving with this. Much of this process was spent talking to Ani and Skyler to see what their needs were for any additional functionality.

## Sumary of week
This week I made some bug fixes and made two major feature additions. First I adjusted the weighting calculations to be $\text{weight} = \frac{\text{number of this crew members has worked for this director in their primary role for this director}}{\text{number of times this director has employed this role}}$. To explain this formula more, each crew member is assigned a primary role (their most worked role) PER director. This is counted and then dived by the number of times that director has emplyed this specific crew role. This normalizes the weights to give the proportional relationship based on role counts and movies. This approach also prevents relationships being hidden if crew members had a different primary role for different directors. It is reasonable to assume that crew members progess to higher roles and may work for different directors in those higher up roles. 

The second feature is a returned csv file from a data farme that contains iterative statistics of the netowork. The tbale is indexed by the number of directors added to the network and has at each index the number of nodes, number of edges, density, and average shortest path length.

## Next Steps 
Next I plan to do a performance analysis and hopefully reduce the time complexity. I will of course also continue to work with my other team members to bug fix and add any features that we need. 

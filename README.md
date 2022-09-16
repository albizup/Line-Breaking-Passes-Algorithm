# Line Breaking Passes at Euro 2020


Understanding teams’ abilities, flaws and tendencies in the build-up phase can be crucial for several aspects. 
For instance, learning which players are usually more involved in the first stage of the action can be useful both for opposition analysis, since we may want to limit the opponent’s playmakers, or for scouting,  e.g., we may need to replace our creative midfielder and we need to find a similar player.

One key aspect, which in football analytics was often overlooked for the lack of tools (tracking data) and not for the lack of importance, is the ability of player or a team to find teammates behind the enemy lines,  i.e., the ability to make passes that dissect a line of the opponent’s formation. 

The aim of this article is therefore to briefly discuss an algorithm that individuates line breaking passes with the use of the StatsBomb360 data, which allow to have the positions of a subset of defenders, and to present tendencies relative to this aspect at Euro2020. 

## Line Breaking Pass Algorithm 

 We consider a pass a line breaking pass if:

1) The pass is successful, i.e., it reaches a teammate; 

2) Progress the ball forward at least 10 meters; 

3) It breaks at least one defensive line, which is defined as  a “vertical line” between two defenders that are at most 8 m apart. Note that it may break more than one line, but we are interested only if it breaks at least one. 


![image](https://user-images.githubusercontent.com/92165441/190650829-42c339e4-1545-4c13-bd13-2b311e8d965b.png)
![image](https://user-images.githubusercontent.com/92165441/190650862-e4e6e676-4ccc-43a0-afe5-4533ae09fb0f.png)


### Scheme of the algorithm

- The positions of the defenders, which may be less than 11 in the visible area, is taken by considering the SB360 frame corresponding to the start of the pass (we freeze the defenders at that time). 

- We exclude the goalkeeper from the set of defenders.

- The defensive lines are identified with a 1-D clustering Fisher-Jenks algorithm and by ordering along the y-direction. The number of clusters is set between (0,3) depending on the number of defenders in the frames. 

- We compute if the segment line of the pass intersects with one defensive line. 

*Time of execution for 51 games: approx. 10 minutes!*

**Inspired by:** 
- https://www.statsperform.com/resource/how-impactful-are-line-breaking-passes
- https://statsbomb.com/articles/soccer/statsbomb-360-exploring-line-breaking-passes//

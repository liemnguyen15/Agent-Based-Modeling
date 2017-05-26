# Agent-Based-Modeling
An agent-based model that re-creates a social environment in which agents (humans) are given higher levels of "confidence", which lead to a higher rate of interaction/"dating" among all agents.

In the paper “Human Mate Choice is a Complex System”, authors Paul E. Smaldino and Jeffrey C. Schank face the problem of understanding the dynamics of human mate choice and its sociocognitive mechanisms. The evidence for this problem exists in previous agent based models (ABMs), which do highlight the possible mechanisms of human mate choice, but do not consider location as a factor in either physical or social space. So, the authors developed an agent-based simulation to conduct their experiments. Each agent has one trait that measures his or her attractiveness to a potential mate on numerical scale. The agent searches its local neighborhood (dateSearchRadius) for an agent that is available for a “date”, and if both agents match in attractiveness, the two mate and are removed from the dating pool. Each agent also has one trait that measures his or her initial willingness to accept dates with other agents (exponentN). Also, each agent has a certain probability of matching another agent, and that probability increases as the number of unsuccessful dates for that one agent increases. After a certain maximum number of unsuccessful dates (maxD), the agent will eventually have a successful date and match another agent. This agent-based simulation also includes decision rules for choosing another agent for a “date”. The two decision rules are to choose the most attractive or most similar agent for a date.

Although this model yielded reasonable results about how agents interact with each other in a dating pool, we wanted to further develop this model to yield even better results. To do so, we added level of confidence, a personality trait that reflects an agent’s confidence to look for, date, and match other agents.

To properly incorporate level of confidence, we defined an agent’s level of confidence based on 3 other traits: 
•	An agent’s initial willingness to accept dates with other agents (exponentN)
•	The maximum number of dates until an agent matches another agent (maxD)
•	An agent’s search radius or local neighborhood (dateSearchRadius)

As an agent’s level of confidence increases, an agent becomes more willing to accept dates with other agents (increase in exponentN), more willing to go on more dates until matching an agent (increase in maxD), and more willing to move around more to find dates (increase in dateSearchRadius). As an agent’s level of confidence decreases, an agent becomes less willing to accept dates with other agents (decrease in exponentN), less willing to go on more dates until matching an agent (decrease in maxD), and less willing to move around more to find dates (decrease in dateSearchRadius).

To better scale level of confidence, we ranked an agent’s level of confidence on a scale from 1-5:
•	1 is least confident (very shy), 
•	2 is less confident (shy)
•	3 is neutral (neither bold nor shy)
•	4 is more confident (bold)
•	5 is most confident (very bold) 
We set the standard level of confidence to be equal to 3. 

To properly incorporate our definition of level of confidence, we had to redefine the three other traits mentioned above.

We redefined an agent’s willingness to look for a “date” (exponentN) as:
this.exponentN = e.exponentN * (e.levelOfConfidence/3.0);
		
We redefined an agent’s maximum number of dates until matching an agent (maxD) as:
this.maxD = e.maxD * (e.levelOfConfidence/3.0);
		
We redefined an agent’s search radius or local neighborhood (dateSearchRadius) as:
this.dateSearchRadius = (int)e.levelOfConfidence;

Based on our redefinitions, this is what we can infer. When an agent has a high level of confidence (4.0 or 5.0), that agent is labeled as “bold”, and his or her values for exponentN, maxD, and dateSearchRadius will all increase. When an agent has a low level of confidence (1.0 or 2.0), that agent is labeled as “shy”, and his or her values for exponentN, maxD, and dateSearchRadius will all decrease. When an agent has a neutral level of confidence (3.0), that agent is labeled as “neither bold nor shy”, and his or her values for exponentN, maxD, and dateSearchRadius will not change. From here, we can come up with a hypothesis:

The higher the confidence, the higher the correlation of matches among all agents.

In order to prove our hypothesis, we decided to test the code after making the necessary modifications to the original Mate Choice model. To start, we ran 3 virtual experiments, with each virtual experiment testing the influence that level of confidence has on each of the 3 other traits, individually. To end, we ran a fourth and final virtual experiment, which detailed the influence level of confidence has on all 3 traits, collectively.

For virtual experiment #1, we decided to test level of confidence in relation to the agent’s dateSearchRadius. We did not redefine an agent’s exponentN nor MaxD, and only redefined an agent’s search radius or local neighborhood (dateSearchRadius) as:
this.dateSearchRadius = (int)e.levelOfConfidence;



Figure 1a.					      Figure 1b.

Based on our results, we determine that as an agent becomes more willing to move around more to find dates (dateSearchRadius increases), there is no consistent increase nor decrease in correlation of matches among all agents when agents are applying the “best similar” and “most attractive” rule. It appears that if all agents in the dating pool are more willing to move around, there is lack of fluctuation in correlation among these agents. This means more factors must be evaluated together with an agent’s search radius.

For virtual experiment #2, we decided to test level of confidence in relation to the agent’s maxD. We did not redefine an agent’s exponentN nor dateSearchRadius, and only redefined an agent’s maximum number of dates until he or she matches another agent (maxD) as:
this.maxD = e.maxD * (e.levelOfConfidence/3.0);



Figure 2a.					      Figure 2b.

Based on our results, we determine that as an agent becomes more willing to go on dates until finding an agent to match with (maxD increases), there is no consistent increase nor decrease in correlation of matches among all agents when agents are applying the “most attractive” rule, but there is a small, consistent increase in correlation of matches among all agents when agents are applying the “best similar” rule. It appears that as all agents are looking for the “most similar” agents in the dating pool and are more willing to go on more dates until finding a match, they have an element of similarity they share with one another, which causes the slight increase in correlation as more agents find other agents with the same level of encouragement to go on dates. On the other hand, if all agents are looking for the “most attractive” agents in the dating pool, the agents’ willingness to go on dates does not change correlation. This means more factors must be evaluated together with an agent’s maximum number of dates until finding a match.

For virtual experiment #3, we decided to test level of confidence in relation to the agent’s exponentN. We did not redefine an agent’s maxD nor dateSearchRadius, and only redefined an agent’s initial willingness to accept dates with other agents (exponentN) as:
this.exponentN = e.exponentN * (e.levelOfConfidence/3.0);




Figure 3a.					      Figure 3b.

Based on our results, we determine that as an agent becomes more initially willing to accept dates with other agents (exponentN increases), there is a consistent increase in correlation of matches among all agents when applying both the “best similar” and “most attractive” rule. It appears that if all agents are looking for the “best similar” agents in the dating pool and are more willing to accept dates, they have an element of similarity they share with one another, which causes an increase in correlation as more agents find other agents with the same level of willingness to initially accept dates. It also appears that if all agents in the dating pool are looking for the “most attractive” agents in the dating pool and are more willing to accept dates, agents whose attractiveness are different are more open to accepting dates with each other, and so causes the increase in correlation. 

Because we are making the same type of changes to every agent in the dating pool, the “best similar” rule plays a larger part in correlation among agents that are matching than the “most attractive” rule, which is why the correlation values in Figure 1a, 2a, and 3a are much larger than those in Figure 1b, 2b, and 3b, respectively.

Now that we have conducted our first threevirtual experiments, we will now combine level of confidence’s influence on all 3 traits in a fourth and final virtual experiment.

For virtual experiment #4, we decided to test level of confidence in relation to the agent’s exponentN, maxD, and dateSearchRadius. We redefined these 3 traits as follows: 
this.exponentN = e.exponentN * (e.levelOfConfidence/3.0);
this.maxD = e.maxD * (e.levelOfConfidence/3.0);
this.dateSearchRadius = (int)e.levelOfConfidence;



Figure 4a.					    Figure 4b.

Based on our final results, we determine that as an agent becomes:
•	more willing to move around more to find dates (dateSearchRadius increases)
•	more encouraged to go on dates until finding an agent to match with (maxD increases)
•	more initial willing to accept dates with other agents (exponentN increases)
all of which are a result of an increase in an agent’s level of confidence, there is a consistent increase in correlation of matches among all agents when applying both the “best similar” and “most attractive” rule. 

There is also a higher correlation when all agents are looking for the “best similar” agents rather than the “most attractive” agents in the dating pool. Our rationality is simple. Under the “best similar” rule, when we increase the level of confidence among all agents in the dating pool, we also increase the similarity among all agents in the dating pool. So, when an agent is looking for another agent, he or she will encounter more agents that are similar, and thus more matches among agents is inevitable. But under the “most attractive” rule, when we increase the level of confidence among all agents in the dating pool, we don’t increase the level of attractiveness among all agents in the dating pool. When an agent is looking for another agent, rather than dating other agents based on similarity, he or she will be more likely to date other agents despite their differences in attractiveness. So, the increase in correlation as confidence increases is justified, but is not as large of an increase as it is under the “best similar” rule than under the “most attractive” rule.

Our initial hypothesis was that: The higher the confidence, the higher the correlation of matches among all agents. Based on our virtual experiments and results, we have confirmed our hypothesis. As the dating pool of agents all increase in level of confidence, there is a corresponding increase in matches among all the agents. 

This draws excitingly eerie parallels to real-life social phenomenon, that as a population of humans become overall more confident in interacting and dating, there will be an increase in number of humans who will interact and date.

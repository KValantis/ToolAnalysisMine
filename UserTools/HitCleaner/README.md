# HitCleaner

The `HitCleaner` tool cleans up events by selecting only digits that are above a certain threshold, have a certain number of neighbouring hits or are clustered with other digits.

## Input

`HitCleaner` uses `RecoDigit` objects that have been generated by the `DigitBuilder` tool.

**RecoDigit** `vector<RecoDigit>`
* Loops over the digits and checks whether digits fulfill certain conditions (space/time/pulse threshold).

## Output

`HitCleaner` returns the input vector of `RecoDigit` objects, but with an adjusted `isFiltered` status flag. Those digits that passed the cuts have a `isFiltered` flag of 1, while the ones that did not pass the cut have a flag of 0.

**RecoDigit** `vector<RecoDigit*>*`
* Collection of `RecoDigits` with their filter status flag set.

The tool furthermore stores the hit cleaning parameters in the `RecoEvent` store:

**HitCleaningParameters** `map<string,double>`
* Map containing the Hit Cleaning parameters

It also stores the information about found hit cleaning clusters:

**HitCleaningClusters** `vector<RecoCluster>`
* The found clusters are stored in the form of a vector.

## Configuration

HitCleaner can be configured in the following way:

```
verbosity 2
Config 3               	#config type: 1 = pulse height cut, 2 = neighbour cut, 3 = cluster cut								
PmtMinPulseHeight 30    	#minimum pulse height
PmtNeighbourRadius 60  	#digit neighbouring distance [cm]
PmtMinNeighbourDigits 2	#minimum neighbour digits
PmtClusterRadius 80 	#digit clustering distance [cm]      
PmtTimeWindowN 50	#neighbouring time window [ns]    
PmtTimeWindowC 50 	#clustering time window [ns]           
PmtMinHitsPerCluster 4	#number of hits per cluster								                         
LappdMinPulseHeight 0	#minimum pulse height                             
LappdNeighbourRadius 25 #digit neighbouring distance [cm]              
LappdMinNeighbourDigits 20 #minimum neighbour digits                      
LappdClusterRadius 25   #digit clustering distance [cm]                                    
LappdTimeWindowN 0.6    #neighbouring time window [ns]                 
LappdTimeWindowC 1      #clustering time window [ns]                   
LappdMinHitsPerCluster 20 #number of digits per cluster	
MinClusterDigits 10	#minimum clustered digits							  
IsMC 0			#Data or MC?
SinglePEGains ./configfiles/EventDisplay/Data-ANNIEEvent/ChannelSPEGains_BeamRun20192020.csv
```
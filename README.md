# Exp_robotics_lab Assignment1
## INTROCUCTION
Purpose of this repository is to develop the assignment 1 of Experimental Robotics Laboratory. The assignment is about developing the simulation of the cluedo game in the ros environment. Cluedo is a board game, the objective of the game is to determine who murdered the game's victim, where the crime took place, and which weapon was used(more details on https://en.wikipedia.org/wiki/Cluedo). In this simulation robot moves between the rooms as in a cluedo game to look for the hints and once it find the hints it goes back to the oracle room to check the solution. If the solution is correct the game ends or the robot look for more hints by moving around the rooms. At first the solution is generated, then the robot moves randomly between places and finds the hints. Then it checks for the consistency with the Armor service, once the generated is conistent. It checks for the correct solution. Games ends based when the solution is correct.

## SOFTWARE ARCHITECTURE
In order to better understand the software architecture we can utilise the UML component diagram

UML COMPONENT DIAGRAM
![CLUDO_FSM](https://user-images.githubusercontent.com/82164428/219979474-29c5449c-e85b-4ddb-817e-4d44d3e8b080.jpg)

Finite state machine node is the main node of the architecure, with which each and every node communicates. It simulates the scene of the cluedo gmae. At first orcale node genreates the solution when the game starts. 

Finite state machine node ask the go to point node to simulate the movement of the robot from point to point. It sends the co ordinates to the go to point to simulate the movibg action.

It ask the hints with the oracle node. Oracel node provide the hint (what[], where[], who[]) with the ID. It also ask the oracle node for solution check. Oracle send back the true or false for the solution check.

It communicates with the myArmor class to effectively communicate with the armor service. myArmor class communicates with the armor service and sends the response from armor service back to the state machine node. It perfoems all the armor functions. 

It communicates with the place class to generate the place object with co ordinates of the place and its name. 

Lets dive into the details of the software architecture of the ros workspace:
The workspace consist of the scripts , launch and srv directories & cluedo ontology file. Scripts directory contains all the scripts and class to execure the architecture. Launch folder contain the launch file to execute all the nodes to simulate the game. srv folder has all the service messages. 

### SCRIPTS:

### STATE_MACHINE.PY: 
This node stimulate the three sates of the robot. The three states are move state, enter the room state and the solution check state. 
  
 1)MOVE: In the first state the robot starts from the oracle room and start to explore rooms in order to acquire hints. The Move custom service message is send to the go_to_point node in order to simulate the movement of the robot. And it is followed by any one of the following state.
 2)ENTER_ROOM: The robot enters the room and ask the hint with the AskHint custom message to oracle node, oracle node provides the hint with the ID. Then it add the hints to the ontology by MYArmor class and checks for the consistency. If it is consistent, it goes to the oracle room to check the solution.
 3)SOLUTION: This is the state which the robot try to check the solution with the Solution custom message to the oracle node. Based on the solution i.e whether it is true or false it ask to end of game solution or goes back to move node.
 
 ### ORACLE.PY
 ORACLE is the simulator of the oracle room of the game. It generates the solution at first. Whenver the hint is requested it genrates the random hints. Hints are always random with the place, person and weapon and it is generated with the hint ID. Hints are too random sometimes inconsistent and incomplete hints are generated. It also checks for solution correctness when requested by the state machine node.
 
 ### go_to_point.py:
 This is a node simulate the movement of the robot. It generates wait time when the state machine request for the movement simulation. It calculates the euclidean diestance between the point one to another and wait for the time to reach the distance. And sends the complete signal to state machine.
 
 
            


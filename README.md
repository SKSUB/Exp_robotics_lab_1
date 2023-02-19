# Exp_robotics_lab Assignment1
## INTROCUCTION
Purpose of this repository is to develop the assignment 1 of Experimental Robotics Laboratory. The assignment is about developing the simulation of the cluedo game in the ros environment. Cluedo is a board game, the objective of the game is to determine who murdered the game's victim, where the crime took place, and which weapon was used(more details on https://en.wikipedia.org/wiki/Cluedo). In this simulation robot moves between the rooms as in a cluedo game to look for the hints and once it find the hints it goes back to the oracle room to check the solution. If the solution is correct the game ends or the robot look for more hints by moving around the rooms. At first the solution is generated, then the robot moves randomly between places and finds the hints. Then it checks for the consistency with the Armor service, once the generated is conistent. It checks for the correct solution. Games ends based when the solution is correct.

## SOFTWARE ARCHITECTURE
In order to better understand the software architecture we can utilise the UML component diagram

UML COMPONENT DIAGRAM
![CLUDO_FSM](https://user-images.githubusercontent.com/82164428/219979474-29c5449c-e85b-4ddb-817e-4d44d3e8b080.jpg)


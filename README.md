# CPN
Code for 'Composability verficiation of complex systems using colored petri nets'

**4.** **Case Study: Composability Verification of an Elevator Model**

In this section, we provide the details of the case study of an elevator model. We assume the elevator which servers 6 floors. For the sake of simplicity and reduced space, we initialize each floor with 3-4 passengers (though the actual model is capable of taking a large number of incoming passengers). The following steps demonstrate the composability verification process of the elevator model.

**4.1** **Requirement Specification**

We define RS = 〈**O1, S1〉** where

 Objective **O1** **= {**All the arrived passengers must reach their destination floor**}**

Constraint **S1** **= {**The door should never be opened when the elevator is moving**}**

**4.2** **Model Components**

The four basic components developed for the construction of an elevator model are briefly described next.

**4.2.1 Panel**

It is the button panel that is installed on each floor outside the elevator door. When the passengers arrive, they press the panel buttons to call the elevator at their current floor. It takes the passenger tokens as input in their respective floors, processes them in a FIFO queue, constructs a list of trips and passes on the passenger tokens to the output (see Figure 1). 

![PanelComponent](https://user-images.githubusercontent.com/86586703/123754287-288e1a80-d8d4-11eb-9d67-8c1b734a8f13.JPG)

**4.2.2  Door**

The door opens and closes on arriving at each floor and allows the passengers to enter the cabin according to the capacity. The place *‘current floor’* represents the current floor. The place ‘*Load*’ represents the current load in the cabin. Only those passengers can enter which are at the current floor. The door closes when there are no more passengers or the maximum capacity has been reached. Figure 2 illustrates the door component. 

![DoorComponent](https://user-images.githubusercontent.com/86586703/123754352-393e9080-d8d4-11eb-81a8-6cc27e0de67a.JPG)

**4.2.3  Cabin**

It is the carriage for a maximum of 10 passengers. When the passengers enter the cabin they wait until their desired floor has arrived. When the passengers enter the cabin, their desired floor is selected and a list of trips is created after removing the duplicates. The passengers wait until the elevator arrives at their desired destination. Figure 3 illustrates Cabin component. 

![CabinComponent](https://user-images.githubusercontent.com/86586703/123754403-478cac80-d8d4-11eb-9679-a02a00c1f405.JPG)

**4.2.4  Motor**

It takes a list of trips as input from the cabin (the internal button panel selection for the desired floor) or from the floors (outer panel) and moves the motor right to go upwards or left to go downwards. Motor has brakes, which are applied when the desired floor is reached. This component is responsible to change the ‘*current floor*’. Figure 4 illustrates Motor component. 

![MotorComponent](https://user-images.githubusercontent.com/86586703/123754462-5a06e600-d8d4-11eb-81ef-c36e5c2a5c15.JPG)

**4.3 Model composition**

All the components are composed together to form an elevator model as shown in Figure 5:

![Composed Model](https://user-images.githubusercontent.com/86586703/123754891-c84ba880-d8d4-11eb-9c22-dee2b6ab0db2.JPG)

**4.4  Model Execution**

Figure 6 illustrates the initial state and the final state of the model execution. The tokens in the initial state represent passengers as a tuple: **{Passenger ID, Current Floor, Desired Floor}**. Note that in the final state, all the passengers reach their desired floor. 

![Initial State](https://user-images.githubusercontent.com/86586703/123755660-938c2100-d8d5-11eb-9062-00f7fe5ccb52.JPG)

![Final State](https://user-images.githubusercontent.com/86586703/123755684-98e96b80-d8d5-11eb-8b2c-1d64b13e4a53.JPG)

**4.5 Composability Verification**

In this step we perform the state-space analysis. After generating the state-space of the composed model, we visualize it in Gephi tool as shown in Figure 7. In the state-space, Node 1 is the initial node and Node 223 is the goal state. The shortest path to reach the goal state is shown in red color. We develop and perform the query functions, shown in Figure 8 to prove that the goal state is reachable and the constraint will never be reached. The goal is to ensure that all the passengers arrive at their desired floors, so we check that there exists a marking that satisfies this criteria. The constraint is to ensure that the door will never be opened when the elevator is moving. We prove that if there are tokens in ‘*Entered*’ place of any floor, meaning the door is opened, then the ‘*RotatingLeft*’ or ‘*RotatingRight*’ place is empty and vice versa. The satisfaction of goals and constraints assert that all the components are consistent and their behavioral composability is verified as per the given requirement specification. 

![State-Space](https://user-images.githubusercontent.com/86586703/123756999-f3cf9280-d8d6-11eb-8ce1-97a257d22b8a.JPG)

![GoalState](https://user-images.githubusercontent.com/86586703/123757188-25e0f480-d8d7-11eb-92a5-c19c42b3ecae.JPG)

**4.6  Reusability of Model Components**

We create another scenario of the Elevator Model where two elevators are used to show the reuse of model components. Figure 9 shows the initial step of the simulation after reuse and Figure 10 show the final step. 

![Model_Reuse](https://user-images.githubusercontent.com/86586703/123757646-a0aa0f80-d8d7-11eb-8dd9-99b1880831f1.JPG)

![Model_Reuse2](https://user-images.githubusercontent.com/86586703/123757663-a56ec380-d8d7-11eb-9378-b941fd5f72fe.JPG)

The reuse of the elevator component renders the same results however improves the overall efficiency of the system as the passengers randomly select either elevator and reach their final destination in lesser time. When we apply our composability verification process the goal state is reached and the safety property is satisfied. Thus, we can say that a verified composed model satisfies its requirement specification and that successful composability verification is an important characteristic of model reuse. 


**CPN Tools Installation Process**
1. To install CPN Tools for Windows, download and run the file cpntools_setup.exe
2. After successfully installation, ypu need to open the CPN file. Double click on the file, it will open in CPN tools.
3. Once the file will be open, you need to drag the simulation tools from the index to the workspace.

![SimulationsTool](https://user-images.githubusercontent.com/86586703/123760713-8de50a00-d8da-11eb-82d9-8b2b08480123.JPG)

4. We can also define the specific number of steps by applying play tool cell.

![play](https://user-images.githubusercontent.com/86586703/123761268-15cb1400-d8db-11eb-889d-5921f9162568.JPG)

5. It is also possible to execute the simulation step by step or  apply one of the simulation tools from the transition marking menu to an enabled transition..

![trans](https://user-images.githubusercontent.com/86586703/123761418-3dba7780-d8db-11eb-86de-608ff81e006b.JPG)



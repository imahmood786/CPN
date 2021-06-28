# CPN
Code for 'Composability verficiation of complex systems using colored petri nets'

**4.** **Case Study: Composability Verification of an Elevator Model**

In this section, we provide the details of the case study of an elevator model. We assume the elevator which servers 6 floors. For the sake of simplicity and reduced space, we initialize each floor with 3-4 passengers (though the actual model is capable of taking a large number of incoming passengers). The following steps demonstrate the composability verification process of the elevator model.

**4.1** **Requirement Specification**

We define RS = 〈**O1, S1〉** where

 Objective **O1** **= {**All the arrived passengers must reach their destination floor**}**

Constraint **S1** **= {**The door should never be opened when the elevator is moving**}**

**4.2** **Model Components****

The four basic components developed for the construction of an elevator model are briefly described next.

**4.2.1** **Panel:** It is the button panel that is installed on each floor outside the elevator door. When the passengers arrive, they press the panel buttons to call the elevator at their current floor. It takes the passenger tokens as input in their respective floors, processes them in a FIFO queue, constructs a list of trips and passes on the passenger tokens to the output (see Figure 2). 
![PanelComponent](https://user-images.githubusercontent.com/86586703/123599378-f797e200-d80e-11eb-8b4d-d61a5876e0ba.JPG)

**4.2.2  Door**

The door opens and closes on arriving at each floor and allows the passengers to enter the cabin according to the capacity. The place *‘current floor’* represents the current floor. The place ‘*Load*’ represents the current load in the cabin. Only those passengers can enter which are at the current floor. The door closes when there are no more passengers or the maximum capacity has been reached. Figure 3 illustrates the door component. 

![DoorComponent](https://user-images.githubusercontent.com/86586703/123599889-8c024480-d80f-11eb-8530-339fbdfef66a.JPG)

**4.2.3  Cabin**

It is the carriage for a maximum of 10 passengers. When the passengers enter the cabin they wait until their desired floor has arrived. When the passengers enter the cabin, their desired floor is selected and a list of trips is created after removing the duplicates. The passengers wait until the elevator arrives at their desired destination. Figure 4 illustrates Cabin component. 

![CabinComponent](https://user-images.githubusercontent.com/86586703/123599581-30d05200-d80f-11eb-9e73-18a2c4e20aeb.JPG)

**4.2.4  Motor**

It takes a list of trips as input from the cabin (the internal button panel selection for the desired floor) or from the floors (outer panel) and moves the motor right to go upwards or left to go downwards. Motor has brakes, which are applied when the desired floor is reached. This component is responsible to change the ‘*current floor***’.** Figure 5 illustrates Motor component. 

![MotorComponent](https://user-images.githubusercontent.com/86586703/123599945-99b7ca00-d80f-11eb-8693-02078083346c.JPG)

**4.3 Model composition**

All the components are composed together to form an elevator model as shown in Figure 6:

![Composed Model](https://user-images.githubusercontent.com/86586703/123600184-db487500-d80f-11eb-9aba-0f4d946ed0e4.JPG)

**4.4  Model Execution**

Figure 7 illustrates the initial state and the final state of the model execution. The tokens in the initial state represent passengers as a tuple: **{Passenger ID, Current Floor, Desired Floor}**. Note that in the final state, all the passengers reach their desired floor. 

![Initial State](https://user-images.githubusercontent.com/86586703/123600305-fadf9d80-d80f-11eb-89cd-106e4017ffc9.JPG)

![Final State](https://user-images.githubusercontent.com/86586703/123600324-ff0bbb00-d80f-11eb-88d8-6d22d840ec90.JPG)

**4.5 Composability Verification**

In this step we perform the state-space analysis. After generating the state-space of the composed model, we visualize it in Gephi tool as shown in Figure 8. In the state-space, Node 1 is the initial node and Node 223 is the goal state. The shortest path to reach the goal state is shown in red color. We develop and perform the query functions, shown in Figure 9 to prove that the goal state is reachable and the constraint will never be reached. The goal is to ensure that all the passengers arrive at their desired floors, so we check that there exists a marking that satisfies this criteria. The constraint is to ensure that the door will never be opened when the elevator is moving. We prove that if there are tokens in ‘*Entered*’ place of any floor, meaning the door is opened, then the ‘*RotatingLeft*’ or ‘*RotatingRight*’ place is empty and vice versa. The satisfaction of goals and constraints assert that all the components are consistent and their behavioral composability is verified as per the given requirement specification. 

![State-Space](https://user-images.githubusercontent.com/86586703/123600446-1c408980-d810-11eb-936b-8b7a0f3c6429.JPG)

![GoalState](https://user-images.githubusercontent.com/86586703/123600501-2c586900-d810-11eb-9f3a-bb8ef9e26696.JPG)

**4.6  Reusability of Model Components**

We create another scenario of the Elevator Model where two elevators are used to show the reuse of model components. Figure 10 shows the initial step of the simulation after reuse and Figure 11 show the final step. 

![Model_Reuse](https://user-images.githubusercontent.com/86586703/123600655-501baf00-d810-11eb-8c67-d1a4e4de6c1d.JPG)

![Model_Reuse2](https://user-images.githubusercontent.com/86586703/123600669-5578f980-d810-11eb-993b-bfc5fbc6214f.JPG)

The reuse of the elevator component renders the same results however improves the overall efficiency of the system as the passengers randomly select either elevator and reach their final destination in lesser time. When we apply our composability verification process the goal state is reached and the safety property is satisfied. Thus, we can say that a verified composed model satisfies its requirement specification and that successful composability verification is an important characteristic of model reuse. 

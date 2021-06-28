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

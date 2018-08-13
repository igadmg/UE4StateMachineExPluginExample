## State Machine Blueprint library.

Implementation of a state machine inside blueprint editor. Was searching for the best form of state machine presentation in blueprints and created my own state machine implementation for Unreal Engine 4.

![alt text](./Documentation/25baa4391e8a40fd8fe72e82ebd20025.png)

## States

States are implemented by subclassing State class. So every state is represented by a separate blueprint, states can be easely reused in different state machines (if they are not dependent on specific state machine type, by default they are not), any state machine can have as amny instances of any state as you want, but I am not sure it is useful in any case.

![alt text](./Documentation/6521739cca12299ab3fda8dd6824da44.png)

Create requred states by subclassing State class. Every state incapsulate it's logic inside a blueprint class (but also states can be implemented purely in C++). Every state have **Enter**, **Tick** and **Exit** functions. These are executed when state is entered, updated and left.

![alt text](./Documentation/0993c61994e0c252b2ef42cca48279e1.png)

Any state can have variables exposed by setting **Expose on Spawn** flag, their corresponding nodes can be wired to set their values before state is entered.

![alt text](./Documentation/70ba9a862d9f0e2521e3c1e6627ec360.png)

## State transitions

Transitions are represented with blueprint's **Event Dispatchers**.

![alt text](./Documentation/d25e2ab4c0f2e245a7bbf8904db67ae3.png)

Every event dispatcher is generation execution output node on a state, which can be connected to another state, or to some blueprint logic. Dispatcher events can have their own parameters, which are exposed by state bluperint node.

![alt text](./Documentation/e8de95722b055efab22c82344c0c1cae.png)

From inside a state you can initiate a transition by simply calling event dispatcher.

![alt text](./Documentation/d0a032fcb194590a83f6ac8740ead3d6.png)

## State Machine

To run all the sates you should have some Sate Machine object. Any blueprint can be converted into sate machine by adding a **StateMachine** variable (naming is important) of type StateMachine.

It should be created and initialized before any use of state machine, or state creation. Better to do this in Event BeginPlay.

To run a StateMachine you should call it's update function whenever you want (but preferably in Tick event)

![alt text](./Documentation/bee43d2544498cf5eab0f1e25b1d0de9.png)

## Definition of a State MAchine

To define a state machine you simply put state nodes on a blueprint canvas.

![alt text](./Documentation/563c1f35ffb6ee67c6aa3a3385af5c19.png)

After adding empty state node go to it's details and select it's **State Class**.

![alt text](./Documentation/1f42a9be6b5e65477b14738a6922f687.png)

After that connect state outputs to state nodes or bluperint nodes to define state machine transition logic.

![alt text](./Documentation/25baa4391e8a40fd8fe72e82ebd20025.png)

## Troubleshooting

If, after editing state events or variables, compilation of a blueprint fails just right click on a state node and click Refersh Node.

![alt text](./Documentation/4f3d32d6c6a0a454232e096d9f85de9d.png)
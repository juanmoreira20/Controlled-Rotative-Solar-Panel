# Controlled-Rotative-Solar-Panel
A simulink/matlab control study of a Solar Panel that is designed to rotate towards the sun's exposure
This is an experiment based on matlab simulink tutorials, the data used can be founded on their website

The system uses a voltage input to control the position of the Panel based on the error feedback provided by the following system(in block diagram):

![image](https://user-images.githubusercontent.com/95920281/191161197-96695871-3b23-486a-a6c8-3358066acea3.png)

It was used a PI controller because that was no need to incorporate the derivative part of the equation, being that we are supposed to be able to pinpoint the sun's position at every instant and we´re not considerating abrupt changes such as cloud appearences.
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------
The system is based in the motor and the panel rotation. First, the motor is described by the following equation and block diagram:

![image](https://user-images.githubusercontent.com/95920281/191161376-e58fa62d-468e-4993-8a64-524e387b848f.png)

As you can see, the output of this subsystem is the Torque, which has been fed with the panel current angle velocity and the input voltage.

As for the Panel rotation, here we have the equation on which he is rotating and his subsystem's block diagram

![image](https://user-images.githubusercontent.com/95920281/191161633-a3e86433-1f64-4f4c-ae87-8bd777836bd4.png)

As you can see, the subsystem feeds our final output(position) to the scope and for the system feedback, and the velocity feedback for the motor subsystem.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Some results with different inputs:

Step:

![image](https://user-images.githubusercontent.com/95920281/191162023-08758613-2057-47ab-a6a1-d6e78355c3a1.png)

Ramp:

![image](https://user-images.githubusercontent.com/95920281/191162084-8f120cc8-20d4-4354-9350-904148688a0e.png)


Sun's Position:

![image](https://user-images.githubusercontent.com/95920281/191162155-8b675921-98bf-41ad-8cf7-c1cc992850ae.png)

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
After the initial results a study was made to proper tune the PID controller, in fact, it was used a I-PD controller, tuned by the Sokegestad rules, all in which will be displayed above.
The tuning is made based on the transfer function time constants and gains. All the math is displayed Above:
1) Finding the transfer function
i)$\frac{\theta(s)}{V(s)} = \frac{1}{s}\frac{KgKt}{KdR((\frac{Js}{Kd}+1)+\frac{K^2gKfKt}{KdR})}$





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
1) Finding the transfer function using the following differential equations

![image](https://user-images.githubusercontent.com/95920281/191574171-238da503-fda4-4b9e-8c9f-427654134506.png)

with the parameters that were explicit in the params file, we can assume that L/R is aproximate to zero, than, we can use this transfer function:
![image](https://user-images.githubusercontent.com/95920281/191582898-196c24b4-f6e9-4a3b-ba82-9f1556aee151.png)

2) Provided with the approximate transfer function, we’re able to easily see that it represents a first order system with a integrator.
Using Skogestad SIMC rules for first order systems with a integrator in series and its conversion to ideal I-PD we have:

![image](https://user-images.githubusercontent.com/95920281/191583102-3a90619f-e529-45bb-b39e-efb2bb286e89.png)

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

In this section we'll observe the differences in the process with the current presented setting and the previous step signal entry results
First, let's look into the "new" block model with the I-PD controller and the display of the voltage in the major scope

![image](https://user-images.githubusercontent.com/95920281/191591778-84a1a403-1c7a-4d47-bc03-801da97708d9.png)

Now, we'll see the results with the step entry:

![image](https://user-images.githubusercontent.com/95920281/191588478-6213b4f3-5d56-4d81-a296-202d260e64ae.png)

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

However, even with the new efficient results removing the overshoot, we must use a limit to our voltage input to a -24 to 24, using a saturation that is provided whithin the I-PD block, resulting in the following wind-up effect:

![image](https://user-images.githubusercontent.com/95920281/191589074-b8a6d653-1194-46aa-b8d5-3b51ac0c5dc6.png)

To ensure that out system is fighting this effect, we'll use the anti-wind up method of back calculation with the kb = 0.3, this provide the following results for the same -24 to 24 voltage input saturation

![image](https://user-images.githubusercontent.com/95920281/191592713-0c932431-60fb-4977-b8a9-d9ff039984de.png)












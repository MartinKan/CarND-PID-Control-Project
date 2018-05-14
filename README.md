## Udacity - Self Driving Car Nanodegree (Term 2) - PID Control Project
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

Background
---
In this project, my goal is to build a PID controller that will autonomously drive a car around a track in a simulation.

Overview of Repository
---
This repository contains the following source files that I have forked from the [main repository](https://github.com/udacity/CarND-PID-Control-Project) and subsequently modified for the extended Kalman filter project:

1.  [PID.cpp](https://github.com/MartinKan/CarND-PID-Control-Project/blob/master/src/PID.cpp)
1.  [main.cpp](https://github.com/MartinKan/CarND-PID-Control-Project/blob/master/src/main.cpp)

The PID class implements the PID controller algorithm, which is summarized as follows:

![alt text](https://github.com/MartinKan/CarND-PID-Control-Project/blob/master/PID_formula.JPG)

The PID class is initialized with the coefficients for each of the P, I and D components.  At each time interval, the error values for P, I and D are first updated by referencing the cross track error (CTE) value, and the total error value is calculated by using the formula above.  

The parameter values for P, I and D are chosen manually. I tuned each value by hand to see how it would impact on the result.  I settled in the end for P = -0.1, I = -0.0002 and D = -6.0.

The P value determines how hard the car would steer itself back to the middle of the lane.  The higher the value, the steeper the angle that the car will use when steering itself back to the middle of the lane.  This has the benefit of approaching the middle of the lane faster, but a high P value may result in a car that swerves from side to side as it constantly overshoots the target when correcting the error.  This is shown below when a high P value of -1.0 is chosen (D is zero):

![alt text](https://github.com/MartinKan/CarND-PID-Control-Project/blob/master/HighP.gif)

When a small P value of -0.1 is chosen, the car does not swerve as much:

![alt text](https://github.com/MartinKan/CarND-PID-Control-Project/blob/master/LowP.gif)

The I value is to correct any offset that wasn't addressed by the P value.  I played around with the I value during the parameter tuning process but it doesn't seem to be necessary.  An I value of zero will still allow the car to navigate itself perfectly around the track.  I chose to use a very small I value as it seems to make the cornering better (I have no proof for this, it just felt better) but a value of 0 will also work well too.

The D value counteracts against the P value and helps to pull back on the vehicle as it approaches the middle of the lane, which results in a smoother ride.  The effect of this is most pronounced during cornering, when the slightest overshooting mistake will be magnified.  Here is the car cornering with a P value of -0.1 and a D value of zero:

![alt text](https://github.com/MartinKan/CarND-PID-Control-Project/blob/master/LowPZeroD.gif)

And here is the car attacking the same corner with a P value of -0.1 and a D value of -6.0:

![alt text](https://github.com/MartinKan/CarND-PID-Control-Project/blob/master/LowPHighD.gif)

You can see how a high D value will help prevent the car from overshooting itself.

To run the code, first compile the code by running the following command:

	cmake .. && make

Then run the code by executing the following command:

	./pid

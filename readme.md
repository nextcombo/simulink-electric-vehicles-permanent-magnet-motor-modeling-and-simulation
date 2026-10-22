# Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation

1. Permanent Magnet Synchronous Motors
1.1 Overview
1.2 Modeling of PMSM
1.3 Vector Control of PMSM
1.4 Using SIMSCAPE blocks for modeling
1.5 Subsystem ECU
2 DC Motors
3 Electric Vehicles
Edited by:
1 Permanent Magnet Synchronous Motors
1.1 Overview
This paper aims to simulate the performance of permanent magnet synchronous motors (PMSM), which are controlled using the Rinehart motion system-AC motor controller. The first step is to collect all available data about the motor and its controller, which will help provide values for various variables in the modeling process. This paper uses a research paper written by Pragasen Pillay and Ramu Krishnan on "Modeling, Simulation, and Analysis of Permanent Magnet Motor Drives" to understand the modeling of PMSM and validate existing Simscape modules used for modeling PMSM and vector control. Due to time constraints, the modeling of the cooling system was simplified to a basic heat transfer model using previous engineering courses understanding and referencing the book "Heat and Mass Transfer" by R.K.
The dynamic motor model and thermal model were fine-tuned using available experimental data through parameter estimation.
PM100DZ motor controller
The motor controller converts direct current from the vehicle's energy storage system into three-phase alternating current required by the motor. The PM100DZ adopts vector control technology to control the motor's torque output.
1.2 Modeling of PMSM
PMSM and SM have similar stator and rotor windings, with the induced current in the PMSM rotor being negligible, and both produce similar back electromotive forces. Therefore, the mathematical model of PMSM is similar to that of the wound rotor. Thus, the d-q equation for PMSM is:
​Edited by:
νd and νq are the voltages on the q and d axis, iq and id are the stator currents on the q and d axis, id and iq are the stator currents on the d and q axis, Ld and Lq are the inductances on the d and q axis, λd and λq are the stator flux linkages on the d and q axis, and R and ωs are the stator resistance and the frequency of the inverter respectively. λaf is the magnetic flux due to the rotor magnets connected to the stator. The electric torque is:
Editor
The motion dynamics equation is:
Editor
P is the pole number, TL is the load torque, B is the damping coefficient, ωr is the rotor speed, J is the rotational inertia. SIMSCAPE modeling – Simscape's general model with PMSM machines, here are some details about the Simscape PMSM module:
Editor
The permanent magnet synchronous machine module operates in generator or motor mode. The operating mode is determined by the sign of mechanical torque (positive for a motor, negative for a generator). Since Pragasen Pillay and Ramu Krishnan assume that we will use this option, the module can choose between sinusoidal or trapezoidal flux. The equation driving this module is:
Editor
Editor
Here, Lq and Ld are the inductances of the q and d axes respectively, R is the resistance of the stator winding, iq and id are the currents on the q and d axes respectively, vq and vd are the voltages on the q and d axes respectively, ωm is the rotor's angular velocity, λ is the amplitude of the magnetic flux induced by the rotor permanent magnets in the stator phases, p is the number of pole pairs, Te is the electromagnetic torque and dynamic motor equation:
Editor
Among them, J is the combined inertia and rotor load, F is the viscous friction, θ is the rotor angle position, ωm is the rotor's angular velocity, Tm is the shaft mechanical torque, Tf is the shaft static friction torque. Comparing the two models, we can see that the model in the core concept research paper and the one in simscape are the same, although the assumptions cited in the paper are more. Therefore, we conclude that we can use the PMSM module, and we can use a simpler version by ignoring some variables.
1.3 PMSM Vector Control Vector control is commonly used for AC motors to convert them into equivalent excitation DC motors with very idealized control characteristics in terms of performance. Wikipedia defines vector control as a variable frequency drive (VFD) control method in which the stator current of a three-phase AC motor is identified as two orthogonal components, which can be visualized using vectors. One component defines the magnetic flux of the motor, and another component defines the torque. The drive's control system calculates the corresponding current component reference values based on the magnetic flux and torque reference values provided by the drive speed control. ". The rotor flux linkage rotates at the rotor speed ωr and is displaced from a fixed reference by the rotor angle position, as shown in Figure 1 of the vector control phase diagram:
Editor
Figure 1 Vector Control Phase Diagram
Editor
Where t is time. If id is forced to zero, then:
Editor
Editor
Since the flux is constant, the torque is proportional to the q-axis current. This can be expressed as:
Editor
Among them:
Editor
The torque equation is similar to the torque equation of a field-oriented control (FOC) dc motor. The Simscape model - Simscape has a vector control PMSM module as shown below.
Editor
Editor
This module uses the vector control logic of PMSM, which we will use to simulate our complete dynamics.
1.4 Use SIMSCAPE blocks for modeling since many variables used in motor modeling are unknown, we will create single-valued variables for these parameters so that we can use them for parameter estimation. There is no need for a step-by-step modeling guide because most modules exist in Simscape, and understanding their functions and parameter estimation is the focus. Vector control model:
Edit
Edit
Edit
The modules shown above are easily available in Simulink, and you only need to understand the functionality of the module to help create the correct circuit.
Edit
1.5 Subsystem ECU The subsystem soft ECU receives signals from HCU and sensors and calculates the necessary actions to achieve the required torque. This subsystem is imported from the provided soft MCU model, as the provided model is sufficient to meet the requirements of this article.
Edit
Edit
Edit
Edit
Edit
Need to click here:
Edit
2 DC Motor
Edit
Edit
Edit
Edit
3 Electric Vehicle
Edit

## Images

![Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation](01.gif)
![Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation](02.png)
![Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation](03.png)
![Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation](04.png)
![Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation](05.png)
![Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation](06.png)
![Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation](07.png)
![Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation](08.png)
![Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation](09.png)
![Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation](10.png)
![Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation](11.png)
![Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation](12.png)
![Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation](13.png)
![Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation](14.png)
![Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation](15.png)
![Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation](16.png)
![Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation](17.png)
![Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation](18.png)
![Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation](19.png)
![Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation](20.png)
![Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation](21.png)
![Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation](22.png)
![Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation](23.png)
![Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation](24.png)
![Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation](25.png)
![Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation](26.png)
![Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation](27.png)
![Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation](28.png)
![Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation](29.png)
![Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation](30.png)
![Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation](31.png)
![Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation](32.png)
![Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation](33.png)
![Simulink|Electric Vehicles, Permanent Magnet Motor Modeling and Simulation](34.png)

<!-- PAYMENT_BLOCK -->

## Get this dataset

- Payment link (Stripe): [Buy now](https://buy.stripe.com/3cs8yP7sY87d0vu9AB)
- Payment QR code: ![Payment QR code](pay.png)

<!-- /PAYMENT_BLOCK -->

# Smart-vehicle-reverse-braking-system
This is a C Code for an arduino circuit designed using tinkercad that acts as a smart reverse-braking system
<h3>An overview</h3><hr>
<ul>
  <li>This project intends to provide additional safety to a vehicle that comes close to an object or an obstacle, while moving in the reverse direction, by providing different lighting alerts (depending upon how close the vehicle is to an object) .</li>
  <li>Also, sound alarms come off depending on how fast the vehicle is moving towards the object ; this helps to avoid the level of damage that may occur to the vehicle as the speed increases.</li>
  <li> When the vehicle exceeds the safety limits and gets too close to an object, automatic braking is applied.</li></ul>
  <h3>Modules of the project</h3><hr>
  <ul>
<li>Module-1: Object Detection<br>
This module concentrates in detecting an object that comes close to the rear side of the vehicle using ultra sonic sensor</li>
<li>Module-2: Lighting and sound alert<br>
This module focuses on giving off lighting and sound effect to the vehicle which alerts the driver to slow down accordingly (5V red, green and orange  LED bulbs, buzzers and jump wires are used)</li> 
<li>Module-3 Speed calculation for alerts<br>
The ultra sonic sensor helps us to predict the exact distance between the vehicle and the object and also helps in predicting the speed of the vehicle.</li> 
<li>Module-4 Braking system<br>
This is the most important module which takes us one step closer to safety. This feature helps in stopping the vehicle when the vehicle reaches a particular threshold distance from an object. A servo motor is used for this purpose.</li>
<li>Module-5 Final Integration<br>
Integration of all the above modules and designing the perfect “Smart vehicle reverse-braking system”.</li></ul>
<h3>Working according to safety norms</h3><hr>
<ul>
  <li> When the distance between the vehicle and the object is between 121-200cm, the green light glows, and a message is displayed on the LCD saying that there is no object nearby, however there is no sound alert since this is a safe distance as per the standard norms</li>
  <li> When the distance is between 61-120cm, the yellow light glows, and the message on LED says that there is an object nearby, and the buzzer starts beeping intermittently. The servo mmotor slows down slightly, indicating that you can't go beyond that speed limit.</li>
  <li>If the distance goes below 60cm, the red light glows, braking system is applied, and the servo motor stops rotating, indicating that the brake has been applied.</li>
  </ul>
  
Hence, the primary objective of the project is to come up with a system that is damage-proof and provides safety to vehicles while travelling.


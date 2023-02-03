# iotlab-pilotcase-Eventcenter


Eventcenter's Challenge concept features ten game rooms referred to as Action rooms. In some of these rooms, IR technology sensors are utilized but there have been issues with their unreliability in the Twister room. 

![](https://eventcenter.se/wp-content/uploads/2021/04/Twister-384.jpg
)
# System today
Approximately 100 sensors are positioned on the walls, ceiling, and floor and are meant to respond to a hand or foot placed against the clear and frosted Plexiglas plates, but not to the Plexiglas itself. The current sensors are not deemed reliable enough and the aim is to improve their functionality either through alternative sensors or another altered setup.

![](https://dfimg.dfrobot.com/store/data/SEN0019/200324%20Update/SEN0019-detail-001_564x376.jpg?imageView2/1/w/564/h/376)


# Alternative solutions

## Velostat
Velostat is a pressure-sensitive material that changes its electrical resistance when subjected to pressure. In this scenario, velostat could be used as a replacement for the IR sensors in the Twister room. The velostat material would be placed behind the clear and frosted Plexiglas plates and would detect changes in electrical resistance caused by a hand or foot being pressed against the plates. The role of the velostat is to shorten two conductive surfaces and can be set up in several ways. The image below shows how velostat can short the left and right sides of the PCB if pressure is applied to the foam tape. 

![](https://4.bp.blogspot.com/-65hNUrMq_u4/V1m0NUIfbPI/AAAAAAAAP-U/uNxNeRBFj_QsESKMoGeGz29m-rvurAdjQCLcB/s1600/pressure%2Bsensor%2Bprototype.png)

Another way to do this is to place a conductive wire (copper etc..) on each side of the velostat film, as shown in the image below. 

![](https://i.imgur.com/gjn0nrq.jpg)

And the following circuit shows how we would connect it to a microcontroller. 
![](https://i.imgur.com/kr4XzSI.png)

Reading the analog value of GPIO is also a straightforward task. The following code snippet reads the analog value of the pin, converts it to volts, and prints the voltage to the serial monitor. 

```cpp
// the setup routine runs once when you press reset:
void setup() {
  // initialize serial communication at 9600 bits per second:
  Serial.begin(9600);
}

// the loop routine runs over and over again forever:
void loop() {
  // read the input on analog pin 28:
  int sensorValue = analogRead(28);
  // Convert the analog reading (which goes from 0 - 1023) to a voltage (0 - 3.3V):
  float voltage = sensorValue * (3.3 / 1023.0);
  // print out the value you read:
  Serial.println(voltage);
}
```

## A second option
FSR (Force Sensitive Resistor) sensors are resistors that change their resistance in response to applied pressure or force. 

In comparison to velostat, FSRs are typically more sensitive and responsive to applied pressure compared to velostat, making them more suitable for applications that require precise touch sensing. On the other hand, velostat is cheaper and easier to manufacture compared to FSRs, making it a good option for large-area pressure sensing applications.

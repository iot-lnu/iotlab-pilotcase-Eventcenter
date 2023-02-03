<!-- (This is an HTML comment). Copy and paste this entire HTML `<style>...</style>` element (block)
to the top of your markdown file -->
<style>
/* (This is a CSS comment). The below `img` style sets the default CSS styling for all images
hereafter in this markdown file. */
img
{
    /* Default display value is `inline-block`. Set it to `block` to prevent surrounding text from
    wrapping around the image. Instead, `block` format will force the text to be above or below the
    image, but never to the sides. */
    display:block;
    /* Common float options are `left`, `right`, and `none`. Set to `none` to override any previous
    settings which might have been `left` or `right`. `left` causes the image to be to the left,
    with text wrapped to the right of the image, and `right` causes the image to be to the right,
    with text wrapped to its left, so long as `display:inline-block` is also used. */
    float:none;
    /* Set both the left and right margins to `auto` to cause the image to be centered. */
    margin-left:auto;
    margin-right:auto;
    /* You may also set the size of the image, in percent of width of the screen on which the image
    is being viewed, for example. A good starting point is 60%. It will auto-scale and auto-size
    the image no matter what screen or device it is being viewed on, maintaining proporptions and
    not distorting it. */
    width:60%;
    /* You may optionally force a fixed size, or intentionally skew/distort an image by also
    setting the height. Values for `width` and `height` are commonly set in either percent (%)
    or pixels (px). Ex: `width:100%;` or `height:600px;`. */
    /* height:400px; */
}
</style>

# iotlab-pilotcase-Eventcenter


Eventcenter's Challenge concept features ten game rooms referred to as Action rooms. In some of these rooms, IR technology sensors are utilized but there have been issues with their unreliability in the Twister room. 

![](https://eventcenter.se/wp-content/uploads/2021/04/Twister-384.jpg
)
# System today
Approximately 100 sensors are positioned on the walls, ceiling, and floor and are meant to respond to a hand or foot placed against the clear and frosted Plexiglas plates, but not to the Plexiglas itself. The current sensors are not deemed reliable enough and the aim is to improve their functionality either through alternative sensors or another altered setup.

![](https://dfimg.dfrobot.com/store/data/SEN0019/200324%20Update/SEN0019-detail-001_564x376.jpg?imageView2/1/w/564/h/376)


# Alternative solutions

## Velostat
Velostat is a pressure-sensitive material that changes its electrical resistance when subjected to pressure. In this scenario, velostat could be used as a replacement for the IR sensors in the Twister room. The velostat material would be placed behind the clear and frosted Plexiglas plates and would detect changes in electrical resistance caused by a hand or foot being pressed against the plates. The role of the velostat is to short two conductive surfaces and can be set up in a number of ways. The image below shows how velostat can short the left and right side of the PCB if pressure is applied to the foam tape. 

![](https://4.bp.blogspot.com/-65hNUrMq_u4/V1m0NUIfbPI/AAAAAAAAP-U/uNxNeRBFj_QsESKMoGeGz29m-rvurAdjQCLcB/s1600/pressure%2Bsensor%2Bprototype.png)

Another way to do this is to place a conductive wire (copper etc..) on each side of the velostat film, as show in the image below. 

![](https://i.imgur.com/gjn0nrq.jpg)

And the following circuit show how we would connect it to a microcontroller. 
![](https://i.imgur.com/kr4XzSI.png)

Reading the analog value of GPIO is also a straight forward task. The following code snippet reads the analog value of the pin, converts it to volts and prints the voltage to the serial monitor. 

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

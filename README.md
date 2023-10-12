# Water-Level-Indicator-Project-
# Automated Water Level Monitor System
# Course : ICE 3107


# Objective :

The main purpose of this device is to provide its users a hassle free experience. Just install the system once and you are good to go. The device monitors the water level inside your reservoir using Ultrasonic/Sonar sensor & then controls the water pump accordingly.

# Components :

 -PIC16F877A Microcontroller - 1 Pc
  *Ultrasonic Sensor - 1 Pc
 *5v voltage Regulator (LM7805) - 1 Pc
 *Crystal oscillator (16 MHz) - 1
 *Capacitors (22pF) - 2Pc
 *Wires
 *LED - 3 Pc
 *5v Relay - 1 Pc
 *9v Battery - 1 Pc
 *Breadboard
 *Software Used :


Procedure :

We had to setup the ranges (distance) for our water tank using the Ultrasonic sensor. We had three levels: Full, Half and Empty. For fixing up the ranges we used the serial monitor of the Arduino microcontroller and used a piece of code to generate a signal and take the readings.
We then made our simulation using the Proteus simulation tool.
We wrote the necessary conditions for our system using Mikro C and tested it in our Proteus simulation.
After testing the simulation we used the Pic-kit 3 burner to burn our code into the microprocessor 16F877A.
The Sonar sensor’s trig pin is connected to the Pic’s RB0 pin as output and echo pin is in RB1 as input.
Then the rest of the pins such as RB2, RB3, RB4, RB5 are connect to green led,yellow led,red led and relay.
So when the input comes from the sonar to the pic depending on the condition the LED’s and the relay will light up.
For testing purposes we considered our water tank to be is total 40 cm.
Here we set the lower level from 30 cm to 40 cm which indicates the water level is low and light up only the red led ,also turn on the relay.
The Relay (which control 220v AC pump motor) will be turned on until the tank gets full of water. In this case, water and ultrasonic sensor will keep distance of 10 cm. That means, at 10 cm motor/relay will be turned off. Or we can say the tank will be full.
The middle level is from 20-29 cm which will light up both yellow and red led but not the relay.
Lastly the upper level from 10-19 cm which will light up all the led’s but not the relay as it indicated the tank is full.
Image of hardware Implementation :

# Implemented picture

![2](https://github.com/nayan-pust/Water-Level-Indicator-Project-/assets/114688354/75959e07-be29-4257-934f-0fe6993baf56)


# CODE mikrC 
```ruby /*
RB0 is Trig Pin
RB1 is Echo pin
RB2 is green led pin
RB3 is yellow led pin
RB4 is red led pin
RB5 is for motor
*/

int findDistance()
{
    int distance1 = 0;
    TMR1L = 0x0;
    TMR1H = 0x0;
    RB0_BIT = 1;
    delay_us(10);
    RB0_BIT = 0;
    T1CON.F0 = 1;
    while(RB1_BIT);
    T1CON.F0 = 0;
    distance1 = (TMR1L | (TMR1H<<8));
    distance1 = (distance1*0.034)/2;

    return distance1;
}

void main() {
int distance = 0;
TRISB = 0x02;

PORTB = 0x0;
TMR1L = 0x0;
TMR1H = 0x0;

while(1)
{
    distance = findDistance();
    if(distance >= 30)
    {
        RB2_BIT = 0;
        RB3_BIT = 0;
        RB4_BIT = 1;
        RB5_BIT = 1;

        while(distance > 10)
        {
            if(distance >= 30)
            {
                RB2_BIT = 0;
                RB3_BIT = 0;
                RB4_BIT = 1;
                RB5_BIT = 1;
            }
            else if(distance >= 20 && distance <= 29)
            {
                RB2_BIT = 0;
                RB3_BIT = 1;
                RB4_BIT = 1;
                RB5_BIT = 1;
            }
            else if(distance >=11 && distance <=19)
            {
                RB2_BIT = 1;
                RB3_BIT = 1;
                RB4_BIT = 1;
                RB5_BIT = 1;
            }
            else if(distance <=10 )
            {
                RB2_BIT = 1;
                RB3_BIT = 1;
                RB4_BIT = 1;
                RB5_BIT = 0;
            }
            distance = findDistance();

         }
    }
    else if(distance >= 20 && distance <= 29)
    {
        RB2_BIT = 0;
        RB3_BIT = 1;
        RB4_BIT = 1;
        RB5_BIT = 0;

    }
    else if(distance >=10 && distance <=19)
    {
        RB2_BIT = 1;
        RB3_BIT = 1;
        RB4_BIT = 1;
        RB5_BIT = 0;
    }
}

}

```




# Water-Level-Controller-using-8051-Microcontroller
The water level controller, which uses the 8051 microcontroller project, helps automatically control the water motor by detecting the water level in a tank. In this article, you will learn how to detect and control the water level in a tank or other container. This system monitors the tank water level and automatically turns ON the Motor when the tank is empty.

The Motor is turned OFF when the top tank or tanky is full. Here the water level of the tank is shown on the LCD screen (liquid crystal display). With this system, we can also avoid overflowing the water. Here we are designing the circuit which is used to detect and control the water level automatically in the overhead tank using 8051 Microcontroller.

# Introduction
Water level controller, the name itself indicates that an electronic device or circuit kit used for controlling the water level can be termed as a water level controller. It is difficult to know the level of water in the overhead tank such that wastage of water can happen frequently. To conserve water, avoid overflow of water in the overhead tank which may cause loss of water, loss of electrical power, etc.,. Thus, an ultrasonic water level controller using 8051 microcontroller is an innovative electronics project application for controlling water level.

A Water Level Controller using the 8051 Microcontroller project will help in automatically controlling the water motor by sensing the water level in a tank. This article explains how to detect and control the water level in an overhead tank or any other container. This system monitors the water level of the tank and automatically switches ON the motor whenever the tank is empty.

# Need of Project
A water level controller is a device that manages water levels on a variety of systems such as water tanks, pumps and swimming pools. The basic function of a water level controller is to regulate water flow and optimize system performance. One of the main advantages of water level control devices includes the ability to control power fluctuations when the motor is switched on. Most of these devices ensure uninterrupted water supply by filling the overhead tank once it is below level. The motor power is switched on when the overhead tank becomes empty and switches off automatically when the underground tank is empty or the overhead tank becomes full. In this way it becomes easy to ensure 24 hours water supply without any kind of interruption

# Application
Fuel level indicator in vehicles.
Used in big buildings where manual monitoring is difficult.
Used in industries to control the liquid level automatically.
Automatic water level controllers can be used in Homes apartments, commercial complexes.
# Limitation
The Rust, Foul and Deteriorate.
Wire use in the tank can be replaced every two years.
System Circuit Diagram
Capture
# Component Used
AT89S52 Microcontroller (or any 8051 based Microcontroller)
8051 Programmer (Programming Board)
11.0592 MHz Quartz Crystal
2 x 33pF Capacitor
2 x 10KΩ Resistor (1/4 Watt)
10µF Capacitor
Push Button
1KΩ x 8 Resistor Pack (for Pull – up)
16 x 2 LCD Display
5V Relay
4 x 2N2222 (NPN) Transistors
DC Motor (for demonstration)
10KΩ Potentiometer
1N4007 PN Junction Diode
Programming cable
Connecting wires
Power Supply
Keil µVision IDE
#Proteus (for circuit diagram)
![image](https://github.com/nayan-pust/Water-Level-Indicator-Project-/assets/114688354/ffb09076-791e-41d7-8cea-ceaab4beeb10)


# Algorithm for Water Level Controller Circuit
1] First configure the controller pins P0.0, P0.1 and P0.2 as inputs and P0.7 as output. Now, initialize the LCD.
2] Continuously check the water level input pins P0.0, P0.1 and P0.2.
3] If all the pins are low, then display tank as “EMPTY” on the LCD and make P0.7 pin HIGH to run the motor automatically.
4] If the level is low i.e. if P0.0 is HIGH, display the water level as “LOW” and continue to run the motor.
5] A HIGH pulse on the pin P0.1 indicates that water has reached half level. So, display the same thing on LCD and run the motor normally.
6] If P0.2 is HIGH, then the water level in the tank is FULL.
7] Now, make the P0.7 pin as LOW to turn off the motor automatically.
# How to Operate Water Level Controller Circuit using 8051 Microcontroller?
Step 1 - Initially, write the program for Water Level Controller in Keil µVision IDE and generate the .hex file.
Step 2 - Burn the program (.hex file) to the microcontroller using external programmers and Proteus Software.
Step 3 - Now give the connections as per the circuit diagram.
Step 4 - If water in the upper tank is below the lower sensor, turn on the motor and display the message ‘Tank is empty and Motor is on’.
Step 5 - If water in the upper tank is above the lower sensor and below the mid sensor, turn on the motor and display the message ‘Tank is empty and Motor is on’.
Step 6 - If water in the upper tank touches the upper sensor, turn off the motor and display the message ‘Tank is full and motor is off’.
Results
# Simulation Result State - 1
![image](https://github.com/nayan-pust/Water-Level-Indicator-Project-/assets/114688354/ee2ea464-6907-430e-bfcc-2abd5145194f)

TANK IS EMPTY AND MOTOR IS ON SIMULATION RESULT
Simulation Result State - 2
![image](https://github.com/nayan-pust/Water-Level-Indicator-Project-/assets/114688354/6bc09395-2088-4f43-b2a7-195b328ab2f9)

TANK IS FULL AND MOTOR IS OFF SIMULATION RESULT

# CODE mikroC 

```ruby
sbit full at P1.B0;
sbit mid at P1.B1;
sbit emp at P1.B2;
sbit t2 at P1.B3;
sbit rs at P0.B0;
sbit rw at P0.B1;
sbit en at P0.B2;
sbit rly at P3.B0;

void lcddata(char[], char);
void lcdcmd(char);
void msdelay(unsigned int);

void main() {
    rly = 0;
    P0 = 0x00;
    P2 = 0x00;
    full = 1;
    mid = 1;
    emp = 1;
    t2 = 1;

    lcdcmd(0x38);
    lcdcmd(0x0C);
    lcdcmd(0x06);
    lcdcmd(0x01);

    while (1) {
        if (t2 == 0) {
            if (emp == 1 && mid == 1 && full == 1) {
                rly = 1;
                lcdcmd(0x01);
                lcdcmd(0x80);
                lcddata("tank is empty", 13);
                lcdcmd(0xC0);
                lcddata("motor is on", 11);
            } else if (emp == 0 && mid == 1 && full == 1) {
                rly = 1;
                lcdcmd(0x01);
                lcdcmd(0x80);
                lcddata("tank filling", 12);
                lcdcmd(0xC0);
                lcddata("motor is on", 11);
            } else if (emp == 0 && mid == 0 && full == 1) {
                rly = 1;
                lcdcmd(0x01);
                lcdcmd(0x80);
                lcddata("tank is mid", 11);
                lcdcmd(0xC0);
                lcddata("motor is on", 11);
            } else if (full == 0 && mid == 0 && emp == 0) {
                rly = 0;
                lcdcmd(0x01);
                lcdcmd(0x80);
                lcddata("tank is full", 12);
                lcdcmd(0xC0);
                lcddata("motor is off", 12);
            }
        } else {
            rly = 0;
            lcdcmd(0x01);
            lcdcmd(0x80);
            lcddata("tank 2 empty", 12);
            lcdcmd(0xC0);
            lcddata("fill tank 2", 11);
        }
    }
}

void lcdcmd(char cmd) {
    P2 = cmd;
    rs = 0;
    rw = 0;
    en = 1;
    msdelay(5);
    en = 0;
}

void lcddata(char a[], char len) {
    char x;

    for (x = 0; x < len; x++) {
        P2 = a[x];
        rs = 1;
        rw = 0;
        en = 1;
        msdelay(5);
        en = 0;
    }
}

void msdelay(unsigned int a) {
    unsigned int x, y;

    for (x = 0; x < a; x++)
        for (y = 0; y < 1275; y++);
}

```


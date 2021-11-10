# Analog music synthesizer
![](media/3cb7b73756102739de394550df0a3099.jpg)

|                                                                                                        |
|--------------------------------------------------------------------------------------------------------|
| Module code: ELEC40006 Lecturers: Dr. Stott and Mrs. Perea 14/06/2020                                  |
| Group name: Luozhixiang    Songyu Huang CID:01716233 Ziheng Qi CID:01714505 Yingkai Yang CID:01516794  |

![图片包含 游戏机, 盒子, 食物
描述已自动生成](media/d65c8c67386744610ca3319dcb439eda.jpg)

![图片包含 游戏机, 盒子, 食物
描述已自动生成](media/d65c8c67386744610ca3319dcb439eda.jpg)

目录

[1. Introduction](#introduction)

[a) Technical problem](#technical-problem)

[b) Design Criteria](#design-criteria)

[2. Design process](#design-process)

[A. Overview of the design](#overview-of-the-design)

[i) High-level design](#high-level-design)

[ii) Detail design](#detail-design)

[iii) Final connection and test results](#final-connection-and-test-results)

[3. Project planning and management](#project-planning-and-management)

[A. Organization](#organization)

[B. Meeting structure and time
management](#meeting-structure-and-time-management)

[4. Evaluation](#evaluation)

[Further improvement](#further-improvement)

[Power consumption](#power-consumption)

[Bills of material](#bills-of-material)

[Effects of High Tolerance components](#effects-of-high-tolerance-components)

[5. Conclusions](#conclusions)

[6. Reference](#_Toc43066447)

[7. Appendix](#_Toc43066448)

# Introduction

An analog (or analogue) synthesizer is a
[synthesizer](https://en.wikipedia.org/wiki/Synthesizer) that uses [analogue
circuits](https://en.wikipedia.org/wiki/Analogue_electronics) and [analogue
signals](https://en.wikipedia.org/wiki/Analog_signal) to generate sound
electronically.

## Technical problem

Analogue Synthesisers are wildly used in modern music production. The purpose of
this project is to design a circuit for an Analogue Synthesiser and simulated on
LTspice. Trying to make the synthesiser as authentic as the real sound of
instruments.

## Design Criteria

-   The synthesiser must generate audio frequency tones for the 7 notes in the C
    major scale.

-   The keys on the keyboard of the Analogue Synthesiser can be symbolized using
    a voltage source on LTspice, where 5V represents a pressed key and 0V means
    the key is released.

-   A loudspeaker with 8Ω impedance can be driven by the synthesiser.

-   No ‘behavioural’ components or any other sources can be used in the final
    design.

-   More functionalities can be added to the design to make the synthesiser
    sound more accurate compared to real instruments.

-   Matlab script can be used to listen to the output wave from the synthesiser.

# Design process

## **Overview of the design**

### High-level design

The synthesiser is made by different parts of the circuits. Each part has its
functionality. The two diagrams below show the block diagram of the synthesizer.

![synth10_11](media/0510b408710137b961c1b8ca5020b49e.gif)

The output of the first diagram goes to the input of the second diagram.

![](media/547ebd118451c3d4988505cd778c4835.png)

-   **The trigger block** represents the keys on the keyboard.

-   **The voltage-controlled oscillator blocks** are used to generate different
    waveforms, such as sine, square, sawtooth, and triangular. Sound tones are
    related to waveforms.

-   The envelope generator changes the volume of the sound dynamically when keys
    are pressed and released. It can also be used to adjusting the timbre, as
    well as modulating the filter to change the sound.

-   The mixer allows waves of the sound to be mixed. This makes the synthesiser
    can be monophonic or polyphonic.

-   The voltage-controlled amplifier is used to amplify the signal from the
    oscillator. Where the gain of the amplifier is controlled by another signal.
    Volume control and envelop shaping of the sound is achieved using this
    amplifier as well.

-   The voltage-controlled filter is responsible for shaping the tones and
    frequency. Same as the amplifier, this can be controlled by a signal as
    well.

The second block diagram connection is one of the options for the users, it can
several other connections. There is also another block called Low-frequency
oscillator which helps provide the low-frequency input for the control input of
the VCA and VCF.

### Detail design

#### Trigger

This part is achieved using a PWL voltage source in LTspice. 5V means the key is
pressed and 0V means the key is released. The picture below shows an example of
a PWL voltage source. Also called gate signal.

![](media/94353d869519e317773a0ed9a4f9f13e.png)

figure 1

The PWL creates a pulse from 0.5s to 2s, represents the key is being pressed for
1.5s.

#### VCO ---- Voltage-controlled oscillator

Sound is produced by oscillations and different notes just oscillate with
different frequencies. However, various shapes of waves also sound different.
Therefore, we produced a voltage control oscillator with four fundamental
waveforms.

The most used four waveforms are the sinusoid wave, triangular wave, sawtooth
wave, and square wave.

##### Sine wave

Sinusoid wave only contains two parameters which are frequency and amplitude. A
wein bright oscillations are used to generate the sinusoid wave.

https://www.electronics-tutorials.ws/oscillator/wien_bridge.html

How wein bridge oscillations work

![](media/2ddf5de72c03ea8db039133b870e8afc.png)

The output of the op-amp is fed back to both inverting and non-inverting input
of the amplifier. R1 and R2 form a non-inverting amplifier configuration, so
gain should be .

The series connection of RC is known as a high pass filter and the parallel
connection of RC is known as a low pass filter. These two RC circuit forms a
band pass filter which means neither too high nor too low frequency can pass. Z1
and Z2 are used to represent the impedance of series and parallel connection of
R and C. Vout/Vin should be .

![oscillator output gain](media/bed34902a39f42b6fbf7426f392dc72b.gif)

The impedance of a capacitor is . It will cause a 90-degree phase shift. At very
low frequencies the phase angle between the input and output signals is
“Positive” (Phase Advanced), while at very high frequencies the phase angle
becomes “Negative” (Phase Delay). At the resonance frequency, the phase
difference is zero. So, the only term left in the transfer function is 1/3. only
at a certain frequency (resonance frequency) the output will be maximum. The
resonance frequency is .At this case, the non-inverting input will be one-third
of the op-amp output. To get a sustained oscillator, so the product of inverting
and noninverting gains should be 1. So must equal to 3. In another word, R1 must
equal 2R2.

For example, generating notes Si in C major. The frequency should be about 493.
8HZ.we set R and C to be 3324ohms and 0.1ufara respectively and R1 is exactly
two times of R2. Frequency of the output sine wave should be .

![](media/2b217be14a6ce194e8643272f043b24d.png)

This picture shows the circuit and the waveform of the output signal. The shape
of the wave and the frequency is perfect, but its amplitude is too small which
about 6mv. An inverting amplifier is added to the output. Gian of this
configuration is times, the picture shows that amplitude increase without any
change in frequency. ![](media/95a9c6e64f19f59c420c8b45190ad45a.png)

##### Square Wave

A 555 timer is used to generate the square wave.

![555 Timer Block Diagram](media/f95c5e306b497180cd36cf6c2728526a.png)

From the block diagram, it consists of two comparators, a flip-flop, a voltage
divider a discharge transistor, and an output stage. The voltage divider
consists of three identical 5kohms resistors. That is why it is called 555
timers. it produces two reference voltage at one third and two-third of VCC. The
comparator is the circuit that compares the reference voltage and the input. if
THRESHOLD connecting to non-inverting input is HIGHER than the reference
voltage( VCC) connecting to the negative terminal, the output of the first
comparator will be 1, otherwise, the output will be 0. For the second
comparator, if THRIFFER connecting to non-inverting input is LOWER than the
reference voltage( VCC) connecting to the negative terminal, the output will be
1, otherwise, it will output 0.

In terms of the flip-flop, input R represents “reset” if Input R is high, the
flip-flop output Q will be reset and if Q is already 0 there will be no effect.
On the other hand, S represents “set” if Input S is 1, the flip-flop output Q
will be set to 1 and if Q is already 1, there will be no effect.

The discharge transistor connects to the ground and it can ground the flip-flop
output at any time if the output of the flip-flop is low.

The output stage is used to provide high output resistance and it also has an
inverse output compares to the flip-flop.

![](media/2290a72c33a836a2de0b6570c91c27e7.png)

In this circuit, two inputs are connected, so at any time input TRIGGER and
THRESHOLD will have the same value.

Initially, the voltage source is at zero and starts charging the capacitor
through the Resistors R1 and R2. At that time, 0(THRESHOLD) less than 2/3VCC, so
the first comparator outputs 0 and the second one outputs 1 because of 1/3VCC
greater than 0(TRIGGER). The output of the flip-flop is set to 1 because of R=0
and S=1. Outputs of both comparators won’t change until the voltage across the
capacitor is over one-third of VCC. The second comparator will switch from 0 to
1 because TRIGGER is larger than 1/3VCC. But it will make no difference because
both inputs of the flip-flop are 0. Once the voltage reaches 2/3VCC. THRESHOLD
is greater than 2/3VCC. The first comparator will output 1 therefore, reset the
flip-flop output to 0. The low output of flip-flop activates the discharge
transistor and connects the capacitor to the ground. the capacitor starts to
discharge through a resistor R2.

as the voltage across the capacitor decreases, the first comparator outputs 0
again, flip-flop output does not be affected because it already set to 0. But
Once the capacitor voltage drops to 1/3 VCC. The second comparator has an active
high output that causes an active high flip-flop output. The discharging
transistor is turned off. The capacitor starts charging again. Overall, the
voltage that crosses the capacitor will fluctuate between 1/3VCC and 2/3VCC.

The process of charging and discharging will go through repeatedly by its own
that produces a square wave. The output of 555 timers is inverse of the
flip-flop output.

![555 Timer Astable Mode Output Square
Wave](media/138a4667f22bf47c653ebcc8a738847b.png)

This picture indicates the relationship between the capacitor voltage and the
output stage. A square wave can be divided into high and low times. The square
wave is high when capacitor charges and active low when it discharges. High
times depend on the capacitance of C, the resistance of R1 and R2. Low time only
depends on R2 and C. both times can be calculated using the formula of charging
a capacitor.

High times= Low times=.

The period of the wave equals the sum of high time and low time; frequency is
one over the period. . The duty cycle of the square wave can be calculated by
using High times divided by the period which is . To get a 50% duty cycle square
wave. We set R2 much larger than R1.

This picture is the circuit and simulation result for the square wave of notes
la. The resistance of R1 equals 3.3kohms and R2 is 33kohms, R2 is one time
larger than R1 which makes the duty cycle to be approximately 50%. The reading
of the cursor indicates the frequency is right.

##### Triangular wave

Triangular wave is generated from the square wave using an RC integrator. These
two types of waves therefore always have the same frequency. There is a
limitation that this method only works for the square wave with a 50% duty
cycle.

![](media/8cf03749b0b00cc17fd48c2cdd2eb107.png)

RC integrator is a type of low pass filter which contains a capacitor and a
resistor. As we know the speed is charging a capacitor is not linear. The time
taken for a capacitor to fully charged is equal to five RC time constants when
the capacitor connected to a constant voltage source. After replacing the
constant voltage source with a square wave(pulse). The capacitor only charges
when the square wave is in high and discharges when it in low times. The shape
of the wave depends on the difference between the RC constant and the period of
the input square wave. We assume the square wave’s duty cycle is 50%. When the
period of the input square wave is 10RC. The capacitor is fully charged during
the “high times” (0 to 5RC) and then fully discharged during “low times” (5RC to
10RC). The amplitude of the output signal is the same as the input square wave.
The waveform is shown in the picture below.

![square wave rc waveform](media/fad488c1c6400768c168c08689fddfe0.gif)

If the period of the input square wave is even larger. The capacitor will stay
fully charged and discharged longer producing the waveform shown in the picture.
![longer rc time period](media/a29177e70774c295a24de00f3b3a9450.gif)

When the period less than 10RC.The capacitor will not have enough time either to
fully charge or discharge. Therefore, the amplitude of the output signal drops.
The smaller the period is the larger the difference is between input and output.

![short rc time period](media/2cb4a4e5ba1cfab88bdaad414a3adba4.gif)

However, the waveform will be closer to the triangular wave as the period
decreases. The period should be held constant and a rise in the RC constant
could provide the same result.

![](media/94bf59ba708b41f6916fe60788be1efb.png)

For example, we choose a 100kΩ resistor and 22.7nF capacitor to form the low
pass filter for note la. The simulation result shows a good triangular waveform
with a much smaller amplitude.

##### Sawtooth wave

The sawtooth wave is generated using two PNP and an NPN transistor.

![](media/f8aece9e384a453f04d5fc5a8dbe417d.png)

the left part of the circuit becomes a constant current source charging the
capacitor C1. To be specific, Resistor R1 and R3 set Q1’s bias voltage to be
5.5v. it turns on Q1 and allows current flows from emitter to collector. the
current flowing through the collector of Q1 is about 30microamphers, it charges
the capacitor at a constant speed. This forms the rising edge of the sawtooth
waveform. The right part of the circuit forms a positive feedback circuit that
ground the capacitor at an extremely high speed. it also contains a potential
divider that sets the base voltage of Q2 to be 3v. once the voltage across C1 is
over 3.7v. Q2 will be turned on. the collector current of Q2 is Q3’s base
current and the collector of Q3 is connected to the base of Q2. It forms a loop
that reinforces both transistors and discharges the capacitor immediately. This
forms the very steep falling edge. The voltage reduces until it is too small to
turn on Q2 and Q3. It will start charging again and repeat the process.

The period of the sawtooth wave can be increased by using a larger capacitor.
Because it requires more time to charge up.

For example, this picture shows the circuit and the simulation result of the
sawtooth wave of note la. The output wave has a frequency of 439.5 which fits
the requirement.

![](media/b8e54eee8d80e947176f79341028a6bd.png)

##### Modification of the oscillator

After building the VCA, we realized that the four types of the waves all have
different amplitudes and some of them also contain a DC offset. An inverting
amplifier is used to set the amplitude of all output signals to 1v and another
amplifier configuration is used to remove all DC offset of triangular sawtooth
and square wave. ![](media/37e7923f90d0a0a9d35d3619fc80dcbe.png)

![](media/045218bc6a11a9acea7aec0ed90b2816.png)

These pictures show the different simulation results before and after we
modified the amplitude and remove DC offset.

#### LFO ---- Low-frequency oscillator

Potential meters are required in LFO; however, it cannot be found in the library
of LTspice.

![](media/7b2106b7f407b64280c14df9464c24b8.png)

This is the circuit and symbol design of potential meter. Between port1 and
port2 is the part of the resistor that connected into the circuit. It consists
of a parameter pot to represent which fraction of the resistor is connected into
the circuit.

The biggest difference is that it will produce waves with a very low frequency
which is normally cannot be heard by humans. Out LFO can produce three types of
waves with frequency from 3 to 30. The picture below indicates the circuit
design. There are three output ports which are square sine and triangular wave.
The left two potential meters control the frequency of the wave. The right one
controls the shape of the sine output. It outputs a perfect sine wave when the
potential meter switches to 50.

The output of LFO cannot be heard by humans, but it can be used as a control
signal. In other words, “invisible hand” so that it can produce many sounds that
cannot be made manually. For example, applying a 10hz square wave to the control
signal of VCF

![](media/8fbda341a299787d905e128cf4ce4134.png)

LFO works similarly with VCO，when the transistor Q1 is turned off, capacitor C1
charges up until it reaches the threshold voltage of the op-amp U2. U2 will
output a negative voltage that turns the transistor on. capacitor C1 therefore
is connected to the ground and starts to discharge. The process of charging and
discharging will go through repeatedly by its own that produces a square wave
and a triangular wave. The threshold voltage of U2 is set by resistor R11 and
R11. The potential meters in the left can provide frequency control. When
switching it from 1 to 100. The frequency increases from 3HZ to about 30HZ. The
right part of the circuit is designed to generate a sinusoid wave. It is
connected to the triangular wave output to convert the triangular wave into a
sinusoid wave. The triangular output goes through two transistors that form a
differential amplifier configuration. An integrated circuit is connected at its
output to create a sin wave. However, this circuit cannot produce a perfect
sinusoid wave. The third potential meter is used to find a better sinusoid
waveform. After tests, we set the parameter of potential meter to 50 which can
generate the best sinusoid wave.![](media/3090b33a68f7dce632ab435792d17196.png)

The amplitude of the three waves is approximately the same. The frequency showed
in the graph is 14hz, which is very low.

#### EG ---- Envelope Generator

The envelope Generator is also known as the ADSR, which means it can generate a
signal with four stages: Attack, decay, sustain, and release.

![](media/56f3a948631d7d3e71af75913bd542da.png)

Attack:

The attack time is how long the sound takes to increase its volume from zero to
the maximum value when you press a key.

Decay:

The decay time is how long the sound volume decreases to the sustain level after
the maximum value has reached. The decay stage is immediately after the attack
stage.

Sustain:

The sustain level is the volume of the sound produced after the attack and decay
stage, the key is still pressed.

Release:

The release time is how long the volume of the sound decreases to zero after the
key is released. The release stage is after the sustain stage.

The input signal of the envelope generator is the gate signal, which represents
when the key is being pressed and when it is released.

The ne555 timer chip is the heart of the envelope generator.

![](media/9e63a8214f0ddfb0a08adfec6308ec2c.png)

According to the graph of the envelope generator, it is similar to a monostable
circuit with some delays at the attack and release stage. Therefore we can
modify the monostable configuration of the 555 timers to achieve the ADSR
diagram.

The circuit can be separated into different blocks.

![图片包含 游戏机, 钟表
描述已自动生成](media/85dfb105c459b571f69af9ad605d56cf.jpg)

The input signal of the envelope generator is a gate signal. However, the
555timer’s trigger input is active low, which means the 555timer only being
activated when there is a low pulse arriving at the trigger input.

Below are the steps of the final design circuit to generate ADSR.

1.  The transistor blocks will generate a low pulse when the key is being
    pressed, thus activate the 555timer.

2.  The output of the 555timer will go high. Then the current will arrive at the
    attack pot to charge the capacitor.

3.  The threshold pin is connected to the capacitor of the attack pot. Once, the
    voltage reaches a certain voltage that goes above the threshold voltage, the
    output will zero. The capacitor will start discharging.

4.  As the voltage at release the pot is 5V, the threshold voltage is lower than
    5V, the current will not flow in the release pot. It will flow out of the
    capacitor to the decay pot due to lower voltage at the lower part of the
    circuit. And start sinking current to the opamp.

5.  The opamp is in a negative feedback configuration, this will make two inputs
    of the opamp same. Therefore the opamp is used to sinking current that comes
    out of the capacitor from attack pot.

6.  When the voltage decreased to a certain level. The sustain pot is connecting
    to the non-inverting input of the opamp to force the output of the envelope
    generator to stay at a certain level when at the sustain stage.

7.  As soon as the key is being released, the gate goes low, the transistors
    will be biased and can be sinking current. Then the current left at the
    attack capacitor will start flows to the release pot, as the voltage at the
    upper end is lower than the threshold voltage of the 555timer.

8.  The reset pin of the 555 is also connected to the release pot, this ensures
    that when the voltage across the release pot reaches close to zero, the
    555timer will be reset and the process can start over again.

The circuit is built block by block.

The transistor blocks are used to make a low pulse when the key is pressed.

The gate signal is representing key pressed and released.

![](media/d8b1fca17d1fc33e6c773e4b7670ad0c.png)

![](media/216a6ab66d0e4bacc75c88e49020b91f.png)

The white line shows a low pulse when the gate is high.

The picture below shows the whole design of the circuit.

![](media/522c49d6189caef437f7120291c7d996.png)

The circuit is built based on the block diagram above. The diodes in each block
make sure that the current only flows in one direction. There is a voltage
follower at the end to protect this circuit from being affected by other
circuits when connecting.

![](media/584369755e95bbff2dc56da3a26473cb.png)

The graph showed above proved that this circuit completed the ADSR stage.

However, the circuit did not perform perfectly when the key is not being
pressed. The graph had a small offset causing the output at both ends is not 0V.
This may cause problems when connecting the Envelope generator to the
voltage-controlled amplifier, as the gain may not be zero if the envelope
generator is not 0 when the key is not pressed.

To fix this problem, the graph must be shifted down about 0.8V, a subtractor
must be used to shift this graph down.

![](media/eacb414e4014f7bb4ccaf4d560225529.png)

\-Vr is the voltage that we need to bring this voltage down.

Vr must be 0.8 in this case. After applying this at the end of the circuit.

![](media/6abddae3f74f7e71ea411d38ac2df11d.png)

![](media/cb049f235049d72f2368b8ed36280609.png)

This is the final result for the envelope generator corresponding to the gate
signal shown in figure 1.

Finally, The different resistor names in the circuit can be used to change the
corresponding attack, decay, release time, and sustain level. All these five
resistors can be replaced by five potentiometers, make it easy to change the
time outside the block. The sustain resistors are used as a potential divider to
control the sustain level, the attack resistor is used in an RC configuration,
corresponding to a time constant τ. Increase the specific resistor will increase
the corresponding attack decay and release time.

#### VCR ---- Voltage-controlled resistor

The voltage-controlled resistor, the VCR, is one important component in
voltage-controlled circuits. The resistance of the VCR is varied by the voltage
applied to it. Two types of VCR are used in this project, including JFET and
Diode.

##### JFET

![](media/0bc9a43f2c3346256428310a9c17b103.png)JFET is the VCR component in the
design of VCA. There are linearized VCR design and non-linearized VCR design. In
this project, non-linearized VCR is chosen. It just costs one JFET and does not
affect the result much.

The JFET has two operating regions: saturation region and linear region. The
saturation region is the flat part in Figure 1 where it operates as a
voltage-controlled current source. No matter how drain-to-source voltage (VDS)
changes, the current through the JFET remains constant. In the linear region,
the JFET acts as the voltage-controlled resistor where the resistance is shown
as the slope of each curve and determined by the particular gate-to-source
voltage (VGS). Preferably, there is no DC voltage across the FET’s drain and
source terminals in the VCR mode (Ron Quan). Therefore, the resistive effect
should be able to extend to the negative VDS voltage region, and then it can
operate around 0 dc offset.

##### Application of JFET

![](media/3ee8d38b57a0f27467850de33aa83930.png) In the circuit, there are always
two control voltage sources: one controls the VDS and the other provides DC
supply for the circuit. As VGS changes, the resistance, Rds, of the JFET varies.
With specific VGS, as long as JFET stays in the linear region, it just behaves
like a normal resistor. Hence, R1 and Rds form a potential divider, and an
equation for VOUT can be derived as

If the DC voltage source is replaced with a sine wave or other AC signal, and
the VGS is changed to a voltage source with a specific input signal, a varied
amplitude sine wave can be observed from the VOUT port.

##### Diode

![C:\\Users\\yyk20\\AppData\\Local\\Microsoft\\Windows\\INetCache\\Content.MSO\\226BDAA4.tmp](media/9bed15945a8af051e01007f15e439fa2.png)The
diode is the VCR component in the design of both VCF and VCA. Ideally, the diode
is a one-direction conductor. When the voltage at Anode is higher than the
voltage at Cathode, it is under forward bias, and the diode acts like a
wire----the current flows from left to right. When the voltage applied to the
Cathode is higher, it acts as an open circuit, and there will be no current.
However, realistically, the diode is not ideal. Within a small voltage region,
while the diode turns from an open circuit to fully conduct, the diode behaves
like a resistor.

![](media/d6bd402f38a8525ea54e7ae67888ec09.png)![](media/99eeb251f1b433be3b0e0d165c16d979.jpeg)When
the diode is required to be voltage-controlled resister, the resister should
under forward bias voltage. Figure 4 shows the relationship between the
resistance of diodes and voltage across the diodes. Same as the JFET, the
resistance of a diode also varies with a forward bias voltage applied to it.
However, unlike the JFET, diodes are very good resistor-behave devices with a
small ac signal. In other words, the amplitude of the ac signal should remain
small to get a relatively constant resistance with the same dc forward bias
voltage.

Figure 5 shows how diode behaves under different voltage. The slope of the curve
is not constant which means the resistance of the diode varies with the forward
bias voltage applied to it. However, under a specific dc voltage, the slope of
the curve close to the point is relatively constant. Hence, diodes can be used
as normal resistors for small ac signal operation.

##### Application of diode

![Diode ladder network. \| Download Scientific
Diagram](media/58b0da652c46580c75794f6b17aaa9b2.png)In the circuit, always more
than one diode is used at once because the potential difference across the
voltage-controlled resister always exceeds the limit of one diode. To tackle
this issue, diode ladders are always applied to the circuit. The number of
diodes is determined by the potential difference across the diodes ladder.
Higher the potential difference, the more diodes needed in the diode ladder.
Because all the diodes are in series, the same current flows through each diode
in the diode ladder. According to Figure 5, the resistance of each diode is the
same. Therefore, this diode ladder can be considered as several identical
resistors connected in series.

#### VCA ---- Voltage-controlled amplifier

A normal amplifier can amplify the input waveform with a constant value. With
the voltage-controlled amplifier, the gain of the input voltage can be varied.
The voltage goes into this circuit and achieves this goal is called the control
voltage. There are two sources of the control voltage----one is the envelope
generator (EG), and the other is the low-frequency oscillator (LFO).

The envelope generator generates a control signal including attack, decay,
sustain, and release, and the voltage-controlled amplifier should apply the
waveform to the audio signal. This can mimic the sound of the instruments in the
real world, the process of the amplitude increases, sustain, and then decrease.

![](media/060f33ec4c0340b85c2cce4cb1718a9f.png)The LFO operates as a normal
voltage-controlled oscillator. The only difference is the frequency of the
signal from the LFO is small compared with that from the VCO. This process aims
to generate a ‘pulse’ sound, where the volume becomes high and low alternatively
with the peak and bottom of the LFO signal. This is also called Tremolo.

Here is the screenshot of the whole circuit and the block diagram:

![](media/f886c7b755ec8afe5a28fc80d6ada6dd.png)The names of the input port are
not very clear. Here is how it works: if the user wants to use LFO as control
voltage, she should connect the LFO to CV directly. If the user wants to use the
output from EG as control voltage, she needs to connect to EG first, and then
connect CV to CV_inv. This will be explained in the Input Stage part. There are
four main stages in the VCA design: the input stage, the amplitude modulation
stage, the reference generating stage for the noise reduction, and the output
stage.

##### Amplitude modulation

This is the main part of the VCA. Here is the screenshot for the circuit:

![](media/e508ef74b0f7160a1a91d9791371f8bb.png)R1 is connected to the
non-inverting input of the opamp and ground. This resister stabilizes the
circuit, and the value of the circuit is not restricted. R6 and that diode
ladder also stabilize the circuit. Also, the diode ladder behaves like the
voltage-controlled resister sometime. The sum of the potential difference across
these 5 components provides the Gate voltage for the JFET. JFET acts as the
voltage-controlled resister as written above. When the Gate voltage changes, the
resistance RDS varies as well. JFET and R2 form a potential divider that splits
the input voltage. The value of R2, R3, R4, and RDS determines the gain. When
the control voltage is 0, RDS remains open-circuit, and the gain of the circuit
is minimized where the Avmin = -R4/(R2+R3). For this JFET, the lower the
voltage, the lower RDS is, so as the control voltage decreases, RDS decreases,
and the gain increases. Here, the gain becomes Av = -R4/(R2+R3//RDS). Also, for
this circuit, because of the parasitic capacitance in the JFET, J1, and R2 forms
a low pass filter, which means there will be an upper limit for the frequency of
the input signal.

![](media/cb189871a5af618212f0c695fa359e84.png)

According to the data provided by LTspice, the parasitic capacitance of this
JFET is very low, about 1p, so the corner frequency is around 3.2MHz which is
much higher than the signal generated by the VCO. Thus, the non-ideal
characteristic will not limit the performance of this voltage-controlled
amplifier.

##### Input stage

![](media/cd5acc584ab2a4e06f3412a0f7c02852.png)This input stage is designed
specifically for the input from the envelope generator. It is simply an
inverting amplifier. This input stage aims to invert the EG signal before
connected to the amplitude modulation stage.

![](media/4c2b4b90de227e2d096f71f86f2dd46c.png)Initially, there is no such input
stage, but the result was unexpected. Here is the result before including this
input stage. It looks like the sine wave grows along the edge of an upside-down
envelope instead of being amplitude modulated. In the amplification stage, the
JFET operates normally with the negative voltage, but the voltage of the
Envelope is positive. As a result, the voltage_controlled resistor does not work
as expected. Hence, before feeding the EG signal into the AM stage, an inverting
amplifier is required to invert the EG signal to the negative voltage region to
make sure the JFET stays in the working region.

![](media/a0b748d49301084852ee995cfadcd9f3.png)After including the input
inverting amplifier into the circuit, the control voltage stays in the negative
region, so it can control the JFET as expected.

![](media/bc5dc197b3423c6f35a7fcc20d62196e.png)Also, the result looks like an
envelope-shaped sine wave, but with much noise and small amplitude (left). The
amplitude of the noise is 40mVp-p and that of the peak signal is around 130mV,
which is only 3 times greater than the noise. When listening to the result, the
sound is unclear and weak. When zooming in the waveform(right), a non-distorted
sine wave shows that the main function of this circuit is completed. Next, more
work needs to be done to make the output with less noise.

![](media/ec3ddcdfd82fadaefcd05e21fb1150f7.png)

##### Noise reduction

The plots from the above section show that even when the EG signal stays at 0
Volt, there will still be some moderate gain for the input, which is unwanted.
To reduce the noise, several transistors with different Vt have been tried, but
none of them can reduce the noise into an acceptable amplitude. Therefore, an
additional circuit is required to reduce the noise.

![](media/e2614bb45f5f9a3ea0559da85ca7e602.png)Recall the content of CMRR from
the transistor-level design that the opamp can reduce the common-mode signal,
the noise, and amplify the differential part, so a reference circuit is added to
the VCA. Here is the screenshot for the circuit. It looks much like the
amplitude modulation circuit, and the only difference is that the control
voltage is always connected to the ground. Hence, at the output of the opamp, a
signal identical to the unwanted noise is generated. Then, with this reference
signal, further processing can be done with another opamp which can not only
reduce the noise but provide with desired gain.

##### Increase gain & output stage

![](media/99de2519b4f5ff27d06cbcce0a97b723.png)![](media/877e8dfd48c9d67053447b63022ffe5d.png)With
the original signal connected to the non-inverting input and the reference
signal to the inverting input, the unwanted noise shall be reduced. Also,
because the input signal has been inverted in the previous stage, it can be
inverted back with this configuration. Then, the resistors are set to provide
high gain and prevent clipping, so 100k and 1k have been selected. Afterward, to
minimize the output impedance, a class A-B output stage is added to the end of
the circuit. With this configuration, the 8 loudspeaker can be driven. Here is
the result of the final output. the shape of the Envelope is very clear on the
waveform. Measured with the cursor, the noise stays at 40mVp-p and the peak
reaches 9.8V. Compared with the previous result, this is more desirable.

![](media/0357e52b3b3cc729fbc206513e0635f0.png)

##### Tremolo

![](media/663d1ade55b0b55615fc141804ab806d.png)Unlike the vibrato, which is
frequency modulation, tremolo is a type of amplitude modulation that uses the
amplifier to turn the sound wave up and down regularly. This is always
controlled by LFO. If the user wants to use LFO as the control voltage, she
should directly connect the output of LFO to CV.

![](media/f8127d914a5e68e3887bc6a2bdf26c35.png)It is expected that when the LFO
signal is negative, the JFET will conduct, and the gain will increase; when the
LFO signal is positive, the JFET will become open circuit, and the gain will
decrease. Here are three screenshots of the waveform being controlled by a sine
wave, a square wave, and a Triangle wave respectively.

![](media/34b005e102076868794ba883cb2db72c.png)The amplitude of the output
shifts between high gain and very low gain, and it sounds like a telephone
ringer. Although the amplitude changes significantly, the frequency of the
signal remains constant. Therefore, tremolo only changes the amplitude but does
not affect the frequency.

#### VCF ---- Voltage-controlled filter

![](media/09d906dcdabda13a2c97f96f30015125.jpeg)![C:\\Users\\yyk20\\AppData\\Local\\Microsoft\\Windows\\INetCache\\Content.MSO\\55005F97.tmp](media/31f132f46c86ee4eea58070efc9a13d6.png)RC
first-order filter is a very basic filter. The order of resistor and capacitor
determines whether it is a low pass filter or a high pass filter, and the
capacitance and resistance set the corner frequency of the filter. When using a
music synthesiser, users use the filter to modulate the sound. The corner
frequency of this circuit is .Different corner frequency applied to the same
input signal generates various outputs. However, it is impossible to place lots
of filters that cover each corner frequency, so voltage-controlled resistors are
used in the circuit. Here is the screenshot of the circuit and its symbol.

![](media/b55c1c6831156550f73ba3191b5ec959.png)There are 6 main blocks in the
filter design, five are shown on the picture, and the other one is the input
stage. It is outside this circuit. Because all signals should go through the
input stage before entering LP, HP, and BP, it is more user-friendly to put the
input circuit independent of the filter block. The diode operates linearly only
with small ac voltage, and if the amplitude of the input signal is too large,
the result will be distorted seriously. Therefore, the input stage is designed
to reduce the amplitude of the input signal. The block located at the
bottom-left corner sums up the control voltage which controls the corner
frequency. User can manually control the cut off frequency with a potentiometer,
and there is another port for a control signal that generated by LFO and EG.
Users can control the effectiveness of the control voltage by swiping the other
potentiometer. The center of the VCF is the filtering block which contains the
diode ladder (D1 to D8) and some capacitors. The diode ladder behaves as VCR,
and these resistors form different types of filters with capacitors, C3, C4, and
C5. A differential pair is under the filtering block. The base of one of the
transistors is connected to the control voltage. When the control voltage
changes, the potential difference between the collectors changes. As a result,
the resistance of the diode ladder varied by the changing forward bias voltage,
so the corner frequency of the filters formed by the diodes and the capacitor
shifts. At the top right corner, there is a resonance-control block. It is
simply an amplifier, and the gain is controlled by one potentiometer. By swiping
the potentiometer, a different quality factor can be chosen by users, the higher
resistance, the higher the quality factor. The last part is the output stage
which is also an inverting amplifier. The gain of the inverting amplifier can be
varied by the potentiometer.

##### Low pass

![Diodes in place of R1](media/7582d4b4ce9d6a7283f5756048ab567f.png)The diagram
on the left explains how the voltage-controlled low-pass filter works. The DC
voltage source provides forward bias voltage for the diode ladder. After setting
up the dc voltage source, the resistance of the diode ladder is fixed. Then, the
diode ladder and the capacitor C1 form a low pass filter. Afterward, the input
signal enters the filter, and the filtered value can be detected at the output
port.

![](media/c9830dedcfb3476565027ed7ec786b96.jpeg)Although the circuit is more
complicated, the working principle remains the same. The signal from the LP port
passes through a voltage-controlled resistor first and then goes to the
capacitor, so they form a low pass filter. As the control voltage changes, the
base voltage of Q1 varied. The forward bias voltage over the diode ladder
changes, and, as a result, the resistance of the diode ladder changes, and the
cut off frequency changes. Other blocks of this circuit have been explained in
other stages.

All the potentiometers in this circuit use the parameter method so that users
can modify the value in the symbol instead of going to the basic circuit. This
is user-friendly.

Here is the demo of the circuit when the input is connected to the LP port. All
the tests use the .step param method, so the effect of each potentiometer can be
demonstrated clearly.

1.  **Adjust cut off frequency**

it shows that as the control voltage increases, the corner frequency increases.
This result is expected because the increase in the control voltage will result
in the rise of the forward bias voltage for the diode ladder. Consequently, the
resistance of the diode decreases. According to the basic circuit above, the
reduction in the resistance shifts the corner frequency to right.

![](media/0e752440eda32c049a28b1f91fce5414.png)

1.  **Adjust the quality factor**

The resonance is controlled by the potentiometer. When the resistance of the
potentiometer increases, the gain for the resonance amplifier increases
consequently. In the simulation, the peak of the resonance becomes more obvious
as the resistance of the resonance resistor increases. Also, there is a small
vertical shift for the curve which means that when adjusting the resonance
resistor, the gain will slightly change. In conclusion, the quality factor is
directly proportional to the resistance of the resonance resistor.

![](media/af8539c61fdec6e6b9043c469259cbf0.png)

1.  **Adjust gain**

There is an inverting amplifier at the output stage. Higher Gain resistance
provides a higher gain. This simulation shows that as the resonance resistance
increases the gain of the whole filter circuit rises.

![](media/ffa83544ed432276c4cde5488a9f3d39.png)<https://www.experimentalistsanonymous.com/ve3wwg/lib/exe/detail.php?id=diode_ladders&media=lp_diode_filter.png>

##### High pass

![C:\\Users\\yyk20\\AppData\\Local\\Microsoft\\Windows\\INetCache\\Content.MSO\\A69C735A.tmp](media/ff47a0fefb5fdb17de064bb3c3d9e5e7.png)The
only difference between the High pass filter and low pass filter is the order of
the components. If the input signal passes through the capacitor first and then
the resistor, the filtered signal will be detected between these two components
which are the Vout shown in the picture. In this voltage-controlled filter, when
it is in the high pass mode, the signal reaches the capacitor C4 first and then
the diode ladder, which builds a high pass filter. The corner frequency is
determined by the resistance of the diodes.

![](media/48b993f77a5da9c1e0b86c1773469896.jpeg)The picture on the left
demonstrates how the Alternating Current flows in this VCF when the input is
connected to HP.

Here is the demo of the effects when users adjusting the potentiometers.

1.  **Adjust the corner frequency**

The corner frequency resistor shifts curve horizontally.

![](media/96b45251204d1eebc51e4164f19e7ae6.png)

1.  **Adjust the quality factor**

The resonance around the corner frequency is more obvious when ramping up the
resonance resistor. Also, the curve shifts vertically a little with different
resistance. Hence, the resonance not only affects the quality factor but also
determines the gain

![](media/af003f012fd62fda3d73508a5afb86f8.png)

1.  **Adjust the gain**

The curve shifts vertically with different gain resistance.

![](media/4193aae17b52a42e679840835db8a8c2.png)

##### Band pass

An ideal bandpass filter allows the signal within a frequency domain to pass. It
is built with a low pass filter in series with a high pass filter. The low pass
filter sets the upper limit for the cut off frequency, and the high pass filter
sets the lower limit. In this circuit, there is just one corner frequency. In
other words, it just simply allows the frequency near the corner frequency to
pass. ![](media/cef64afdfcb6882f0b0f8fe80ec6bb47.jpeg)in the circuit, the
resistance of the diode is settled, so the cut off frequency is fixed. The
signal from BP enters one high pass filter and then the low pass filter.
Afterward, only the signal with a frequency near the cut off frequency can pass
the filter.

Here is the demo of the effects when users adjusting the potentiometers when the
input signal is connected to the BP.

1.  **Adjust the cut off frequency**

The cut-off frequency resistor shifts the curve horizontally.

![](media/756af51111ec6c11746a1eadef2e8d53.png)

1.  **Adjust the quality factor**

When ramping up the resonance resistor, the quality factor increases as a
result.

![](media/c17e5a487ace52c4af9ff589e14b8cc7.png)

1.  **Adjust the gain**

The gain of the circuit changes along with the Gain resistor.

![](media/c30bd40c073e3919521e35b60b42c948.png)

##### Vibrato

![](media/e39ff638f514a5cc805bff84af777ed4.png)![](media/e1c6368b8edd37df9fcfedeee8202839.png)Vibrato
is a type of frequency modulation. It is achieved by LFO and VCF. When the
control voltage is not a constant dc, the corner frequency of the circuit
changes constantly. As a result, the gain for the signal against time is not
unchanged. Also, to achieve vibrato, the resonance resistor should be high
because this part determines whether the frequency is going to change. If the
quality factor is small, the waveform will just oscillate along with the input
control voltage instead of varying in
![](media/a8b0186eeae731c36fd27594bd24b249.png)frequency. after setting up
suitable value for resistors, vibrato is observed at the output port. Although
there is a small change in the amplitude, the main difference is that the
frequency of the wave becomes high and low alternatively against time instead of
being a constant value. When the wave from LFO goes up, the frequency of the
signal increases; as the signal from LFO decreases from peak to bottom, the
frequency being observed at the output reduced significantly. Afterward, a .wav
file was generated, and it sounds like a siren. Also, with a higher frequency
control signal from LFO, it sounds more like the blaster gun in Star Wars.

#### Mixer

This block of the analogue synthesiser is used to mix different sounds,
therefore make it monophonic or polyphonic. The summing amplifier is the heart
of the design, as taught in the lab in the last Aunterm term, we have already
listened to the sound that mixed by the summing amplifier during labs in Autumn
term.

Mixer can be used as the last block of the sysnthesiser, which means it also
needs to need to drive the loudspeaker with 8Ω resistance. Therefore, a class AB
amplifier is used to drive the speaker at the output of the summing amplifier.
Same as the VCA output stage.

![电脑的屏幕 描述已自动生成](media/e3e4b3cc122f1736c9c998e091c1f42c.png)

### Final connection and test results

#### EG+VCA+VCO

Before this part, there was just one VCA and EG in the circuit, and all the
notes generated by the VCO was planned to feed into that single VCA. However,
the limitation of that circuit design is that only one note can be processed at
once, so polyphonic cannot be achieved. Also, if the EG and VCO are controlled
by the PWL directly, when the key is released, there will be no wave generated
from the VCO. This circuit should be able to mimic the sound of release, the
process of the sound faded after users loosen the key, but, with this design,
the release becomes an abrupt stop.
![](media/9f83c7d98704605762cd6bce05c782fe.png)

The solution is to add more EGs and VCAs and move them into original VCO blocks.
The screenshot above shows how one At this moment, the VCO is always on while
users using this music synthesiser no matter whether she pressed this key or
not. In a VCO for one note, there are four VCAs and one EG. Four individual VCAs
are connected to the sine wave, square wave, triangular wave, and sawtooth wave
respectively and controlled by the EG. With this design, users’ actions will be
responded by the EG instead of VCO itself. When the key is not pressed, the
control voltage from EG to VCA stays at 0, so there will be no output from the
VCAs. When the key is pressed, the signal enters the EG, and the EG generates a
corresponding contour signal. Then, the VCA applies amplitude modulation to the
input signal. Afterward, the outputs of the VCAs are connected to a mixer which
superposes these waves and produces polyphonic sound.

![图片包含 监控, 物体, 屏幕, 游戏机
描述已自动生成](media/12c7b77986fe1d86c226a2610281aeb4.png)

The circuit showed above can produce the sound of the first note in the C major
scale. We have six other circuits similar to this circuit, but with different
frequencies to fully produce the 7 notes on C major scale.

#### Final design

After finishing the design and building all the blocks, revisit the high-level
design to make all blocks connect, blocks can be connected to make the final
synthesiser.

According to the block diagrams in the high-level design section. The circuit of
the synthesiser is shown below.

![](media/dd95883b6a7cbe3abbac3957e8756b12.png)

7 PWL voltage sources represent 7 different keys on the keyboard. The wave comes
out of the mixer is connected to the VCF to shape the waveform to make it sound
better. The sine output of the LFO is also connected to the VCA to make a
tremolo effect.

There is a capacitor between LFO and VCA to make sure only the AC signal passes
into the VCA from LFO.

This only one combination of the connection, there are multiple selections for
the circuit.

#### Users’ options

-   Users have a lot of options to change the sound wave

-   VCF, LFO, and VCA, all can be used to modify the wave.

-   There are several combinations for the user to alter the amplitude,
    frequency, and shape of the wave.

-   The knobs on a real synthesiser cannot be represented in LTspice. To make
    the circuit more convenient for the user, multiple potentiometers are used
    to replace the resistors in the circuit.

-   However, the control voltage input in VCF and VCA can only be changed by
    deleting the lines and reconnected to other input.

#### Simulation time

Each block in the final design represents an integrated circuit for each part.
The simulation time will be very long in LTspice.

The complexity of this final design grows super-linearly with the number of
nodes when we connected the blocks into one final circuit.

-   A solution to this will be to simulate the circuit block by block, this will
    reduce the number of nodes LTspice simulate.

-   The output of the first block is being exported to a wave file.

-   This wave file can be used as input for the second block, this can be done
    by creating a voltage source, setting it as a PWL type linked to the wave
    file.

-   All the blocks have an inverting amplifier or a voltage follower at the end
    of the circuit, therefore it will not be affected by other parts of the
    block.

# Project planning and management

## **Organization**

The project management was completed right after the high-level design.

Before any further detailed design works begin, the roles of different team
members were decided for each team member.

According to each member’s ability, we have three different roles.

Yingkai Yang is the Project manager, he helps us with the time management and
makes sure that we are on the right track. The discussions were all held by him
and the efficiency is very high.

Ziheng Qi is mainly focused on documenting the process of our design, and help
bring the detailed part of the design together.

Songyu Huang is focused more on detailed circuits design and communicates with
other group members to solve detailed circuit problems.

The chart below shows tasks that needed to be completed

![](media/c082520fb548f61c7163c110b3c5b2ea.png)

All three members have a specific part of the detailed design.

We first breakdown the structure of the project and the things that we have to
complete in the high-level design

The table below shows which part of the circuit

| Group Member     | Detailed circuit blocks                                                |
|------------------|------------------------------------------------------------------------|
| Songyu Huang     | Envelope Generator, part of Voltage-controlled Amplifier and Mixer     |
| **Ziheng Qi**    | **Voltage-controlled oscillator and Low-frequency oscillator**         |
| **Yingkai Yang** | **Voltage-controlled filter and part of voltage-controlled Amplifier** |

## **Meeting structure and time management**

Microsoft teams offers good stability when sharing screens, a group in Microsoft
teams was created so that communications and sharing screens between group
members can be convenient. The sharing screens functionality also allows us to
solve problems together. There are no time limitations between three of us
during the discussion, as we all live in the same time zone and can have higher
efficiency.

The schedule for each week's discussion was created by Yingkai Yang.

We held the discussions at least 4 times a week on Microsoft teams. The
different part of the whole circuits has different problems, our time spent on
each block is not exactly we planned. The plan is constantly changing.

We used a final Gantt chart to show the final time arrangement of our project.

![手机屏幕截图 描述已自动生成](media/acd77876e8ddbe2f61824bcff975d891.png)

Some part of this management was done at the same time.

# Evaluation

1.  **Limitations in the triangular wave generator**

The method used to generate the triangular wave is designed for a square wave
with a 50% duty cycle. However, both the duty cycle and the frequency of the
signal depending on the values of the resistors. Also, in this circuit design,
the precision of the frequency of the wave is prioritized, so for some of the
notes, the duty cycle of the square wave may be slightly higher or lower than
the exact 50%. As a result, the triangular wave generated from a square wave
with a high or low duty cycle will be converted into a wave with moderate
distortion. The triangular wave may look like the sawtooth wave. Hence, this
design of the triangular wave generator circuit limits the variety and quality
of sounds that this synthesizer be able to produce.

1.  **Advantages and drawbacks of using Wien Bridge as the sinusoidal** **wave
    generator**

Compared with using 555 timers and filters to generate a sine wave, the power
consumption is much lower with the Wien bridge. When using the 555 timers and
filters, it is very hard to find a balance between the efficiency of the power
and the quality of the sine wave. The reason is that the high-quality sine wave
can only be generated with more than three passive RC filters where the
amplitude of the output is only one-tenth of the original square wave.

The oscillator circuit used to generate a sinusoid wave is extremely unstable.
The oscillator will be sustainable only if the product of inverting and
noninverting gains is 1. Therefore, the ratio of the resistance of R1 and R2,
which are the resistor that forms the inverting amplifier configuration, must
equal to 2. However, in reality, it is hard to keep R1/R2 always equal to 2. A
small change in temperature or little error from the manufacturer of the
resistors may cause the sine wave generator to be unstable. Once the ratio
between these two resistors does not equal to 2, the Wien bridge begins to
oscillate or be clipping. Also, Wien bridge is not suitable to generate waves
that last for a long time. The amplitude of the wave generated by the Wien
bridge decreases over time. If the users want to generate a very long continuous
wave with Wien bridge, the amplitude may be insufficient after in extreme cases.
Fortunately, this Wien bridge can last for long enough before decaying
significantly.

1.  **The unwanted connection between resonance resistor and the gain in**
    **VCF.**

When adjusting the quality factor with the resonance potentiometer, the gain of
the circuit changed slightly. This phenomenon can be observed in the screenshots
in the VCF part. This effect of the resonance resistor is unwanted but
inevitable because the resonance part in the VCF is a non-inverting amplifier
itself. The result is when the users want to adjust the quality factor only, she
may need to swipe the gain resistor to keep other of the wave remains the same.

1.  **Noise from the VCA and EG**

In the release stage, the amplitude of the output of EG is supposed to drop to
0V. However, the contour signal from the EG does not go back to 0 once
activated. This won’t have a huge effect on a single note because the amplitude
of each note is much higher than the amplitude of the noise. However, with more
keys being pressed, the noises caused by each note overlap, but the peak
amplitude of each useful signal remains the same. As a result, the effect of the
noise becomes more and more significant, and the quality of the sound is not
satisfied.

There is one solution that alleviates this drawback. Because the property of one
transistor used in the EG prevents the voltage from going back to zero, one dc
offset is added to the EG. With this dc offset, the signal from EG drops to a
voltage level that closer to 0V. Even so, the noise could not be removed
completely.

1.  **Some additional power supply used in the circuit**

Besides the 7 PWL voltage sources that mimic 7 keys and the power rail, there is
some additional voltage source used in the circuit. The reason is that when
using a potential divider to get the desired voltage, it always takes a much
longer time to simulate the result than using a voltage source directly.
Therefore, to speed up the simulation, some of the potential dividers are
replaced by some voltage sources. When building the music synthesiser in the
real world, all the additional voltage sources can be substituted with potential
dividers. Therefore, the cost of this music synthesiser is not higher even there
are some voltage sources in the circuit diagram.

1.  **Too many VCA integrated into the VCO.**

28 VCAs are applied to VCOs as far. This is because, in the LTspice, no
component can behave as a nob which selects the waveform. To prevent re-wiring
each time, excessive VCAs are used. In reality, there will be a nob in the
control block with which users can select the desired waveform. As a result,
only 7 VCAs are required.

1.  **Too many opamps are used in the circuit**

Compared with transistors, opamps have more functionality but costs more. This
circuit uses too many opamps, so the cost is not desirable. In the future
design, more transistors should be used if they can achieve the same goal as a
full opamp does.

## Further improvement

This circuit can only generate audio frequency tones for the 7 notes in C major
in one octave. Whenever it goes up or down one octave, the frequency of each
corresponding note doubles or halves. In the future, more notes can be added
easily with an additional circuit shown below.
![](media/cb1090b1bb39fca04d8703b4be1914da.png)

This circuit contains some D-flip flops with their active low outputs connected
to the inputs. for each DFF, the frequency of the output is halved compared with
the former DFF. Therefore, if one node from the highest octave is fed into the
first DFF, the corresponding nodes from other octaves will be generated from
each output.

## Power consumption

To calculate the power consumption of our design. Current flows across the 12V
voltage source are measured. Then the product of current and voltage is power.
As the voltage source is a constant value, the current reflects the power
consumption. We did several investigations to find out the power consumption of
our design while using different functionality.

Firstly, we want to find out how the number of notes affects power consumption.
According to Pic 1 and pic2, the red line is the PWL signal the green line is
the current flows across the voltage source. They are identical for one note and
seven notes. It proves that power consumption is independent of the number of
notes connected to the mixer.

That is what we expected to see. because oscillators of seven notes never turned
off. what we controlled is the waveform of the envelope generator. Therefore no
matter how many notes are used, all blocks of VCO will keep on operating.

![](media/9e52cbbdca7e4152dea2816b3066d6c3.png)

Figure1one note

![](media/22b22c469964c0f76f9a3ae19a91ec87.png)

Figure2 seven notes

![](media/cb71909217bdcf26d6fc7cfe3cca3c93.png)

Figure3 PWL one pulse

Secondly, we were also interested in the relationship between PWL and power
consumption. According to Pic 2 pic 3., we modified the PWL signal that controls
note DO and close other notes. The result indicates that power consumption is
also independent of PWL. In this test, The power is about 22W.

![](media/c0c20a23b2ee0aa629e7e72a00d984d9.png)

Figure4 without VCA

Thirdly, we removed the final VCA and kept other parts unchanged. Comparing Pic2
and pic4 the current reduced to about 1.5A. After removing the final VCA
circuit, the power consumption reduces significantly from 22W to 18W.

## Bills of material

VCA \* 29 (4\*7+1)

| Component    | Quantity |
|--------------|----------|
| Opamp LT1013 | 4        |
| Diode 1N914  | 8        |
| Resistor     | 18       |
| JFET J201    | 2        |
| NPN 2N2222   | 2        |
| PNP 2N2907   | 2        |

EG \* 7

| Opamp LT1013 | 3  |
|--------------|----|
| Diode 1N914  | 4  |
| 555 Timer    | 1  |
| NPN 2N2222   | 2  |
| Resistor     | 21 |
| Capacitor    | 4  |

VCO \* 7

| 555 Timer    | 1  |
|--------------|----|
| Opamp LT1013 | 11 |
| Capacitor    | 4  |
| Resistor     | 36 |
| PNP 3906     | 2  |
| NPN 3904     | 1  |

VCF \* 1

| Resistor and potentiometer  | 24 |
|-----------------------------|----|
| NPN 2N2222                  | 2  |
| Opamp TL072                 | 2  |
| Diode 1N914                 | 10 |
| Capacitor                   | 7  |

LFO \* 1

| Resistor and potentiometer  | 27 |
|-----------------------------|----|
| Capacitor                   | 2  |
| NPN 3904                    | 3  |
| Opamp LT1013                | 3  |

Mixer \* 1

| Resistor     | 8 |
|--------------|---|
| Opamp LT1013 | 1 |

Total cost

| Component        | Quantity  | Price  | Total price  | Reference                   |
|------------------|-----------|--------|--------------|-----------------------------|
| Resistor (1/2W)  | 980       | ￡0.02 | ￡19.6       | **Alibaba, Taobao, Amazon** |
| Capacitor        | 65        | ￡0.02 | ￡1.2        |                             |
| 555 Timer        | 14        | ￡0.06 | ￡0.84       |                             |
| Opamp LT1013     | 218       | ￡0.35 | ￡76.3       |                             |
| Opamp TL072      | 2         | ￡0.30 | ￡0.60       |                             |
| Transistor       | 156       | ￡0.05 | ￡7.8        |                             |
| Diode 1N914      | 270       | ￡0.02 | ￡5.4        |                             |
| JFET J201        | 58        | ￡0.15 | ￡8.7        |                             |
| Total            | 1763      |        | ￡120.44     |                             |

## Effects of High Tolerance components

Here are some fragile parts that may be greatly affected by the tolerance of
manufacturers.

1.  Stability of the Wien Bridge Sine wave generator

The Stability of the Wien Bridge is ensured by the ratio between two resisters.
It is stable only when the ratio is exact 2. However, in the real world, it is
very likely that the ratio is not exact 2 either caused by the error from
manufacturers or changes in temperatures. As a result, it may become unstable.

1.  The corner frequency of the Voltage controller filter

The corner frequency of VCF is determined by the diodes and capacitors. The high
tolerance in components causes different corner frequencies between music
synthesisers.

1.  The gain for the output stage

The resistance sets the gain of the circuit. With tolerance in resistors, the
gain may be different between music synthesisers even when the users turn the
nob to the same orientation.

1.  Frequency of wave for each note

With high tolerance components, the frequency of waves for each note may not
equal to the theoretical value. Hence, this circuit may require careful tuning
before using it.

# Conclusions

From initial planning to final connections and tests, it takes about one month
to complete this music synthesiser project. Up to now, this music synthesiser is
quite functional, including generating notes with different frequency and
waveform, mixing notes from different oscillators together to form polyphonic,
manipulating the waveform with LFO and EG that creates tremolo and vibrato, etc.

While participating in this project, we learned a lot from both academic and
non-academic aspects. On one hand, this project provides a comprehensive
revision for the knowledge from this academic year that we have a much better
and deeper understanding of those contents. On the other hand, we learned how to
communicate and cooperate with teammates and how to divide a big project into
small tasks. What’s more, this project is inspired as we realize that knowledge
can be applied to solve real-world problems. It also encourages us to think
about how it works in addition to how to use it when facing a new device.

# Reference

-   \#105: More Circuit Fun: Simple 3 transistor sawtooth generator /
    oscillator. (2013). *w2aew*. Available at:
    https://www.youtube.com/watch?v=2a1I1X3RV0g [Accessed 13 Jun. 2020].

-   Basic Electronics Tutorials. (2013). *Wien Bridge Oscillator Tutorial and
    Theory*. [online] Available at:
    https://www.electronics-tutorials.ws/oscillator/wien_bridge.html.

-   DIY Analog Synthesizer Part 2: The Voltage Controlled Amplifier (VCA)/Low
    Frequency Oscillator (LFO (2019). *DIY Analog Synthesizer Part 2: The
    Voltage Controlled Amplifier (VCA)/Low Frequency Oscillator (LFO)*. *How to
    Mechatronics*. Available at: https://youtu.be/OHbvecDEqsI [Accessed 13 Jun.
    2020].

-   DIY Synth Design Tutorial Series - 004: Analog Envelope Generator and
    Amplifier. (2019). *the.room.dis.connect*. Available at:
    https://www.youtube.com/watch?v=gevD3INR1kk&t=1368s [Accessed 12 Jun. 2020].

-   Electron Coaxing Techniques & Notes (2012). *diode_ladders*. [online]
    Electron Coaxing Techniques & Notes. Available at:
    https://www.experimentalistsanonymous.com/ve3wwg/doku.php?id=diode_ladders
    [Accessed 12 Jun. 2020].

-   How a 555 Timer IC Works. (2018). *YouTube*. Available at:
    https://www.youtube.com/watch?v=i0SNb__dkYI [Accessed 13 Jun. 2020].

-   Hua, Z. (2016). *压控增益放大器(LM307)*. [online] tech.hqew.com. Available
    at: https://tech.hqew.com/circuit_1482055 [Accessed 8 Jun. 2020].

-   NA (2015). *Resistance of a Diode*. [online] Circuit Globe. Available at:
    https://circuitglobe.com/resistance-of-a-diode.html [Accessed 12 Jun. 2020].

-   NA (n.d.). *FabFilter One Help - Envelope generator*. [online]
    www.fabfilter.com. Available at:
    https://www.fabfilter.com/help/one/using/envelopegenerator [Accessed 12 Jun.
    2020a].

-   NA (n.d.). *How to Build a Ramp Generator with Transistors*. [online]
    www.learningaboutelectronics.com/. Available at:
    http://www.learningaboutelectronics.com/Articles/Ramp-generator-circuit-with-transistors.php
    [Accessed 10 Jun. 2020b].

-   Quan, R. (2017). *EDN - A guide to using FETs for voltage controlled
    circuits, Part 1*. [online] www.EDN.com. Available at:
    https://www.edn.com/a-guide-to-using-fets-for-voltage-controlled-circuits-part-1
    [Accessed 12 Jun. 2020].

-   Rise, S. (n.d.). *Voltage-Controlled Amplifier (VCA)*. [online]
    synthesizeracademy.com. Available at:
    http://synthesizeracademy.com/voltage-controlled-amplifier-vca/ [Accessed 8
    Jun. 2020a].

-   Rise, S. (n.d.). *Voltage-Controlled Filter (VCF) \| The Synthesizer
    Academy*. [online] synthesizeracademy.com. Available at:
    http://synthesizeracademy.com/voltage-controlled-filter-vcf/ [Accessed 12
    Jun. 2020b].

-   Yi, S. (2019). *解读模拟合成器（十）加法合成（下）-ABLETIVE电子音乐社区*.
    [online] www.abletive.com. Available at:
    http://www.abletive.com/tech/detail/970 [Accessed 12 Jun. 2020].

# Appendix

![](media/cb189871a5af618212f0c695fa359e84.png)

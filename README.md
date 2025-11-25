# FREQUENCY-DIVISION-MULTIPLEXING

## AIM
To implement Frequency Division Multiplexing (FDM) for six different message signals using Scilab, generate the multiplexed signal, and perform demultiplexing to recover all the original message signals. The experiment also includes plotting the message signals, multiplexed signal, and demultiplexed signals.

## APPARATUS REQUIRED

1. Computer System
2. Scilab Software

## ALGORITHM

1. Set sampling frequency, time duration, and time vector.
2. Generate six message signals with different frequencies.
3. Assign six different carrier frequencies.
4. Perform DSB-SC modulation by multiplying each message with its carrier.
5. Add all modulated signals to form the multiplexed FDM signal.
6. For each channel, multiply the multiplexed signal with the same carrier (demodulation).
7. Apply a low-pass filter to extract the recovered message.
8. Plot message signals, multiplexed signal, and recovered s  ignals.

## THEORY

Frequency Division Multiplexing (FDM) is a technique in which multiple message signals are transmitted simultaneously over a single communication channel by assigning each signal a different carrier frequency. Each message modulates its own carrier, and all modulated signals are added to form the multiplexed signal. Since the carrier frequencies are well separated, the signals do not overlap in the frequency domain.

At the receiver, each signal is recovered by multiplying the multiplexed signal with the corresponding carrier (coherent demodulation) and passing it through a low-pass filter to extract the original baseband message. FDM is widely used in radio broadcasting, telephone systems, and cable TV.

## PROGRAM
```
clc; 
clear; 
close;

fs = 50000;
t = 0:1/fs:0.05;

// Slightly changed amplitudes and frequencies
m1 = 1.75*sin(2*%pi*165*t);
m2 = 1.85*sin(2*%pi*175*t);
m3 = 1.95*sin(2*%pi*185*t);
m4 = 2.05*sin(2*%pi*195*t);
m5 = 2.15*sin(2*%pi*205*t);
m6 = 2.25*sin(2*%pi*215*t);

// Slightly changed carrier frequencies
c1 = cos(2*%pi*2100*t);
c2 = cos(2*%pi*4200*t);
c3 = cos(2*%pi*6100*t);
c4 = cos(2*%pi*8200*t);
c5 = cos(2*%pi*10200*t);
c6 = cos(2*%pi*12200*t);

s1 = m1 .* c1;
s2 = m2 .* c2;
s3 = m3 .* c3;
s4 = m4 .* c4;
s5 = m5 .* c5;
s6 = m6 .* c6;

fdm = s1 + s2 + s3 + s4 + s5 + s6;

r1 = fdm .* c1;
r2 = fdm .* c2;
r3 = fdm .* c3;
r4 = fdm .* c4;
r5 = fdm .* c5;
r6 = fdm .* c6;

// Slightly changed cutoff
cutoff_hz = 420;
norm_cutoff = cutoff_hz/(fs/2);

M = 101; 
[h, w] = wfir('lp', M, [norm_cutoff, 0], 'hm', 0);  

d1 = conv(r1, h, 'same');
d2 = conv(r2, h, 'same');
d3 = conv(r3, h, 'same');
d4 = conv(r4, h, 'same');
d5 = conv(r5, h, 'same');
d6 = conv(r6, h, 'same');

d1 = 2 * d1;
d2 = 2 * d2;
d3 = 2 * d3;
d4 = 2 * d4;
d5 = 2 * d5;
d6 = 2 * d6;

figure(1);
subplot(3,2,1); plot(t,m1); title("Message 1");
subplot(3,2,2); plot(t,m2); title("Message 2");
subplot(3,2,3); plot(t,m3); title("Message 3");
subplot(3,2,4); plot(t,m4); title("Message 4");
subplot(3,2,5); plot(t,m5); title("Message 5");
subplot(3,2,6); plot(t,m6); title("Message 6");

figure(2);
plot(t,fdm); title("Multiplexed FDM");

figure(3);
subplot(3,2,1); plot(t,d1); title("Demod 1");
subplot(3,2,2); plot(t,d2); title("Demod 2");
subplot(3,2,3); plot(t,d3); title("Demod 3");
subplot(3,2,4); plot(t,d4); title("Demod 4");
subplot(3,2,5); plot(t,d5); title("Demod 5");
subplot(3,2,6); plot(t,d6); title("Demod 6");


```

## OUTPUT WAVEFORM
<img width="1917" height="878" alt="Screenshot 2025-11-18 212926" src="https://github.com/user-attachments/assets/33402cd7-4abd-439b-919a-dbba0c7dac4b" />

<img width="1919" height="899" alt="Screenshot 2025-11-18 213129" src="https://github.com/user-attachments/assets/5e095c50-cbac-4d04-8fa3-023301301b60" />

<img width="1919" height="869" alt="Screenshot 2025-11-18 213147" src="https://github.com/user-attachments/assets/5622cff0-1d41-4f85-b62d-fc893c6e340b" />




## CALCULATION
![WhatsApp Image 2025-11-22 at 12 33 15 PM](https://github.com/user-attachments/assets/156d0476-6c2d-4323-a3ac-c6a1a96714a5)

![WhatsApp Image 2025-11-22 at 12 33 16 PM](https://github.com/user-attachments/assets/ad96bb96-b9ea-4b14-b8de-abd0b07bcf80)

## RESULT
Six different message signals were generated and modulated using FDM. All modulated signals were added to form a multiplexed FDM signal. Each message was successfully recovered using coherent demodulation followed by low-pass filtering. The plots confirmed accurate multiplexing and demultiplexing.

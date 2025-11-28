# SIMULATION-OF-FREQUENCY-DIVISION-MULTIPLEXING-FDM-AND-DEMULTIPLEXING-USING-SCILAB
AIM:
To write a Scilab program to simulate frequency division multiplexing and demultiplexing for six different frequencies, and verify the demultiplexed outputs correspond to the original signals.

EQUIPMENTS Needed
Computer with Scilab installed

ALGORITHM:
Define six different frequencies to generate six sine wave signals.

Generate the time vector to represent time samples.

Compute six sine signals for each frequency over the time vector.

Frequency Division Multiplexing: sum all six sine signals to make one multiplexed signal.

Frequency Division Demultiplexing: for each frequency, multiply the multiplexed signal by a sine wave of that frequency (mixing), then apply a lowpass filter to extract the baseband (original) signal.

Plot original signals, multiplexed signal, and demultiplexed signals for verification.

PROGRAM:
```
fs = 80000;
t = 0:1/fs:0.035;

m1 = sin(2*%pi*139*t);
m2 = sin(2*%pi*149*t);
m3 = sin(2*%pi*159*t);
m4 = sin(2*%pi*169*t);
m5 = sin(2*%pi*179*t);
m6 = sin(2*%pi*189*t);
                 
fc = [1390 1490 1590 1690 1790 1890];
                 
c1 = cos(2*%pi*fc(1)*t);
c2 = cos(2*%pi*fc(2)*t);
c3 = cos(2*%pi*fc(3)*t);
c4 = cos(2*%pi*fc(4)*t);
c5 = cos(2*%pi*fc(5)*t);
c6 = cos(2*%pi*fc(6)*t);

s1 = m1 .* c1;
s2 = m2 .* c2;
s3 = m3 .* c3;
s4 = m4 .* c4;
s5 = m5 .* c5;
s6 = m6 .* c6;

s = s1 + s2 + s3 + s4 + s5 + s6;

d1 = 2 * s .* c1;
d2 = 2 * s .* c2;
d3 = 2 * s .* c3;
d4 = 2 * s .* c4;
d5 = 2 * s .* c5;
d6 = 2 * s .* c6;

cutoff = 1000; // Hz

function y = fft_lowpass(x, cutoff, fs)
    N = length(x);
    X = fft(x);
    f = (0:N-1)*(fs/N);
    mask = (f <= cutoff) | (f >= fs - cutoff);
    Y = X .* mask;
    y = real(ifft(Y));
endfunction

r1 = fft_lowpass(d1, cutoff, fs);
r2 = fft_lowpass(d2, cutoff, fs);
r3 = fft_lowpass(d3, cutoff, fs);
r4 = fft_lowpass(d4, cutoff, fs);
r5 = fft_lowpass(d5, cutoff, fs);
r6 = fft_lowpass(d6, cutoff, fs);

scf(1);
clf;

subplot(6,3,1);  plot(t, m1);
subplot(6,3,4);  plot(t, m2);
subplot(6,3,7);  plot(t, m3);
subplot(6,3,10); plot(t, m4);
subplot(6,3,13); plot(t, m5);
subplot(6,3,16); plot(t, m6);

subplot(6,3,8);  plot(t, s);

subplot(6,3,3);  plot(t, r1);
subplot(6,3,6);  plot(t, r2);
subplot(6,3,9);  plot(t, r3);
subplot(6,3,12); plot(t, r4);
subplot(6,3,15); plot(t, r5);
subplot(6,3,18); plot(t, r6);

```
GRAPH:
<img width="1919" height="992" alt="image" src="https://github.com/user-attachments/assets/ab07d178-a09d-435c-b28b-9798d83b9c53" />

TABULATION:

RESULTS:
The program successfully simulates FDM and demultiplexing for multiple frequency signals with filtering to recover original signals accurately in Scilab.

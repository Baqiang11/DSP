Project Brief
1 Filtering
An audio signal has been corrupted with a sine wave and high frequency noise. This can be
downloaded from canvas.
• Show and describe all of your measurements in you report.
• Use Matlab or Simulink to show the power spectrum and work out what frequency the
sine wave is,
• Design an FIR or IIR filter that will remove the sine-wave signal.
• Design an FIR or IIR filter that will remove the high frequency noise signal.
• Show the filters remove the noises in
– A Simulink simulation
– Running on the DSP board. You can connect the audio output of the PC to the line
in of the DSP board. You need to ensure that the volume level is not too high so
that the board does not clip the signal.
– Measure the magnitude frequency performance of the filters running on the board
using at least two dierent methods. Comment on the differences.
– Marks are given for selecting and justify methods that will minimise the impact
of the filter on the original sound (by amplitude and phase) as well as running as
efficiently as possible on the board.


2 Sine-wave Detection
Using the DSP sine-wave block, design a model that will turn on the boards LED when, and
only when a 3 kHz sine wave is encountered. (This can be achieved by an FFT and considering
the ratio of the power in the 3Hz band and the reminder of the signal.) Explain, how you
calculate the position of the peak in the FFT data and how it is robust against noise.

3 Envelope Detection
On application of a digitalfilter is an envelope detector. An envelope detector (or peak detector)
takes a (relatively) high-frequency amplitude modulated signal as input and provides an
output, which is the demodulated envelope of the original signal.
![image](https://github.com/user-attachments/assets/7df85b30-51ed-494a-98c3-85b9ac2d278f)

Figure 1: Envelope Example

The yellow line is the original signal, and the blue line is its envelope. An example application
is AM radio, in which the lower frequency audio signal is the blue line, and the yellow line is a
high frequency carrier signal that we wish to remove.
There are lots of methods to achieve this, but we will implement a simple one. It works by
squaring the input signal and sending it through a lowpass filter. In order to maintain the
correct scaling, this method also includes two more operations. In the first operation, you
place a gain of 2 on the signal. Since you are keeping only the lower half of the signal energy,
this gain boosts the final energy to match its original energy. In the second operation, you take
the square root of the signal to reverse the scaling distortion from the input signal squaring
operation.
We need to reduce the sampling frequency, since we don’t want the high frequency. This can
be achieved by adding a decimation filter. In our case we only take every 15 samples. This
needs a low pass filter in front of it to remove aliasing.

![image](https://github.com/user-attachments/assets/f0948dcf-d5df-4bf0-9af3-364b27c525f9)

Figure 2: Model

In Simulink, create a 1 kHz sine-wave and pulse generator that produces a 50/50 duty square
wave. Multiply both signals together to make a signal like that in Figure 1.

![image](https://github.com/user-attachments/assets/69e60d4b-dec5-4233-80e8-d94275c5a141)

Figure 3: Sine wave and pulse generator output

Show this working in Similink only, then transfer to the DSP board and turn on the LED when
the signal is greater than 0.25.
• Note, to decimate by a factor of 15, the sample frame size of the data must be a multiple
of 15.
• The low pass filter has a cut-o frequency of Nyquist frequency/M where M is downsampling ratio (ie 15)

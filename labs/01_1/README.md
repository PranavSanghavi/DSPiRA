# 1.1. Random Signals and Sampling

- [1.1. Random Signals and Sampling](#1-random-signals-and-sampling)
    - [1.1.1. Random Discrete Signals](#11-random-discrete-signals)
    - [1.1.2. Sampling](#12-sampling)
    - [1.1.3. Histograms](#13-histograms)
    - [1.1.4. GnuRadio Companion Example.](#14-gnuradio-companion-example)

<!-- /TOC -->

## 1.1.1. Random Discrete Signals

Random signals are signals where the next value can be though of as chips
drawn from a hat with many many values, where the exact number of chips with those values relative to eachother can be given by an equation, the 'distribution'.  One of the simplest is a uniform random signal, where each value has an equal number of chips.  

In GnuRadio we can create these signals with a 'Random Uniform Source' block.<!-- TOC -->

A very common distribution in nature is the 'gaussian' distribution.  

## 1.1.2. Sampling

Sampling can always be though of as the act of pulling the chips out of the hat, and rounding the value on the chip to the nearest integer. When a real signal is digitized by an analog to digital converter (ADC), every clock cycle, the level of the signal is measured and recorded to the nearest value.

## 1.1.3. Histograms

A histogram is a plot of the number of occurances of the signal that occur between a set of levels chosen.  Plotting the histogram is a way of trying to measure the distribution of an incoming random signal.  

## 1.1.4. GnuRadio Companion Example.  

Create the shown GnuRadio flowgraph.  
![sampling](img/sampling.png) 

Use a random source between -10 and 10.  The random source only creates discrete integer values, so you also need and Int to Float block with a 'scale' which will multiply the incoming signal by the scale value.  

Run the flowgraph, with the scale factor at 1.  What does the time plot look like?  What does the histogram look like?  Now play with the scale factor.  Can the histogram have large gaps? Can you make the histogram look continuous?  What intuition do you gain from this about sampling a 'random' signal?  

Now also try different distribution sources.  Use the "Noise Source" block and set it to a gaussian distribution.  What does the timestream look like?  What about the histogram?

Now again use a cosine input signal as you've used in a previous excercise.  What does the timeseries look like?  The histogram?  A cosine signal is not very random.  What if instead, each measured point in time of the cosine was completely randomized (could also think of using a uniform random signal put through a cosine function)?  Would the histogram look any different?  This would also be a random signal, and has the functional form $$\frac{A}{\sqrt{1-y^2}}$$, which should agree with your histogram.  

## 1.1.5 Make your own gaussian noise block

You are now ready to try to make your own gaussian noise block out of other blocks.  

Create a new flowgraph in grc.
 We'll start by using a just a QLFSR block.  This is a 'linear feedback shift register'  block, which is a very simple way to create 'pseudorandom' noise.  Look [here](https://en.wikipedia.org/wiki/Linear-feedback_shift_register) for more details.  Set the type to float, the degree (how many elements in the shift register) to 32, repeat yes.  Change the seed to any number.  Leave the 'mask' at zero to get an 'optimal' source that wont repeat.  Try using other numbers to compare, 1075838979 is a nice choice for random looking data.  Use a histogram sink and a gui sink to look at the output.  Even though the output is only -1 or 1, without knowing the initial seed and how many cycles have gone by, the answer is random.

 Add a number of these sources together:
 ![gaussian](img/lfsr_noise.png)

 What does the output look like now?  This is one of the simple ways of going from a 'flat' random number to a gaussian white noise.
 
  




[↑ Go to the Top of the Page](#) ......[Next Lab](../02)


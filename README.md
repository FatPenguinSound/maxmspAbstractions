# Max/MSP Abstractions

This repository is a collection of random abstractions for Max and Max/MSP. Feel free to drop me a message if something's not working or if you have any questions. I'm also happy to help design things.

## Distance Calculator
This is a pretty easy one to make yourself, but hey...

This is GenDSP distance calculator. Four inlets -- x1 y1 x2 y2. Outlet is a float. If you need this at signal rate, it's pretty easy to convert.

## DBAP
This set of files implements Distance Based Amplitude panning. It would be super-nice if the control-rate Gen would allow the manipulation of lists... maybe someday.

### DBAP
The DBAP abstraction is reliant on the other abstractions in the folder.

This abstraction does not include speaker weights or variable radii. I might add this in at some point, but it's not something that I use. I've found that taking the inverse and multiplying works more reliably than trying to use the reverse-inlet operators.

The three inlets of the DBAP abstraction are the speaker positions, the object position, and the rolloff number. The R value (third inlet) should be a positive number -- I usually use 3 or 6 depending on the application.

The first inlet feeds a collection, and the panning is in three dimensions; so you will need to feed it four values for each speaker: n x y z. The number (n) of the speakers should start at 1 and not skip any numbers. If you are only working in two dimensions you can just zero the z value. The second inlet is the position of the object to be panned, and just needs three values: x y z.

The oulet of the abstraction spits about the speaker weightings, prefixed by the index of the speaker: n v. You can route the gain scales by index, convert them to signals, and multiply the object by each scaler before sending it to the speakers.

Any input on the first or second inlet triggers calculations, so make sure you have your speaker list and initial object panning set before turning on DSP.

### aCoeffCalc
This abstraction calculates the a coeff for DBAP.

### kCoeffCalc
This abstraction calculates the k coeff for DBAP. There is some additional logic to prevent NaN and inf outputs (replacing them with 0 and 1).

### vCalculator
This abstraction calculates the gain scalars for output.

### distanceCalculator
Calculates distance in three dimensions.

## mspFaderConverter
Convenience abstraction for Max/MSP to convert a slider into a fader.

This abstraction takes a number input from 0. to 1, and returns an amplitude scalar representing a range from -70dB to +12dB.

The 0dB value for the abstraction is 0.80214

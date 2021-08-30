[!][(http://raw.githubusercontent.com/macumbista/benjolin/master/pure_data_benjolin.png)]

*INTRODUCTION*

The Benjolin is a standalone synthesizer designed by Rob Hordijk from the Netherlands in 2009 and available as an open hardware project online. It contains two oscillators (one LFO and one VCO), a voltage controlled filter and a circuit called a “Rungler”, which allows chaotic cross-modulation possibilities between the different parts of the circuit. Hordijk refers to the Benjolin as a circuit which has been “bent by design.”

This Pure Data implementation of the Benjolin was coded by Derek Holzer in SEP-NOV 2016 in Helsinki, after several years of producing customized hardware Benjolins from his Berlin studio. The Pd Benjolin includes some modifications of the original design, including a Looping switch, an external Filter Source and an External Clock Source.

The Pd Benjolin uses anti-aliased oscillators and filters from Mike Moser-Booth’s MMB library and Tom Schouten’s CREB library to avoid some of the usual digital errors and artifacts common in digital emulation of analog synthesis.

*QUICKSTART*

Using the latest Pd, make sure all the necessary libraries are installed using Deken , then open the patch named “benjolin-help.pd”, make sure DSP is turned on in Pd and have fun!

*DEPENDENCIES*

The Pd Benjolin requires a few external libraries to function correctly. It was designed originally using Pure Data Extended, but since that is no longer supported, you should  install the “Vanilla” version of Pure Data and add the external libraries yourself with Deken, the built-in external manager.

—Pure Data “Vanilla”
—Must be combined with the libraries listed below to run the Pd Benjolin
—https://puredata.info/downloads/pure-data

—MMB library by Mike Moser-Booth
—A copy of this has been provided in the Pd Benjolin Git
—https://puredata.info/downloads/mmb

Use Deken (Help --> Find Externals) to install:

–jmmmp

–hexloader

–iemmatrix

–maxlib

–zexy

–creb

–flatgui

–ggee

–list-abs

*USAGE*

—CONTROLS

—O1 FRQ: manual frequency control of Oscillator 1 (VCO)

—O1 RUN: amount of “Rungler” control voltage sent to Oscillator 1 (VCO)

—O2 FRQ: manual frequency control of Oscillator 2 (LFO/Clock)

—O2 RUN: amount of “Rungler” control voltage sent to Oscillator 2 (LFO/Clock)

—FIL FRQ: manual frequency control of the Voltage Controlled Filter

—FIL RES: manual resonance control of the Voltage Controlled Filter

—FIL RUN: amount of “Rungler” control voltage sent to the Voltage Controlled Filter

—FIL SWP: amount of Oscillator 2 triangle wave control voltage sent to the Voltage Controlled Filter

—PATCHBAY SIGNAL OUTPUTS

The matrix patchbay of the Pure Data Benjolin has 8 outputs, three control voltage (CV) inputs and a main output. Some combinations (having an oscillator modulate its own frequency) don’t make a lot of sense and have been marked with an “X”, but are still possible to try if you wish.

—O1 TRI: Triangle wave output of Oscillator 1

—O1 PLS: Pulse wave output of Oscillator 1

—O2 TRI: Triangle wave output of Oscillator 2

—O2 PLS: Pulse wave output of Oscillator 2

—PWM: Pulse-width-modulated combination of Oscillator 1 and 2

—RUN: the “Rungler” produces a chaotic, stepped wave output which is clocked by Oscillator 2 (used as control information, so not anti-aliased!)

—XOR: The XOR (exclusive/or logic operation) of the pulse waves of Oscillators 1 and 2 (used as control information, so not anti-aliased!)

—FIL: output of the Voltage Controlled Filter

—PATCHBAY and EXTERNAL CONTROL INPUTS

—O1 CV: Control Voltage Input to Oscillator 1

—O2 CV: Control Voltage Input to Oscillator 2

—FIL CV: : Control Voltage Input to the Voltage Controlled Filter

*DETAILS*

Please see the “benjolin-help.pd” file for specific info on creating the instrument.

The Benjolin is a chaotic, internally sequenced generative instrument. Understanding how it works requires considering O1 (Oscillator 1) as the “VCO” (the “voice” oscillator), and O2 as the LFO (the “clock” oscillator). The Pulse Width Modulation (a comparison of the two Triangle waveforms from each oscillator) is then fed into a resonant “VCF” (a multi-mode filter), which can then be sent to the output. The various waveforms of different internal sections of the Benjolin can also be sent to either the main output of the instrument, or the various control inputs of the oscillators and filter, using the matrix patchbay in the upper left of the screen.

All the control information is produced by the Rungler (labelled RUN in the patch), which is a digital shift register followed by an “analog-to-digital” converter which takes the last three bits exiting the shift register and makes a value from them. The shift register is fed “data” from the Pulse wave of O1, and is clocked by the Pulse wave of O2. For every cycle of O2, a new bit of information enters the shift register, and the value of each cell in the shift register is passed on to the next. Normally, the last bit leaving the shift register makes an Exclusive-OR (“XOR” in the interface) operation on the incoming bit from O1, which allows for some chaotic nonlinear feedback in the Rungler and helps to produce self-similar but still emergent patterns. The LOOP switch defeats the incoming bits and recycles the bits leaving the shift register to make looped patterns possible.

The instrument can also bypass the internal oscillators and take an external audio signal either as the input of the filter, or the clock of the Rungler, using the switches in the upper right of the interface.

*CHANGELOG*

17.05.17: corrected modulation inputs to O1 (thx Anton!), added Pd-native [rev2~] in place of external [freeverb~] in the help patch.

17.09.19: updated list of libraries necessary to install on Pure Data Vanilla, thx to Dan Friedman.

NOV 2016
Derek Holzer
macumbista AT THE DOMAIN gmail DOT com


# Supplementary materials: Enhanced Demodulation for Low Latency Audio Pitch Shifting in Frequency Domain
This repository contains supplementary materials for an enhancement of pitch shifting algorithm “Ocean”, detailed in the aforementioned paper by Jan Onderka and Martin Novotný. The Ocean algorithm was originally introduced in a paper by Nicolas Juillerat and Béat Hirsbrunner, _“Low latency audio pitch shifting in the frequency domain,” in 2010 International Conference on Audio, Language and Image Processing, IEEE, 2010, pp. 16–24_.

## Equation check notebook

The `equation_check.nb` Wolfram Mathematica notebook progressively constructs the signal and modulation curve equations. Checks are made to ensure the equations presented in the paper are correct. This notebook may also be used for further exploration of different windows and algorithms by changing the appropriate equations. A static version of the notebook, not requiring Wolfram Mathematica, is present in `equation_check.pdf`.

## Implementation outputs

Outputs of three signals processed by the algorithms studied in the paper are present in the `/output` folder. The output signals are in form `/output/<signal>/<signal>_<scaling factor>_<algorithm>.flac`. The inputs are also present as `/output/signal/<signal>.flac`. The primary scaling factors chosen were in 12-tone equal temperament, from -12 semitones up to +12 semitones, spaced a semitone apart. Scaling factors _0.25_, _1.75_ and _4_ were also included. The _1.75_ scaling factor (corresponding to a 7/4 interval, "harmonic seventh") was added due to its presence in the original Ocean paper and it not being approximated well by 12-tone equal temperament. All of the outputs are a result of offline 32-bit processing with parameters _O=4_ and _N=1024_. 

The signals in the repository are:
 - `sines`: A succession of bin-centered sinusoidal waves. They serve as mainly for confirmation of the adherence of the implementation to the algorithm properties and testing the audability of amplitude modulation in sinusoidal waves. The introduced amplitude modulation is rather prominent in them, resulting in an "organ-like" sounds.
 - `bass`: A bass guitar recording, going from low E (E1) up by semitone at a time until finally stopping on the highest note (E4) and letting it ring out. In our experience, the held note at the end of the recording is the one where the introduced amplitude modulation is heard the best. In lower octaves, detuning artifacts are usually apparent.
 - `guitar`: An electric guitar recording where four chords are played and each one is let to ring out. The last chord (F) was found to be the one in which the amplitude modulation artifacts are the most apparent.
 
 The algorithms used are:
 - original Ocean (`original`): The original Ocean algorithm, using a single demodulation curve.
 - no demodulation (`no_demod`): The original Ocean algorithm without the demodulation step being performed. This produces extremely apparent amplitude modulation in most cases.
 - our enhanced algorithm (`enhanced`): Enhanced algorithm presented in our paper. We found it removes undesired amplitude modulation the same as or better than the original algorithm, albeit at a price of higher processing time requirements.
 - single-bin demodulation (`single`): Single-bin algorithm also considered in our paper. Similar to the enhanced algorithm, but splits bins in two groups before analysis-windowing. Performs well for single-bin input signals, but introduces discontinuity artifacts to real signals (especially apparent in the bass signal outputs).
 
 For reviewing the outputs, we recommend a digital audio editor such as [Audacity](https://www.audacityteam.org/) and potentially an ABX testing tool such as the [Lacinato ABX/Shootouter](https://lacinato.com/cm/software/othersoft/abx).
 

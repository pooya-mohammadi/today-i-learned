# Wave
1) To describe a sound wave we have some information as below:
2) ![img.png](images/wave/wave_image.png)
   1) Frequency: Is the inverse of Period.
      1) Number of cycles that happens in a second.
      2) 1 Hz: 1 cycle per period
      3) higher frequency results in higher pitch
   2) Amplitude: is the maximum magnitude value a wave can have. The scale of the amplitude is Pascal. Because showing the true pascal values could mess up graphs most of the time the graph readability is preferred over actual values and instead of 10.000.000 Pa the 10 is shown. 
      1) Loud sounds have larger amplitude
         1) Loudness is defined in  terms of the ratio of a sound pressure level (serving the role of output  power) to the auditory threshold sound pressure level (serving the role of input power)
      2) to be clear, the scale of **sound pressure level** is Pascal and the **loudness scale** is **decibel** which is the relative sound pressure.
         1) loudness is indicated with dB. 
            1) dBFS, or decibels relative to Full Scale, is used to measure digital audio signal levels. dBFS is another dimensionless quantity, because it is just a number and cannot be converted to another unit.
            2) It starts from zero to -infinity
            3) -6 db is equivalent to 50% of the maximum level
               1) -inf - -6 -> 0-50%
               2) -6 - 0 -> 50-100%
            4) decible aligns better with how we hear sound.
            5) equation:
               1) 20 log10(Am/Ar) -> 20 log10(Am)
                  1) Am: measured amplitude
                  2) Ar= reference amplitude -> maximum possible amplitude before clipping which is one
               2) Am = 0 -> db = -inf
               3) Am = 1 -> db = 1
               4) Am = 0.5 -> db = -6
            6) The level of 0 dBFS(db-full-scale) is assigned to the maximum possible digital level.
               1) For example, a signal that reaches 50% of the maximum level has a level  of −6 dBFS, which is 6 dB below full scale. 
               2) Conventions differ for root-mean-square (RMS) measurements, but all peak measurements smaller than the maximum are negative levels. 
         2) Max pressure is indicated with Pa
            1) Normal conversation sound pressure ranges from 0.002 Pa to 0.2 Pa. 
               1) In comparison, a trumpet sound pressure reaches a sound pressure level of 63 Pa. 
               2) A jet engine sound pressure level reaches a sound pressure level of 632 Pa.
               3) These pressure levels tell you that the human voice exerts less pressure on the surrounding air molecules than a trumpet. And, the trumpet exerts less pressure on the surrounding air molecules than a jet engine.
            2) Calculation of the decibel level of a sound pressure level is computed by the following equation:
               1) dB(SPL) = 20 log10(p/p0)
               2) P0 = reference pressure level of auditory threshold(Pa) = 20 micro Pa(this is the minimum threshold for human ear)
               3) dB (SPL) values computed by this formula are commonly called the  loudness of the sound.A sound source with a higher dB (SPL) level is  considered to be a louder sound.
               4) Fact: 
                  1) An increase of 6 dB (SPL), doubles the loudness of the sound.
                  2) this indicates increase of 6 dB means the pressure of the sound has been twiced.
                  3) an increase of 10 dB (SPL) triples the loudness of the sound.
   3) Frequency vs Loudness:
      1) Frequency and loudness are two different characterizations of sound. Frequency is an absolute value that describes the oscillations of a vibrating sound source. Loudness is a relative value that compares the sound pressure level of the sound wave of one sound with the sound pressure level of a sound at the auditory threshold.
      2) Changing the loudness of a sound has no effect on its frequency.
      3) frequency describes oscillation while loudness describes sound pressure level relative to the auditory threshold.
      4) A general sound consists of the combination of multiple frequencies.  This fact was determined by Wiener in his application of the wave theory  of Fourier to frequency variables. 
      5) Loudness of a specific frequency within a specific and general sound cannot be determined. This limitation is a result of modern sound  recording equipment. Loudness can be determined for the complete sound,  not for frequencies within a complete sound.
      6) However, loudness of a frequency can be determined if the sound consists of a single frequency. A sound that consists of a single  frequency is called a pure tone. Audiologists use pure tones when testing  a person’s hearing
      7) When there are more than one frequency we can't determine the loudness.
   4) Frequency formulation:
      1) f(t) = a * sin(2 * pi * f * t)
      2) t = time (seconds)
      3) a = maximum amplitude
      4) f = frequency (cycles/sec or Hz)
      5) f(t) = amplitude of sound wave at time t (Pa or [-1, +1])
   5) Period:
      1) Period is the time in seconds between two crests of a waveform. It could also be determined between two zeros or two troughs.
      2) P = 1 / f
      3) where
      4) P = period (sec)
      5) f = frequency( cycles / sec or Hz)
   6) Wavelength:
      1) wavelength of a sound wave is the length of the beginning of the positive pressure to the end of the negative pressure.
      2) W = c/f
      3) where
      4) W = wavelength
      5) c = speed of sound(meters/second)(300 m/sec) ( speed of sound in a specific medium)
         1) Sound travels at a speed of 340.29 meters/second at sea level
         2) Speed of sound varies depending on the density of the atmosphere
         3) Both temperature and atmospheric pressure affect the speed of sound
         4) Studies show that humidity does not affect the speed of the sound.
      6) f = frequency (cycles / sec or Hz)
      7) if f = 1 Hz and c is 300 m/s the wavelength is 300 meters per 1 Hz
3) https://hometheaterhifi.com/technical/technical-reviews/audio-frequency-loudness-part-introduction-basics/
4) pictures are taken from the above-mentioned website.
## what for?

Acoustic analysis can be used to determine the health status and mood of
the bees.

### apidictor patent

**frequencies to measure:**

  - 180-190 Hz ("normal"): healthy bee sound in quiet period (night?)
  - \~220-290 Hz ( "warble"): if that sound occurs, queen's rate of egg
    laying has diminished.
  - \>3000 Hz ("hiss") : sound occurs by clapping or knocking on the
    hive.
      - short sharp hiss: healthy queen
      - sluggish rise in hiss with slow fade: abnormality

**interpretation of the sounds**

| warble | hiss                                                                                          | interpretion                                                    |
| ------ | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| yes    | sluggish rise and fall, max intensy much less than normal. "at time of issue it has vanished" | swarming activity. possibly noticeable 15 days before swarming. |
| yes    | short sharp hiss                                                                              | age or deformity of the queen                                   |
| yes    | on hiss vanishes completly                                                                    | death or removal of queen                                       |

So practical usage would be alerting if warble sounds occure. Also a LED
signal responding to the hiss would be a quite nice on-field use and
interaction: knocking on the hive: "everything alright?" - and the
sensor answers with green (shor sharp hiss), red (sluggish hiss) or no
light (nobody there\!)..?

### Acoustic sensor for beehive monitoring (US 8152590)

The patent says that it's possbile determine quality and quantity of air
pollution and desease (mites, foulbrood) by analysing sound spectrum
frequencies in bee hives. Quite complex statistical analysing required
and basic data. Question would be, if every hive responds in the same
way to pollution/desease, so that collected data could be compared with
new positioned hives.

If that's possible the OSBH could set up a world wide pollution map with
beehives\! Also determinig bee's desease would be important data to
analyse bee die off.

## Arduino audio capabilities and sample Rates

  - Arduino can sample up to 8 kHz with analogRead.
  - bypassing AnalogRead gives about 38,5 kHZ
  - Sample rate should be at least about 2.5 time the signal frequencie
  - With Analog Read it would be possible to analyse frequencies up to
    3.2 kHZ (is that enough?)

## FFT Frequency analysis

  - fight leakage of the signal with windowing functions (e.g. hamming)
  - time smearing is not that big problem because of the probably
    constant sound inside the hive
      - for detecting leaving and incoming bees it might be important to
        look at that issue again

## Links

  - <http://www.beehacker.com/wp/wp-content/uploads/2010/07/2806082_DEFECTI.pdf>
  - <http://www.digitalbees.info/sources/S%20Ferrari%202008.pdf>
  - [US Patent
    US 8152590](http://www.google.com/patents/US7549907?hl=de&dq=honey+bee+acoustic+recording)
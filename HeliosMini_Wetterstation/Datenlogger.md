HeliosMini rht von Skye Instruments ist eine kleine Wetterstation, die
Luftfeuchte und Tauwasser misst und aufzeichnet. Ein Regenmesser kann
noch angeschlossen werden. Das Gerät besitzt eine serielle Schnittstelle
zum Herunterladen der Daten. Die Einstellungen sind:

  - 9600 baud, no parity, 8 data bits, 1 stop bits and Xon / Xoff flow
    control

Laut dem Benutzerhandbuch gelten folgende Befehle:

  - `a` ... Offload in ASCII
  - `b` ... Offload in (formatted) Binary
  - `c` ... Send Readings from all Channels (No Logging)
  - `d` ... Send Logger Status
  - `1` ... Send Logger Time
  - `RM` ... Reset Memory

<!-- end list -->

  - `T` ... Set the Date and Time. This must be entered exactly - hour,
    minute, second, day, month, year, e.g. 100620010301 which would be
    10:06:20 on 01/03/01. This will be repeated and you need to enter OK
    (in capital letters). The logger will repeat OK and the changes will
    take effect. Please note, the date and time must be entered within 3
    seconds of pressing T. If not, the logger will reset itself and no
    changes will have been made. You will then need to repeat the
    process.

<!-- end list -->

  - `ID` ... Enter new logger ID. This must be exactly 16 characters
    (numbers or letters) which must not include spaces, commas, full
    stops etc. For example you could enter HeliosinField010.
    Then enter OK (in capitals) and OK will be repeated and the changes
    will take effect. Please note, the date and time must be entered
    within 3 seconds of pressing ID. If not, the logger will reset
    itself and no changes will have been made. You will then need to
    repeat the process.

<!-- end list -->

  - `SF` ... Enter new scaling factors. These must be entered as a
    string of numbers which are 6 sets of 5 digits. The first is the
    figure for 1%RH, the second for 75% RH, the others are spare
    calibration points and any numbers may be entered. For example, you
    could enter 476285094311111222223333344444 whereby 47628 is the 1%
    calibration figure, 50943 is the 75% calibration figure and the
    remaining numbers are not used in this version of the Helios range
    and any numbers or letters may be entered.
    These numbers will be repeated, enter OK (in capitals) which will be
    repeated and the changes will take effect. Please note, the date and
    time must be entered within 3 seconds of pressing SF. If not, the
    logger will reset itself and no changes will have been made. You
    will then need to repeat the process

<!-- end list -->

  - `LI` ... This will change the Log Interval. The codes are:
      - `1` ... 1 minute
      - `2` ... 5 minutes
      - `3` ... 10 minutes
      - `4` ... 15 minutes
      - `5` ... 20 minutes
      - `6` ... 30 minutes
      - `7` ... 1 hour
      - `8` ... 2 hours

NOTE - these logging intervals are ‘spot’ logs only. The logger will
take a set of 3 consecutive measurements at each logging interval time
and store the average of these 3 measurements. No measurements are taken
to form an average over the entire the logging interval.

Mit dem folgenden Shell-Script konnte ich die Zeit des Datenloggers mit
der Systemzeit des Raspberry Pi einstellen:

`#!/bin/bash`

`echo T $(date +"00%H%M%S%d%m%y)") > /dev/USB-Serial-Port &&`
`sleep 1 &&`
`echo "OK" > /dev/USB-Serial-Port`

Zu beachten ist, dass ich aus unerfindlichen Gründen noch zwei Nullen
vorne an das Datum hängen musste.
# Controlling Panasonic AC unit with Raspberry and IR transmitter

## Hardware

I  purchased ANAVI Infrared pHAT for my Raspberry Pi 4 and installed it using their instructions (<https://github.com/AnaviTechnology/anavi-docs/blob/master/anavi-infrared-phat/anavi-infrared-phat.md>)

Unfortunately I didn't find proper IR codes for my AC unit (Panasonic CS-TZ25TKEW) so I had to record (some of those) myself.

## Recording and using the IR codes

To record the IR codes I stopped the lircd service and issued the following command with different file names:

`mode2 -m -d /dev/lirc1 >22c_auto_fanspd_mode2_record`

The files themselves need a bit modifying to be usable, those can be found in the `ac-lircd.conf` file shared in this repo. The file is to be placed in `/etc/lirc/lircd.conf.d/ac-lircd.conf`

To send the corresponding IR codes to the AC unit one can use the following commands:

```
irsend send_once ac off
irsend send_once ac on
irsend send_once ac 25c_min_fanspd
irsend send_once ac 25c_max_fanspd
irsend send_once ac 25c_auto_fanspd_auto_swing
irsend send_once ac 22c_auto_fanspd
irsend send_once ac 22c_auto_fanspd_auto_swing
irsend send_once ac 22c_max_fanspd
irsend send_once ac 22c_min_fanspd
```

All modes with the exception of "_auto_swing" have the air deflector set in a fixed position that is suitable for my apartment. The `ac on` corresponds to target temp of 25C with automatic fanspeed and fixed deflector setting.
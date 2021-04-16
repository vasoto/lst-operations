# NoMachine Installation

## Issue

Dear Vassil, I think I need your help.
1. I downloaded the evaluation version for NoMachine Enterprise Desktop from
https://www.nomachine.com/product&p=NoMachine%20Enterprise%20Desktop
to operatorSpare

2. I uninstall the standard NoMachine from operatorSpare
`/usr/NX/scripts/setup/nxserver --uninstall`

3. I installed the Enterprise Desktop on operatorSpare
a) `tar zxvf nomachine-enterprise-desktop_7.0.211_4_x86_64.tar.gz`
b) `/usr/NX/nxserver --install`

4. However, I cannot connect from remote to the new server. The log on the NX server says:
```
2629 2629 2021-01-07 02:44:15 747.238 NXSERVER User 'lst1' logged in from '127.0.0.1' using authentication method NX-password.
2666 2666 2021-01-07 02:44:35 005.736 NXSERVER WARNING! NXRedis: timeout for command evalsha which is 10 has been reached.
2666 2666 2021-01-07 02:44:45 014.124 NXSERVER Previous message repeated 1 time
2666 2666 2021-01-07 02:44:45 014.185 NXSERVER WARNING! NXRedis: failed twice connection to db.
2666 2666 2021-01-07 02:44:45 014.230 NXSERVER ERROR! NXRedis: Cannot get output for command: evalsha after resending.
2629 2629 2021-01-07 02:44:45 023.092 NXSERVER ERROR! Received error from nxserver --daemon nxFrameBuffer error while starting
2629 2629 2021-01-07 02:44:45 540.415 NXSERVER User 'lst1' from '127.0.0.1' logged out.
```

Since I could connect to operatorSpare from my NoMachine client before, I think there must be some configuration issue.
Also, I am puzzled that on the NoMachine client I get
"Cannot detect any display running. Do you want NoMachine to create a new display and proceed to connect to the desktop?"
I thought there was an X running... but OK, maybe there is indeed no active session for user lst1? But somehow I see no big difference if I compare operator1 and operatorSpare...
Your help is appreciated!
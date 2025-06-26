# NTP

## LIN3 - Rapport d'évaluation NTP et Kerberos

* Candidat : Alexandre GAPANY

***

### Server

* Which ntp client is setup ?

```
    [INPUT]
    systemctl | grep NTP

    [OUTPUT]
    chrony.service  loaded active running   chrony, an NTP client/server
```

* Is ntp a service ?

```
    [INPUT]
    systemctl status chrony

    [OUTPUT]
    chrony.service - chrony, an NTP client/server
     Loaded: loaded (/lib/systemd/system/chrony.service; enabled; vendor preset: enabled)
     Active: active (running) since Sun 2023-01-01 16:58:35 CET; 3h 11min ago
```

* Does the date correctly display (as well as the timezone)

```
    [INPUT]
    date

    [OUTPUT]
    Sun Jan  1 20:10:32 CET 2023
```

* Is the ntp config file correct (sources, logs, ip range restriction)

```
    [INPUT]
    vi /etc/chrony/chrony.conf

    [OUTPUT]
    # Welcome to the chrony configuration file. See chrony.conf(5) for more
    # information about usuable directives.

    # Use the AWS time sync service per
    # https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/set-time.html
    server 2.ie.pool.ntp.org prefer iburst
    server 0.europe.pool.ntp.org iburst
    server 1.europe.pool.ntp.org iburst

    # This directive specify the location of the file containing ID/key pairs for
    # NTP authentication.
    keyfile /etc/chrony/chrony.keys

    # This directive specify the file into which chronyd will store the rate
    # information.
    driftfile /var/lib/chrony/chrony.drift

    # Uncomment the following line to turn logging on.
    # TODO log disable
    #log tracking measurements statistics

    # Log files location.
    logdir /var/log/chrony

    # Stop bad estimates upsetting machine clock.
    maxupdateskew 100.0

    # This directive enables kernel synchronisation (every 11 minutes) of the
    # real-time clock. Note that it canâ€™t be used along with the 'rtcfile' directive.
    rtcsync

    # Step the system clock instead of slewing it if the adjustment is larger than
    # one second, but only in the first three clock updates.
    makestep 1 3

    # Network allow
    allow 10.0.2.0/28
```

* Testing log files

After enabling logs, ok.

* FQDN Issue

```
    [INPUT]
    Error message after tail -f command (as well as restart the service)
    sudo tail -f /var/log/chrony/[logName]
    sudo systemctl restart chrony

    [OUTPUT]
    sudo: unable to resolve host deb.actualit.info: Name or service not know
```

* Validation

```
    [INPUT]
    chronyc tracking
    
    [OUTPUT]
    Reference ID    : 58516482 (brenbox.westnet.ie)
    Stratum         : 2
    Ref time (UTC)  : Sun Jan 01 19:13:28 2023
    System time     : 0.000757703 seconds fast of NTP time
    Last offset     : +0.001277600 seconds
    RMS offset      : 0.001277600 seconds
    Frequency       : 16.465 ppm slow
    Residual freq   : +13.053 ppm
    Skew            : 0.044 ppm
    Root delay      : 0.006816404 seconds
    Root dispersion : 0.001016396 seconds
    Update interval : 64.8 seconds
    Leap status     : Normal
```

```
    [INPUT]
    chronyc sources

    [OUTPUT]
    MS Name/IP address         Stratum Poll Reach LastRx Last sample
    ===============================================================================
    ^* brenbox.westnet.ie            1   6    37    41    +41us[+1318us] +/- 3423us
    ^- routerzw.vanderzwet.net       2   6    37    42   -588us[ +689us] +/-   38ms
    ^- server1b.meinberg.de          2   6    37    42  -1142us[ +135us] +/-   15ms
```

```
    [INPUT]
    chronyc sourcestats

    [OUTPUT]
    Name/IP Address            NP  NR  Span  Frequency  Freq Skew  Offset  Std Dev
    ==============================================================================
    brenbox.westnet.ie          5   5    71    +13.053    145.241   +784us   633us
    routerzw.vanderzwet.net     5   3    71    +10.776    290.565   +581us   549us
    server1b.meinberg.de        5   3    71    -14.790     18.749  -2036us   110us
```

### LIN Client

* Which ntp client is setup ?

```
    [INPUT]
    systemctl | grep NTP

    [OUTPUT]
    chrony.service  loaded active running   chrony, an NTP client/server
```

* Does the date correctly display (as well as the timezone)

```
    [INPUT]
    date

    [OUTPUT]
    Mon Jan  2 14:23:02 CET 2023
```

* Config

```
    [INPUT]
    vi /etc/chrony/chrony.conf

    [OUTPUT]
    # Welcome to the chrony configuration file. See chrony.conf(5) for more
    # information about usuable directives.

    # Use the AWS time sync service per
    # https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/set-time.html
    server 10.0.2.10 prefer iburst
    server 10.0.2.12 iburst

    maxdistance 16.0

    # This directive specify the location of the file containing ID/key pairs for
    # NTP authentication.
    keyfile /etc/chrony/chrony.keys

    # This directive specify the file into which chronyd will store the rate
    # information.
    driftfile /var/lib/chrony/chrony.drift

    # Uncomment the following line to turn logging on.
    log tracking measurements statistics

    # Log files location.
    logdir /var/log/chrony

    # Stop bad estimates upsetting machine clock.
    maxupdateskew 100.0

    # This directive enables kernel synchronisation (every 11 minutes) of the
    # real-time clock. Note that it can’t be used along with the 'rtcfile' directive.
    rtcsync

    # Step the system clock instead of slewing it if the adjustment is larger than
    # one second, but only in the first three clock updates.
    makestep 1 3
```

* Testing log files

ok

* Validation

```
    [INPUT]
    chronyc tracking

    [OUTPUT]
    Reference ID    : 0A00020C (10.0.2.12)
    Stratum         : 2
    Ref time (UTC)  : Mon Jan 02 13:23:29 2023
    System time     : 0.000000777 seconds fast of NTP time
    Last offset     : -0.000751936 seconds
    RMS offset      : 0.000751936 seconds
    Frequency       : 15.837 ppm fast
    Residual freq   : -11.309 ppm
    Skew            : 0.621 ppm
    Root delay      : 0.000982217 seconds
    Root dispersion : 10.000805855 seconds
    Update interval : 64.8 seconds
    Leap status     : Normal
```

### Win Client

* Which ntp client is setup ?

w32tm

* Does the date correctly display (as well as the timezone)

```
    [INPUT]
    Get-Date

    [OUTPUT]
    Monday, January 2, 2023 2:54:10 PM
```

```
    [INPUT]
    Get-TimeZone

    [OUTPUT]
    Id                         : W. Europe Standard Time
    DisplayName                : (UTC+01:00) Amsterdam, Berlin, Bern, Rome, Stockholm, Vienna
    StandardName               : W. Europe Standard Time
    DaylightName               : W. Europe Daylight Time
    BaseUtcOffset              : 01:00:00
    SupportsDaylightSavingTime : True
```

* Config

```
    [INPUT]
    w32tm /query /source

    [OUTPUT]
    10.0.2.10,
```

```
    [INPUT]
    w32tm /query /peers

    [OUTPUT]
    #Peers: 2

    Peer: 0.ie.pool.ntp.org,0x2
    State: Active
    Time Remaining: 150.6305440s
    Mode: 1 (Symmetric Active)
    Stratum: 2 (secondary reference - syncd by (S)NTP)
    PeerPoll Interval: 9 (512s)
    HostPoll Interval: 9 (512s)

    Peer: 10.0.2.10,
    State: Active
    Time Remaining: 150.6617502s
    Mode: 1 (Symmetric Active)
    Stratum: 3 (secondary reference - syncd by (S)NTP)
    PeerPoll Interval: 9 (512s)
    HostPoll Interval: 9 (512s)
```

* Logs ?

https://learn.microsoft.com/en-us/windows-server/networking/windows-time-service/windows-time-service-tools-and-settings

#### Debian NTP stopped

* Lin Client

```
    [INPUT]
    chronyc tracking

    [OUTPUT]
    Reference ID    : 0A00020C (10.0.2.12)
    Stratum         : 2
    Ref time (UTC)  : Mon Jan 02 16:11:27 2023
    System time     : 0.000027046 seconds fast of NTP time
    Last offset     : -0.017648188 seconds
    RMS offset      : 0.017648188 seconds
    Frequency       : 0.284 ppm fast
    Residual freq   : +6.995 ppm
    Skew            : 0.077 ppm
    Root delay      : 0.000555536 seconds
    Root dispersion : 10.001815796 seconds
    Update interval : 0.0 seconds
    Leap status     : Normal
```

* Win Client

```
    [INPUT]
    w32tm /query /peers

    [OUTPUT]
    #Peers: 2

    Peer: 0.ie.pool.ntp.org,0x2
    State: Active
    Time Remaining: 294.7006963s
    Mode: 1 (Symmetric Active)
    Stratum: 2 (secondary reference - syncd by (S)NTP)
    PeerPoll Interval: 17 (out of valid range)
    HostPoll Interval: 9 (512s)

    Peer: 10.0.2.10,
    State: Active
    Time Remaining: 294.7061382s
    Mode: 1 (Symmetric Active)
    Stratum: 0 (unspecified)
    PeerPoll Interval: 0 (unspecified)
    HostPoll Interval: 9 (512s)
```

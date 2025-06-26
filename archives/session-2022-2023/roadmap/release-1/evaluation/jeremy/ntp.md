# NTP

## LIN3 - Rapport d'évaluation NTP et Kerberos

* Candidat : Jeremy FAILLOUBAZ

***

### Server

* Which ntp client is setup ?

```
    [INPUT]
    systemctl | grep NTP

    [OUTPUT]
    chrony.service  loaded active     running         chrony, an NTP client/server
```

* Is ntp a service ?

```
    [INPUT]
    systemctl status chrony

    [OUTPUT]
    chrony.service - chrony, an NTP client/server
     Loaded: loaded (/lib/systemd/system/chrony.service; enabled; vendor preset: enabled)
     Active: active (running) since Sun 2023-01-01 16:58:33 CET; 2h 18min ago
```

* Does the date correctly display (as well as the timezone)

```
    [INPUT]
    date

    [OUTPUT]
    Sun Jan  1 19:18:16 CET 2023
```

* Is the ntp config file correct (sources, logs, ip range restriction)

```
    [INPUT]
    vi /etc/chrony/chrony.conf

    [OUTPUT]
    # Welcome to the chrony configuration file. See chrony.conf(5) for more
    # information about usuable directives.
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
    log tracking measurements statistics

    # Log files location.
    logdir /var/log/chrony

    # Stop bad estimates upsetting machine clock.
    maxupdateskew 100.0

    # This directive enables kernel synchronisation (every 11 minutes) of the
    # real-time clock. Note that it can not be used along with the 'rtcfile' directive.
    rtcsync

    # Step the system clock instead of slewing it if the adjustment is larger than
    # one second, but only in the first three clock updates.
    makestep 1 3

    #allow all
    #TODO remove double allow
    allow allow 10.0.1.0/28
```

* Testing log files

All three are operational.

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
    Reference ID    : 3411E749 (ec2-52-17-231-73.eu-west-1.compute.amazonaws.com)
    Stratum         : 3
    Ref time (UTC)  : Sun Jan 01 18:46:01 2023
    System time     : 0.000000015 seconds fast of NTP time
    Last offset     : -0.000014352 seconds
    RMS offset      : 0.000014352 seconds
    Frequency       : 33.807 ppm fast
    Residual freq   : +5.882 ppm
    Skew            : 0.195 ppm
    Root delay      : 0.001598871 seconds
    Root dispersion : 0.000800823 seconds
    Update interval : 2.1 seconds
    Leap status     : Normal
```

```
    [INPUT]
    chronyc sources

    [OUTPUT]
    MS Name/IP address         Stratum Poll Reach LastRx Last sample
    ===============================================================================
    ^* ec2-52-17-231-73.eu-west>     2   6   377    59    -14us[  -30us] +/- 1676us
    ^- ntp2.flashdance.cx            2   6   377    59   -383us[ -399us] +/-   45ms
    ^- 4.28.147.34.bc.googleuse>     2   6   377    59   +316us[ +300us] +/-   40ms
```

```
    [INPUT]
    chronyc sourcestats

    [OUTPUT]
    Name/IP Address            NP  NR  Span  Frequency  Freq Skew  Offset  Std Dev
    ==============================================================================
    ec2-52-17-231-73.eu-west>  10   5   394     -0.004      0.226   -175ns    22us
    ntp2.flashdance.cx         10   7   394     +0.408      5.326   +231us   524us
    4.28.147.34.bc.googleuse>  10   6   393     -0.364      2.950   +449us   280us
```

### LIN Client

* Which ntp client is setup ?

```
    [INPUT]
    systemctl | grep NTP

    [OUTPUT]
    chrony.service   loaded active running   chrony, an NTP client/server
```

* Does the date correctly display (as well as the timezone)

```
    [INPUT]
    date

    [OUTPUT]
    Mon Jan  2 14:49:16 CET 2023
```

* Config

```
    [INPUT]
    vi /etc/chrony/chrony.conf

    [OUTPUT]
    server 10.0.1.10 prefer iburst
    server 10.0.1.12 iburst
    maxdistance 16.0
    keyfile /etc/chrony/chrony.keys
    driftfile /var/lib/chrony/chrony.drift
    log tracking measurements statistics
    logdir /var/log/chrony
    maxupdateskew 100.0
    rtcsync
    makestep 1.0 3
```

* Testing log files

```
    [INPUT]
    sudo tail -f /var/log/chrony/tracking.log
    sudo tail -f /var/log/chrony/measurements.log
    sudo tail -f /var/log/chrony/statistics.log 
```

ok

* Validation

```
    [INPUT]
    chronyc tracking

    [OUTPUT]
    Reference ID    : 0A00010A (10.0.1.10)
    Stratum         : 4
    Ref time (UTC)  : Mon Jan 02 13:50:24 2023
    System time     : 0.000005523 seconds fast of NTP time
    Last offset     : +0.000007494 seconds
    RMS offset      : 0.047072519 seconds
    Frequency       : 1.841 ppm slow
    Residual freq   : +0.002 ppm
    Skew            : 0.055 ppm
    Root delay      : 0.004153488 seconds
    Root dispersion : 0.015431784 seconds
    Update interval : 130.2 seconds
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
    10.0.1.10
```

```
    [INPUT]
    w32tm /query /peers

    [OUTPUT]
    #Peers: 2

    Peer: 10.0.1.10,
    State: Active
    Time Remaining: 280.8240793s
    Mode: 1 (Symmetric Active)
    Stratum: 3 (secondary reference - syncd by (S)NTP)
    PeerPoll Interval: 9 (512s)
    HostPoll Interval: 9 (512s)

    Peer: 0.ie.pool.ntp.org,0x2
    State: Active
    Time Remaining: 280.8397877s
    Mode: 1 (Symmetric Active)
    Stratum: 2 (secondary reference - syncd by (S)NTP)
    PeerPoll Interval: 9 (512s)
    HostPoll Interval: 9 (512s)
    PS C:\Users\Administrator>

```

* Logs ?

https://learn.microsoft.com/en-us/windows-server/networking/windows-time-service/windows-time-service-tools-and-settings

#### Debian NTP stopped

* Lin Client

```
    [INPUT]
    chronyc tracking

    [OUTPUT]
    Reference ID    : 0A00010C (10.0.1.12)
    Stratum         : 4
    Ref time (UTC)  : Mon Jan 02 15:49:58 2023
    System time     : 0.000011020 seconds slow of NTP time
    Last offset     : -0.000030641 seconds
    RMS offset      : 0.001089668 seconds
    Frequency       : 30.260 ppm fast
    Residual freq   : -0.029 ppm
    Skew            : 0.542 ppm
    Root delay      : 0.004646979 seconds
    Root dispersion : 0.138156489 seconds
    Update interval : 64.6 seconds
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
    Time Remaining: 42.1403321s
    Mode: 1 (Symmetric Active)
    Stratum: 2 (secondary reference - syncd by (S)NTP)
    PeerPoll Interval: 10 (1024s)
    HostPoll Interval: 10 (1024s)

    Peer: 10.0.1.10,
    State: Pending
    Time Remaining: 1158.2568944s
    Mode: 0 (reserved)
    Stratum: 0 (unspecified)
    PeerPoll Interval: 0 (unspecified)
    HostPoll Interval: 0 (unspecified)
```

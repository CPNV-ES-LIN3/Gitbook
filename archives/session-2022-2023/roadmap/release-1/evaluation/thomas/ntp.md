# NTP

## LIN3 - Rapport d'évaluation NTP et Kerberos

* Candidat : Thomas HUGUET

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
     Active: active (running) since Sun 2023-01-01 16:58:28 CET; 3h 0min ago
```

* Does the date correctly display (as well as the timezone)

```
    [INPUT]
    date

    [OUTPUT]
    Sun Jan  1 19:58:56 CET 2023
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
    server 0.ie.pool.ntp.org prefer iburst
    server 3.europe.pool.ntp.org iburst
    server 1.europe.pool.ntp.org iburst

    # This directive specify the location of the file containing ID/key pairs for
    # NTP authentication.
    keyfile /etc/chrony/chrony.keys

    # This directive specify the file into which chronyd will store the rate
    # information.
    driftfile /var/lib/chrony/chrony.drift

    # Uncomment the following line to turn logging on.
    # TODO log aren't activated
    #log tracking measurements statistics

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

    # Allow NTP client access from local network.
    allow 10.0.3.0/24
```

* Testing log files

After enabling log, everything is ok.

* Validation

```
    [INPUT]
    chronyc tracking
    
    [OUTPUT]
    Reference ID    : A29FC801 (time.cloudflare.com)
    Stratum         : 4
    Ref time (UTC)  : Sun Jan 01 19:06:03 2023
    System time     : 0.000010960 seconds fast of NTP time
    Last offset     : -0.000001289 seconds
    RMS offset      : 0.000111256 seconds
    Frequency       : 4.073 ppm slow
    Residual freq   : +0.428 ppm
    Skew            : 0.728 ppm
    Root delay      : 0.017743671 seconds
    Root dispersion : 0.000568838 seconds
    Update interval : 64.2 seconds
    Leap status     : Normal

```

```
    [INPUT]
    chronyc sources

    [OUTPUT]
    MS Name/IP address         Stratum Poll Reach LastRx Last sample
    ===============================================================================
    ^* time.cloudflare.com           3   6   377    44    -20us[  -22us] +/- 9519us
    ^- n1.taur.dk                    1   6   377    43  -1329us[-1329us] +/-   16ms
    ^- skitty.itu.ch                 2   6   377    46   -324us[ -325us] +/-   51ms
```

```
    [INPUT]
    chronyc sourcestats

    [OUTPUT]
    Name/IP Address            NP  NR  Span  Frequency  Freq Skew  Offset  Std Dev
    ==============================================================================
    time.cloudflare.com         9   5   329     +0.163      1.439  +2107ns    89us
    n1.taur.dk                  9   4   330     +0.647     11.343  -1697us   721us
    skitty.itu.ch               9   7   328     -1.306      4.122   -731us   255us
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
    Mon Jan  2 15:08:37 CET 2023
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
    server 10.0.3.10 prefer iburst
    server 10.0.3.12 iburst

    # This directive specify the location of the file containing ID/key pairs for
    # NTP authentication.
    keyfile /etc/chrony/chrony.keys

    # This directive specify the file into which chronyd will store the rate
    # information.
    driftfile /var/lib/chrony/chrony.drift

    # Uncomment the following line to turn logging on.
    #TODO enable logs
    #log tracking measurements statistics

    # Log files location.
    logdir /var/log/chrony

    # Stop bad estimates upsetting machine clock.
    maxupdateskew 100.0

    # This directive enables kernel synchronisation (every 11 minutes) of the
    # real-time clock. Note that it can’t be used along with the 'rtcfile' directive.
    rtcsync

    # Step the system clock instead of slewing it if the adjustment is larger than
    # one second, but only in the first three clock updates.
    makestep 1.0 3
    maxdistance 16.0
```

* Testing log files

after enabling, ok

* Validation

```
    [INPUT]
    chronyc tracking

    [OUTPUT]
    Reference ID    : 0A00030A (10.0.3.10)
    Stratum         : 4
    Ref time (UTC)  : Mon Jan 02 14:15:10 2023
    System time     : 0.000006894 seconds slow of NTP time
    Last offset     : -0.000004036 seconds
    RMS offset      : 0.000003954 seconds
    Frequency       : 2.408 ppm fast
    Residual freq   : -0.001 ppm
    Skew            : 0.286 ppm
    Root delay      : 0.004247246 seconds
    Root dispersion : 0.016169965 seconds
    Update interval : 65.1 seconds
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
    Monday, January 2, 2023 3:19:08 PM
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
    10.0.3.10,
```

```
    [INPUT]
    w32tm /query /peers

    [OUTPUT]
    #Peers: 2

    Peer: 10.0.3.10,
    State: Active
    Time Remaining: 417.0030736s
    Mode: 1 (Symmetric Active)
    Stratum: 3 (secondary reference - syncd by (S)NTP)
    PeerPoll Interval: 9 (512s)
    HostPoll Interval: 9 (512s)

    Peer: 0.ie.pool.ntp.org,0x2
    State: Active
    Time Remaining: 417.0655111s
    Mode: 1 (Symmetric Active)
    Stratum: 2 (secondary reference - syncd by (S)NTP)
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
    Reference ID    : 0A00030C (10.0.3.12)
    Stratum         : 4
    Ref time (UTC)  : Mon Jan 02 15:39:12 2023
    System time     : 0.000000073 seconds slow of NTP time
    Last offset     : +0.000065227 seconds
    RMS offset      : 0.000959382 seconds
    Frequency       : 8.483 ppm slow
    Residual freq   : +0.163 ppm
    Skew            : 0.846 ppm
    Root delay      : 0.013276462 seconds
    Root dispersion : 0.121943936 seconds
    Update interval : 64.5 seconds
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
    Time Remaining: 565.7635501s
    Mode: 1 (Symmetric Active)
    Stratum: 2 (secondary reference - syncd by (S)NTP)
    PeerPoll Interval: 10 (1024s)
    HostPoll Interval: 10 (1024s)

    Peer: 10.0.3.10,
    State: Active
    Time Remaining: 409.7913875s
    Mode: 1 (Symmetric Active)
    Stratum: 0 (unspecified)
    PeerPoll Interval: 0 (unspecified)
    HostPoll Interval: 10 (1024s)
```

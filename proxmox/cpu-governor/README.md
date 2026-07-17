# CPU Governor

CPU governor system service that sets the governor policy at start-up time.

## Installation

1. Copy the files in this directory to your host starting from the root (/):

```bash
cp -aruv . /
```

2. Adjust your settings in /etc/default/cpu-governor

3. Enable the new cpu-governor service, optionally starting it now.

`systemctl enable --now cpu-governor`

You're done!


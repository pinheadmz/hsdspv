# hsdspv

A work-in-progress build process for Handshake SPV resolver executables.

### Goal

Make a "double-click-n-go" application that runs a Handshake recursive resolver
with as little impact on a user's system as possible.

### Methods

Currently this process requires two nodejs package bundlers for different reasons:

1. Configure hsd/bin/spvnode without a wallet and with the recursive resolver listening on port 53

2. [bpkg](https://github.com/chjj/bpkg) bundles hsd AND includes
[native code extensions](https://github.com/chjj/bpkg#bundle-mode)

3. [pkg](https://github.com/zeit/pkg) has the ability to
[compile executables](https://github.com/zeit/pkg#targets) for linux, macos and windows

### Usage

#### Download executable

[On MacOS, download the hsd-macos executable by clicking here.](https://github.com/pinheadmz/hsdspv/raw/master/hsdspv-macos)

#### Run hsdspv

The above goal is almost achievable except for one thing:
On MacOS, a user needs root privileges to run a program that binds to port 53

The solution requires opening a terminal.

1. Type `chmod a+x` and then drag the executable into the terminal window, such that the absolute path gets added.

2. Type `sudo` and then drag the executable into the terminal window, such that the absolute path gets added:

![sudo-CLI](https://raw.githubusercontent.com/pinheadmz/hsdspv/master/doc/sudo-cli.png)

You will have to enter your password to continue.

Watch those logs go! It will take a few seconds to sync the blockchain headers,
then you can start resolving Handshake names.


#### Configure OSX

1. Open System Preferences and go to the Network panel:

![sudo-CLI](https://raw.githubusercontent.com/pinheadmz/hsdspv/master/doc/settings-network.png)

2. Click `Advanced...` and then click the `DNS` tab:

![sudo-CLI](https://raw.githubusercontent.com/pinheadmz/hsdspv/master/doc/settings-network-dns.png)

As shown here, click the `+` and then add `127.0.0.1` to the list of DNS Servers.
If you already have `1.1.1.1` there for example, you can keep it. Just make sure
`127.0.0.1` is FIRST on the list. In addition, you may need to remove any servers
listed under `Search Domains` and just replace it with a `.`

This is to prevent your browser from misinterpreting a Handshake TLD as a search term.

After clicking `OK` and `Apply`, you should start seeing your `hsdspv` process
printing lots of DNS queries to the log output.

Welcome to the decentralized internet! Test it out by browsing to:

http://rough




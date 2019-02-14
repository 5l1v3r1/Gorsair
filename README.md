# Gorsair

<p align="center">
    <a href="https://asciinema.org/a/226476"><img src="images/gorsair.gif" width="700px"/></a>
</p>
<p align="center">
    <a href="#license">
        <img src="https://img.shields.io/badge/license-Apache-blue.svg?style=flat" />
    </a>
    <a href="https://goreportcard.com/report/github.com/Ullaakut/gorsair">
        <img src="https://goreportcard.com/badge/github.com/Ullaakut/gorsair" />
    </a>
    <a href="https://github.com/Ullaakut/gorsair/releases/latest">
        <img src="https://img.shields.io/github/release/Ullaakut/gorsair.svg?style=flat" />
    </a>
</p>

Gorsair is a penetration testing tool for discovering and remotely accessing Docker APIs from vulnerable Docker containers. Once it has access to the docker daemon, you can use Gorsair to directly execute commands on remote containers.

Exposing the docker API on the internet is a tremendous risk, as it can let malicious agents get information on all of the other containers, images and system, as well as potentially getting privileged access to the whole system if the image uses the `root` user.

<p align="center">
    <img src="images/Gorsair.png" width="300px"/>
</p>

## Install

### From a release

Set the:
* `GORSAIR_VERSION` to whatever release you are interested in
* `OS` to your operating system (`linux`, `windows` or `darwin`)
* `ARCH` to your architecture (`amd64`, `arm`, or `ppc64le`)

And then run the following command to install gorsair.

`curl -sS https://github.com/Ullaakut/Gorsair/releases/download/$GORSAIR_VERSION/gorsair_$OS_$ARCH --output /usr/local/bin/gorsair && chmod +x /usr/local/bin/gorsair`

### From the sources

* Make sure that you have a go version that supports modules (versions 1.11 and above)
* Make sure that your environment contains the `GO111MODULE` variable set to `on`
* Run `go build -o /usr/local/bin/gorsair cmd/*.go` from the root of this repository

## Command line options

* **`-t`, `--targets`**:    Set targets according to the [nmap target format](https://nmap.org/book/man-target-specification.html). Required. Example: `--targets="192.168.1.72,192.168.1.74"`
* **`-p`, `--ports`**:      (Default: `2375,2376`) Set custom ports.
* **`-s`, `--speed`**:      (Default: `4`) Set custom nmap discovery presets to improve speed or accuracy. It's recommended to lower it if you are attempting to scan an unstable and slow network, or to increase it if on a very performant and reliable network. You might also want to keep it low to keep your discovery stealthy. See [this for more info on the nmap timing templates](https://nmap.org/book/man-performance.html).
* **`-v`, `--verbose`**:    Enable more verbose logs.
* **`-D`, `--decoys`**:     List of decoy IP addresses to use (see the [decoy section of the nmap documentation](https://nmap.org/book/man-bypass-firewalls-ids.html))
* **`-e`, `--interface`**:  Network interface to use
* **`--proxies`**:          List of HTTP/SOCKS4 proxies to use to deplay connections with
([see documentation](https://nmap.org/book/man-bypass-firewalls-ids.html))
* **`-S`, `--spoof-ip`**:   IP address to use for IP spoofing
* **`--spoof-mac`**:        MAC address to use for MAC spoofing
* **`-v`, `--verbose`**:    Enable verbose logging
* **`-h`, `--help`**:       Display the usage information

## How can I protect my containers from this attack

* Avoid putting containers that have access to the docker socket on the internet
* Avoid using the `root` account in docker containers

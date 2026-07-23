# Forti VPN setup

The ACC VPN is based on [Fortinet](https://www.fortinet.com/) technology. You must install **the latest stable version of [FortiClient](https://www.fortinet.com/support/product-downloads)** for your operating system (you do not need to register; choose the "FortiClient VPN-only" variant).

It's also possible to use the [OpenConnect VPN client](https://www.infradead.org/openconnect/), which has support for multiple VPN protocols, including Forti SSL VPN. On Linux, install [this package](https://launchpad.net/ubuntu/resolute/+package/openconnect) for Ubuntu, [this package](https://packages.fedoraproject.org/pkgs/openconnect/openconnect/) for Fedora or see [here](https://wiki.archlinux.org/title/OpenConnect) for Arch-based distributions.

Once the VPN client is installed, open it and configure a new VPN connection:

- Connection Name: `ACC-UB`
- Remote Gateway: `vpn-acc.unibuc.ro:44398`
- Customize Port: `44398`
- Username and password: the credentials you've been provided by the ACC administrators when your account was created

See also the image below.

![FortiClient VPN configuration](images/forticlient-config.png)

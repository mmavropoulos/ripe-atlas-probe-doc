# Enterprise Linux 9: Binary RPM-specific Installation Instructions

If you want to set up a new Virtual Machine using Oracle EL9 in order to host your probe:

* Set up a new installation of Oracle EL9 (for example using [VirtualBox](https://www.virtualbox.org/) or [Parallels](https://www.parallels.com/)), please refer to the [Oracle EL9 installation guide](https://docs.oracle.com/en/operating-systems/oracle-linux/9/).

* When installing Oracle EL9 in a virtual machine, please configure the virtual network adapter in 'bridge mode' to allow IPv6 to work. Often the default is called 'shared' which only provides IPv4 NAT.

The RIPE NCC maintains binary RPM packages. These are currently available for RHEL9
(x86_64). These have been verified to work on Oracle Linux Server 9.4, Rocky Linux 9.5
and Red Hat Enterprise Linux 9.5.

To add the repository to your system and install the package, follow these steps:

1. Download the RPM that sets up the repository for the software probe RPM:

    ```
    curl -O 'https://ftp.ripe.net/ripe/atlas/software-probe/el9/noarch/ripe-atlas-repo-1.5-3.el9.noarch.rpm'
    ```

2. Check the hash of the RPM:

    ```
    sha256sum -b ripe-atlas-repo-1.5-3.el9.noarch.rpm
    ```

    The hash should be:

    ```
    10086e937b6111e8524a656601374752b022a6bfaa1e8ca92577c345311092c8
    ```

3. Install the RPM (with root privileges):

    ```
    rpm -Uvh ripe-atlas-repo-1.5-3.el9.noarch.rpm
    ```

    Answer `'y'` to the question of whether that is ok.


4. Now you can install the package for the software probe itself (with root privileges):

    ```
    dnf install ripe-atlas-probe
    ```

5. Answer `'y'` to import the GPG key with fingerprint `3AA1 535B DE7A 8322 11A4  7D46 D973 45B4 F6FC F4B8`.

6. Answer `'y'` that is ok to install the RPM. You may may also need to accept a signing key.

7. At the end of the installation process, follow the on-screen instructions to register and start up the probe.

    * The registration process is also described here for reasons of clarity. You need the public key part in order to
register the probe. This process is necessary in order for the probe to function. The public key can be found in 
`/etc/ripe-atlas/probe_key.pub`.

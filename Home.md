The dbus-broker project is an implementation of a message bus as defined by the D-Bus specification. Its aim is to provide high performance and reliability, while keeping compatibility to the D-Bus reference implementation. It is exclusively written for linux systems, and makes use of many modern features provided by recent linux kernel releases.

While compatibility to existing D-Bus implementations is crucial, there are several situations where dbus-broker deviates from existing practices, and provides its own solutions. All these deviations are [documented](Deviations).

It is possible to use dbus-broker as a drop-in replacement for the reference implementation, as described [below](#using-dbus-broker), but it is also possible to [integrate](Integration) the message broker directly as an isolated process without any side-effects or file-system access.

# Available Packages

* Arch Linux: [-git](https://aur.archlinux.org/packages/dbus-broker-git)
* Arch Linux: [-stable](https://www.archlinux.org/packages/extra/x86_64/dbus-broker/)
* Debian: [-sid](https://packages.debian.org/sid/dbus-broker)
* Debian: [-bullseye](https://packages.debian.org/bullseye/dbus-broker)
* Fedora: [-stable](https://copr.fedorainfracloud.org/coprs/g/bus1/dbus/package/dbus-broker/)
* Gentoo Linux: [-git](https://packages.gentoo.org/packages/sys-apps/dbus-broker)
* Gentoo Linux: [-stable](https://packages.gentoo.org/packages/sys-apps/dbus-broker)
* NixOS: [-stable](https://github.com/NixOS/nixpkgs/tree/master/pkgs/os-specific/linux/dbus-broker)
* OpenEmbedded: [-git](http://cgit.openembedded.org/meta-openembedded/tree/meta-oe/recipes-core/dbus)
* OpenSUSE: [-git](https://software.opensuse.org/package/dbus-broker)
* Ubuntu: [-hirsute](https://packages.ubuntu.com/hirsute/dbus-broker)

# Using dbus-broker

Both the D-Bus System and User Bus can be provided via dbus-broker as a replacement for dbus-daemon. You must install the dbus-broker package via your distribution package manager first. It ships two systemd units (both called `dbus-broker.service`, one each for user and system instance of systemd), which are suitable as drop-in replacements for `dbus.service` as provided by the D-Bus reference implementation.

(You still need the dbus reference implementation installed, since it provides tools used by many applications, as well as the `dbus.socket` unit file.)

To enable dbus-broker as system bus, run:

    # systemctl enable dbus-broker.service

This will create a link `/etc/systemd/system/dbus.service` pointing to the dbus-broker service file, as such replacing the service file provided by the reference implementation.

Similarly, the user bus can be provided by dbus-broker via:

    # systemctl --user enable dbus-broker.service
    ..or..
    # systemctl --global enable dbus-broker.service

The first command enables it just for the calling user, while the second command enables it for all local users.

After a reboot the changes take effect.

# Releases

All [dbus-broker releases](https://github.com/bus1/dbus-broker/releases) come with a signed tar archive with all subproject-dependencies included. Distributors are free to use separately packaged subproject-dependencies and discard the bundled versions. Additionally, a checksum and signature of the tarball is provided.

The currently uses GPG-key for release signatures can be found on [@GitHub](https://github.com/dvdhrm.gpg).
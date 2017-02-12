# coreos-dns

Uses [vagrant-landrush](https://github.com/vagrant-landrush/landrush) and an [nginx](https://www.nginx.com/resources/admin-guide/tcp-load-balancing/) container to balance TCP over a target set of nodes.

Note that programmatic creation of the `nginx.conf` file has yet to be implemented.

See [my blog article](https://medium.com/@jeffzzq/vagrant-landrush-and-coreos-844889f8c07#.w5t2joqu4) for the changes required for [vagrant-landrush](https://github.com/vagrant-landrush/landrush) to work
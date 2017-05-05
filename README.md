Role Name
=========

Manage sysctl values via /etc/sysctl.d.

Requirements
------------

None

Role Variables
--------------

```
sysctl_config: []
sysctl_file: "/etc/sysctl.d/00-ansible.conf"
```
Every element of `sysctl_config` should contain a `token` and `value`. A `comment`
can be included, but will have no impact on the settings.
See the sysctl.conf(5) man page for more details on the options.  See example below
for general hardening and 1Gb NIC optmizations.

Dependencies
------------

None

Example Playbook
----------------

    - hosts: some_servers
      vars:
        sysctl_config:
          - token: fs.protected_hardlinks
            value: 1
            comment: provides protection from ToCToU races
          - token: fs.protected_symlinks
            value: 1
            comment: provides protection from ToCToU races
          - token: kernel.kptr_restrict
            value: 1
            comment: makes locating kernel addresses more difficult
          - token: kernel.perf_event_paranoid
            value: 2
            comment: set perf only available to root
          - token: kernel.randomize_va_space
            value: 2
            comment: randomize addresses of mmap base, heap, stack, and VDSO page
          - token: net.core.rmem_default
            value: 16777216
          - token: net.core.wmem_default
            value: 16777216
          - token: net.core.rmem_max
            value: 16777216
          - token: net.core.wmem_max
            value: 16777216
          - token: net.core.optmem_max
            value: 40960
          - token: net.core.netdev_max_backlog
            value: 50000
          - token: net.ipv4.tcp_max_syn_backlog
            value: 30000
          - token: net.ipv4.tcp_max_tw_buckets
            value: 2000000
          - token: net.ipv4.tcp_rmem
            value: '4096 87380 16777216'
          - token: net.ipv4.tcp_wmem
            value: '4096 87380 16777216'
          - token: net.ipv4.tcp_mtu_probing
            value: 1
          - token: net.ipv4.tcp_fin_timeout
            value: 10
          - token: net.ipv4.tcp_rfc1337
            value: 1
          - token: net.ipv4.tcp_tw_reuse
            value: 1
          - token: net.ipv4.tcp_slow_start_after_idle
            value: 0
          - token: net.ipv4.tcp_syncookies
            value: 1
            comment: enables syn flood protection
          - token: net.ipv4.udp_rmem_min
            value: 8192
          - token: net.ipv4.udp_wmem_min
            value: 8192
          - token: net.ipv4.conf.all.accept_redirects
            value: 0
            comment: ignore ICMP redirects
          - token: net.ipv4.conf.all.accept_source_route
            value: 0
            comment: ignore source-routed packets
          - token: net.ipv4.conf.all.log_martians
            value: 1
          - token: net.ipv4.conf.all.secure_redirects
            value: 1
            comment: ignore ICMP redirects from non-gateway hosts
          - token: net.ipv4.conf.all.send_redirects
            value: 0
          - token: net.ipv4.conf.all.rp_filter
            value: 1
          - token: net.ipv4.conf.default.accept_redirects
            value: 0
            comment: ignore ICMP redirects
          - token: net.ipv4.conf.default.accept_source_route
            value: 0
            comment: ignore source-routed packets
          - token: net.ipv4.conf.default.log_martians
            value: 1
          - token: net.ipv4.conf.default.secure_redirects
            value: 1
            comment: ignore ICMP redirects from non-gateway hosts
          - token: net.ipv4.conf.default.send_redirects
            value: 0
          - token: net.ipv4.conf.default.rp_filter
            value: 1
          - token: net.ipv4.icmp_ignore_bogus_error_responses
            value: 1
          - token: net.ipv4.ip_forward
            value: 0
            comment: do not allow IP forwarding between netowrks
          - token: vm.swappiness
            value: 10
      roles:
        - {{ lmickh.sysctl }}

License
-------

MIT

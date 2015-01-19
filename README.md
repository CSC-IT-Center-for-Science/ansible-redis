Redis
=======

This role does an install of Redis via yum and starts the service for Redhat platforms.

The init script is set to the format recommended by redis of redis_portnumber.

You can configure all variables that are availabe in the redis.conf file except for those that come as commented out by default.  Always refer to the redis.conf file before changing variables, lest you cause a catastrophe to your setup.

Example
-------

```
- name: Install redis
  yum:
    name=redis
    state=present
  when:
    ansible_os_family == "RedHat"
  vars:
    redis_config_dir: /etc/redis/corporate_dir
    redis_port: 1234
    max_dbs: 8
    client_idle_timeout: 3
```


Role variables
--------------
```
redis_config_dir: /etc/redis
redis_var_dir: /var/redis

daemonize: yes
pidfile: /var/run/redis/redis.pid
redis_port: 6379
redis_bind:
  - 127.0.0.1
client_idle_timeout: 0
redis_loglevel: notice
log_dir: /var/log/redis
redis_log: "{{ log_dir }}/redis.log"
max_dbs: 16

#db saves: seconds and changes eg 900 seconds and 1 change
redis_save:
  - 900 1
  - 300 10
  - 60 1000

rdb_compression: yes
dbdump_filename: dump.rdb
redis_working_dir: /var/lib/redis
slave_serve_stale_data: yes
append_only: no
append_fsync: everysec
no_append_fsync_on_rewrite: no
auto_aof_rewrite_precentage: 100
auto_aof_rewrite_min_size: 64mb
slowlog_log_slower_than: 10000
slowlog_max_len: 1024
vm_enabled: no
vm_swap_file: /tmp/redis.swap
vm_max_memory: 0
vm_page_size: 32
vm_pages: 134217728
vm_max_threads: 4
hash_max_zipmap_entries: 512
hash_max_zipmap_value: 64
list_max_ziplist_entries: 512
list_max_ziplist_value: 64
set_max_intset_entries: 512
zset_max_ziplist_entries: 128
zset_max_ziplist_value: 64
active_rehashing: yes
```

License
-------

MIT


Author
------

Robert Readman

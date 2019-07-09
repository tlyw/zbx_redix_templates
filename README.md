# zbx_redix_templates
zabbix4.0 redis monitor templates

## 1.redis-cli run success
```
[root@centos ~]# redis-cli -h 127.0.0.1 -p 6379 -a redispwd info
Warning: Using a password with '-a' or '-u' option on the command line interface may not be safe.
# Server
redis_version:5.0.5
redis_git_sha1:00000000
redis_git_dirty:0
redis_build_id:ba67cab96bf0dfae
...
```
## 2.redis-cli run success
```
[root@centos ~]# redis-cli -h 127.0.0.1 -p 6379 -a redispwd info 2>/dev/null | grep $1":" | cut -d ':' -f 2
5.0.5
00000000
0
ba67cab96bf0dfae
...
```
## 3./etc/zabbix/zabbix_agentd.d/userparameter_redis.conf
```
UserParameter=redis.info[*],redis-cli -h 127.0.0.1 -p 6379 -a redispwd info 2>/dev/null | grep $1":" | cut -d ':' -f 2
```
## 4.import zbx_redis_templates.xml
Zabbix->Configuration->Templates->import->zbx_redis_templates.xml

## more redis monitor item
Zabbix->Configuration->Templates->Template DB Redis->Items->Create item->Key：redis.info[redis_info_key]

redis_info_key -> redis-cli info key
```
# Server
redis_version:5.0.5
redis_git_sha1:00000000
redis_git_dirty:0
redis_build_id:ba67cab96bf0dfae
redis_mode:standalone
os:Linux 3.10.0-957.21.3.el7.x86_64 x86_64
arch_bits:64
multiplexing_api:epoll
atomicvar_api:atomic-builtin
gcc_version:4.8.5
process_id:6935
run_id:c39b4471e5c3f03704af1a80e53ca1f5cba8f47d
tcp_port:6379
uptime_in_seconds:13459
uptime_in_days:0
hz:10
configured_hz:10
lru_clock:2382694
executable:/root/redis-5.0.5/src/./redis-server
config_file:

# Clients
connected_clients:1
client_recent_max_input_buffer:4
client_recent_max_output_buffer:0
blocked_clients:0

# Memory
used_memory:854152
used_memory_human:834.13K
used_memory_rss:12615680
used_memory_rss_human:12.03M
used_memory_peak:875064
used_memory_peak_human:854.55K
used_memory_peak_perc:97.61%
used_memory_overhead:840942
used_memory_startup:791248
used_memory_dataset:13210
used_memory_dataset_perc:21.00%
allocator_allocated:853600
allocator_active:1064960
allocator_resident:3551232
total_system_memory:6087524352
total_system_memory_human:5.67G
used_memory_lua:37888
used_memory_lua_human:37.00K
used_memory_scripts:0
used_memory_scripts_human:0B
number_of_cached_scripts:0
maxmemory:0
maxmemory_human:0B
maxmemory_policy:noeviction
allocator_frag_ratio:1.25
allocator_frag_bytes:211360
allocator_rss_ratio:3.33
allocator_rss_bytes:2486272
rss_overhead_ratio:3.55
rss_overhead_bytes:9064448
mem_fragmentation_ratio:15.94
mem_fragmentation_bytes:11824408
mem_not_counted_for_evict:0
mem_replication_backlog:0
mem_clients_slaves:0
mem_clients_normal:49694
mem_aof_buffer:0
mem_allocator:jemalloc-5.1.0
active_defrag_running:0
lazyfree_pending_objects:0

# Persistence
loading:0
rdb_changes_since_last_save:0
rdb_bgsave_in_progress:0
rdb_last_save_time:1562650323
rdb_last_bgsave_status:ok
rdb_last_bgsave_time_sec:-1
rdb_current_bgsave_time_sec:-1
rdb_last_cow_size:0
aof_enabled:0
aof_rewrite_in_progress:0
aof_rewrite_scheduled:0
aof_last_rewrite_time_sec:-1
aof_current_rewrite_time_sec:-1
aof_last_bgrewrite_status:ok
aof_last_write_status:ok
aof_last_cow_size:0

# Stats
total_connections_received:639
total_commands_processed:1199
instantaneous_ops_per_sec:0
total_net_input_bytes:23806
total_net_output_bytes:2129737
instantaneous_input_kbps:0.00
instantaneous_output_kbps:0.00
rejected_connections:0
sync_full:0
sync_partial_ok:0
sync_partial_err:0
expired_keys:0
expired_stale_perc:0.00
expired_time_cap_reached_count:0
evicted_keys:0
keyspace_hits:0
keyspace_misses:0
pubsub_channels:0
pubsub_patterns:0
latest_fork_usec:0
migrate_cached_sockets:0
slave_expires_tracked_keys:0
active_defrag_hits:0
active_defrag_misses:0
active_defrag_key_hits:0
active_defrag_key_misses:0

# Replication
role:master
connected_slaves:0
master_replid:fbf458082c8dea1f7f57d97650882388d3ae0d2d
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:0
second_repl_offset:-1
repl_backlog_active:0
repl_backlog_size:1048576
repl_backlog_first_byte_offset:0
repl_backlog_histlen:0

# CPU
used_cpu_sys:11.531416
used_cpu_user:10.018502
used_cpu_sys_children:0.000000
used_cpu_user_children:0.000000

# Cluster
cluster_enabled:0
```


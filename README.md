# vfricou.postgresql

Install, configure and backup postgresql database engine

**Platforms Supported**:

| Platform | Versions |
|----------|----------|
| EL | 8, 9 |

## ⚠️ Requirements

Ansible >= 2.10.

### Ansible collections dependencies

  * community.postgresql
  * community.general

### Ansible role dependencies

  * vfricou.validator

## ⚡ Installation

### Install with Ansible Galaxy requirement file

**requirements.yml** :
```yaml
---
roles:
  - name: vfricou.postgresql
    src: git@github.com:vfricou/ansible_role_postgresql.git
    version: master
    scm: git
collections:
  - name: community.postgresql
  - name: community.general
```

```shell
ansible-galaxy role install -r requirements.yml
ansible-galaxy collection install -r requirements.yml
```

### Install with git

If you do not want a global installation, clone it into your `roles_path`.

```shell
git clone git@github.com:vfricou/ansible_role_postgresql.git  vfricou.postgresql
```

As the role is not managed by Ansible Galaxy, you do not have to specify the
github user account.

### ✏️ Example Playbook

Basic usage is:

```yaml
- hosts: all
  roles:
    - role: vfricou.postgresql
      vars:
        pg_bkp_base_path: /srv/exploit/backup/postgres
        pg_bkp_conf_target_dir: '{{ pg_bkp_base_path }}/conf'
        pg_bkp_dump_target_dir: '{{ pg_bkp_base_path }}/dump'
        postgres_listen_addr: 127.0.0.1
        postgres_listen_port: '5432'
        postgres_ssl_enable: true
        postgres_ssl_prefer_server_ciphers: true
        postgres_version: '15'
        
```

## ⚙️ Role Variables

Variables are divided in three types.

The **default vars** section shows you which variables you may
override in your ansible inventory. As a matter of fact, all variables should
be defined there for explicitness, ease of documentation as well as overall
role manageability.

The **context variables** are shown in section below hint you
on how runtime context may affects role execution.

### Default variables

#### main


<table>
<tr>
<th> Variable Name </td>
<th> Required </td>
<th> Type </td>
<th> Default </td>
<th> Elements </td>
<th> Description </td>
</tr>
<tr>
<td> postgres_version </td>
<td> False </td>
<td> str </td>
<td>

```yaml
15
```

</td>
<td>  </td>
<td> PostgreSQL version to install and manage </td>
</tr>
<tr>
<td> pg_bkp_base_path </td>
<td> False </td>
<td> str </td>
<td>

```yaml
/srv/exploit/backup/postgres
```

</td>
<td>  </td>
<td> Path for postgresql backup configuration and archives </td>
</tr>
<tr>
<td> pg_bkp_dump_target_dir </td>
<td> False </td>
<td> str </td>
<td>

```yaml
{{ pg_bkp_base_path }}/dump
```

</td>
<td>  </td>
<td> Path for postgresql databases dumps </td>
</tr>
<tr>
<td> pg_bkp_conf_target_dir </td>
<td> False </td>
<td> str </td>
<td>

```yaml
{{ pg_bkp_base_path }}/conf
```

</td>
<td>  </td>
<td> Path for postgresql database backup configuration </td>
</tr>
<tr>
<td> postgres_acl </td>
<td> False </td>
<td> list </td>
<td>

```yaml

```

</td>
<td> list[dict] </td>
<td> Engine ACL deployed in pg_hba.conf file (see #Variable postgres_acl examples) </td>
</tr>
<tr>
<td> postgres_listen_addr </td>
<td> False </td>
<td> str </td>
<td>

```yaml
127.0.0.1
```

</td>
<td>  </td>
<td> PostgreSQL engine listening addresses (comma separated) </td>
</tr>
<tr>
<td> postgres_listen_port </td>
<td> False </td>
<td> str </td>
<td>

```yaml
5432
```

</td>
<td>  </td>
<td> PostgreSQL engine listening port </td>
</tr>
<tr>
<td> postgres_max_connections </td>
<td> False </td>
<td> str </td>
<td>

```yaml
100
```

</td>
<td>  </td>
<td> Max allowed simultaneous connections </td>
</tr>
<tr>
<td> postgres_password_encryption </td>
<td> False </td>
<td> str </td>
<td>

```yaml
scram-sha-256
```

</td>
<td>  </td>
<td> Default password hash method </td>
</tr>
<tr>
<td> postgres_db_user_namespace </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Default user namespace at logon </td>
</tr>
<tr>
<td> postgres_ssl_enable </td>
<td> False </td>
<td> bool </td>
<td>

```yaml
True
```

</td>
<td>  </td>
<td> Enable engine TLS terminisons </td>
</tr>
<tr>
<td> postgres_ssl_ca_file </td>
<td> False </td>
<td> str </td>
<td>

```yaml

```

</td>
<td>  </td>
<td> Specify TLS CA certificate file path </td>
</tr>
<tr>
<td> postgres_ssl_cert_file </td>
<td> False </td>
<td> str </td>
<td>

```yaml
/etc/ssl/certs/ssl-cert-snakeoil.pem
```

</td>
<td>  </td>
<td> Speficy TLS public certificate file path </td>
</tr>
<tr>
<td> postgres_ssl_crl_file </td>
<td> False </td>
<td> str </td>
<td>

```yaml

```

</td>
<td>  </td>
<td> Specify TLS CRL file path </td>
</tr>
<tr>
<td> postgres_ssl_crl_dir </td>
<td> False </td>
<td> str </td>
<td>

```yaml

```

</td>
<td>  </td>
<td> Specify TLS CRL directory path containing CRL files </td>
</tr>
<tr>
<td> postgres_ssl_key_file </td>
<td> False </td>
<td> str </td>
<td>

```yaml
/etc/ssl/private/ssl-cert-snakeoil.key
```

</td>
<td>  </td>
<td> Specify TLS private key file path </td>
</tr>
<tr>
<td> postgres_ssl_ciphers </td>
<td> False </td>
<td> str </td>
<td>

```yaml
HIGH:!aNULL
```

</td>
<td>  </td>
<td> Speficy TLS server side allowed ciphers </td>
</tr>
<tr>
<td> postgres_ssl_prefer_server_ciphers </td>
<td> False </td>
<td> bool </td>
<td>

```yaml
True
```

</td>
<td>  </td>
<td> Indicate than TLS protocol must match servers ciphers order </td>
</tr>
<tr>
<td> postgres_ssl_ecdh_curve </td>
<td> False </td>
<td> str </td>
<td>

```yaml
prime256v1
```

</td>
<td>  </td>
<td>  </td>
</tr>
<tr>
<td> postgres_ssl_min_vers </td>
<td> False </td>
<td> str </td>
<td>

```yaml
TLSv1.2
```

</td>
<td>  </td>
<td> Specify minimal TLS protocol version for connections </td>
</tr>
<tr>
<td> postgres_ssl_dh_params_file </td>
<td> False </td>
<td> str </td>
<td>

```yaml

```

</td>
<td>  </td>
<td> Specify Diffie-Hellman file path for non curves protocols. Autogenerated if not specified </td>
</tr>
<tr>
<td> postgres_shared_buffers </td>
<td> False </td>
<td> str </td>
<td>

```yaml
128MB
```

</td>
<td>  </td>
<td> Match PostgreSQL `shared_buffers` option </td>
</tr>
<tr>
<td> postgres_temp_buffers </td>
<td> False </td>
<td> str </td>
<td>

```yaml
8MB
```

</td>
<td>  </td>
<td> Match PostgreSQL `temp_buffers` option </td>
</tr>
<tr>
<td> postgres_max_prepared_transactions </td>
<td> False </td>
<td> int </td>
<td>

```yaml
0
```

</td>
<td>  </td>
<td> Match PostgreSQL `max_prepared_transactions` option </td>
</tr>
<tr>
<td> postgres_work_mem </td>
<td> False </td>
<td> str </td>
<td>

```yaml
4MB
```

</td>
<td>  </td>
<td> Match PostgreSQL `work_mem` option </td>
</tr>
<tr>
<td> postgres_maintenance_work_mem </td>
<td> False </td>
<td> str </td>
<td>

```yaml
64MB
```

</td>
<td>  </td>
<td> Match PostgreSQL `maintenance_work_mem` option </td>
</tr>
<tr>
<td> postgres_autovacuum_work_mem </td>
<td> False </td>
<td> str </td>
<td>

```yaml
-1
```

</td>
<td>  </td>
<td> Match PostgreSQL `autovacuum_work_mem` option </td>
</tr>
<tr>
<td> postgres_logical_decoding_work_mem </td>
<td> False </td>
<td> str </td>
<td>

```yaml
64MB
```

</td>
<td>  </td>
<td> Match PostgreSQL `logical_decoding_work_mem` option </td>
</tr>
<tr>
<td> postgres_max_stack_depth </td>
<td> False </td>
<td> str </td>
<td>

```yaml
100kB
```

</td>
<td>  </td>
<td> Match PostgreSQL `max_stack_depth` option </td>
</tr>
<tr>
<td> postgres_shared_memory_type </td>
<td> False </td>
<td> str </td>
<td>

```yaml
mmap
```

</td>
<td>  </td>
<td> Match PostgreSQL `shared_memory_type` option </td>
</tr>
<tr>
<td> postgres_dynamic_shared_memory_type </td>
<td> False </td>
<td> str </td>
<td>

```yaml
posix
```

</td>
<td>  </td>
<td> Match PostgreSQL `dynamic_shared_memory_type` option </td>
</tr>
<tr>
<td> postgres_min_dynamic_shared_memory </td>
<td> False </td>
<td> str </td>
<td>

```yaml
0MB
```

</td>
<td>  </td>
<td> Match PostgreSQL `min_dynamic_shared_memory` option </td>
</tr>
<tr>
<td> postgres_max_files_per_process </td>
<td> False </td>
<td> int </td>
<td>

```yaml
1000
```

</td>
<td>  </td>
<td> Match PostgreSQL `max_files_per_process` option </td>
</tr>
<tr>
<td> postgres_vacuum_cost_delay </td>
<td> False </td>
<td> int </td>
<td>

```yaml
0
```

</td>
<td>  </td>
<td> Match PostgreSQL `vacuum_cost_delay` option </td>
</tr>
<tr>
<td> postgres_vacuum_cost_page_hit </td>
<td> False </td>
<td> int </td>
<td>

```yaml
1
```

</td>
<td>  </td>
<td> Match PostgreSQL `vacuum_cost_page_hit` option </td>
</tr>
<tr>
<td> postgres_vacuum_cost_page_miss </td>
<td> False </td>
<td> int </td>
<td>

```yaml
2
```

</td>
<td>  </td>
<td> Match PostgreSQL `vacuum_cost_page_miss` option </td>
</tr>
<tr>
<td> postgres_vacuum_cost_page_dirty </td>
<td> False </td>
<td> int </td>
<td>

```yaml
20
```

</td>
<td>  </td>
<td> Match PostgreSQL `vacuum_cost_page_dirty` option </td>
</tr>
<tr>
<td> postgres_vacuum_cost_limit </td>
<td> False </td>
<td> int </td>
<td>

```yaml
200
```

</td>
<td>  </td>
<td> Match PostgreSQL `vacuum_cost_limit` option </td>
</tr>
<tr>
<td> postgres_bgwriter_delay </td>
<td> False </td>
<td> str </td>
<td>

```yaml
200ms
```

</td>
<td>  </td>
<td> Match PostgreSQL `bgwriter_delay` option </td>
</tr>
<tr>
<td> postgres_bgwriter_lru_maxpages </td>
<td> False </td>
<td> int </td>
<td>

```yaml
100
```

</td>
<td>  </td>
<td> Match PostgreSQL `bgwriter_lru_maxpages` option </td>
</tr>
<tr>
<td> postgres_bgwriter_lru_multiplier </td>
<td> False </td>
<td> str </td>
<td>

```yaml
2.0
```

</td>
<td>  </td>
<td> Match PostgreSQL `bgwriter_lru_multiplier` option </td>
</tr>
<tr>
<td> postgres_bgwriter_flush_after </td>
<td> False </td>
<td> str </td>
<td>

```yaml
512kB
```

</td>
<td>  </td>
<td> Match PostgreSQL `bgwriter_flush_after` option </td>
</tr>
<tr>
<td> postgres_backend_flush_after </td>
<td> False </td>
<td> int </td>
<td>

```yaml
0
```

</td>
<td>  </td>
<td> Match PostgreSQL `backend_flush_after` option </td>
</tr>
<tr>
<td> postgres_effective_io_concurrency </td>
<td> False </td>
<td> int </td>
<td>

```yaml
1
```

</td>
<td>  </td>
<td> Match PostgreSQL `effective_ip_concurrency` option </td>
</tr>
<tr>
<td> postgres_maintenance_io_concurrency </td>
<td> False </td>
<td> int </td>
<td>

```yaml
10
```

</td>
<td>  </td>
<td> Match PostgreSQL `maintenance_ip_concurrency` option </td>
</tr>
<tr>
<td> postgres_max_worker_processes </td>
<td> False </td>
<td> int </td>
<td>

```yaml
8
```

</td>
<td>  </td>
<td> Match PostgreSQL `max_worker_process` option </td>
</tr>
<tr>
<td> postgres_max_parallel_workers_per_gather </td>
<td> False </td>
<td> int </td>
<td>

```yaml
2
```

</td>
<td>  </td>
<td> Match PostgreSQL `max parallel_workers_per_gather` option </td>
</tr>
<tr>
<td> postgres_max_parallel_maintenance_workers </td>
<td> False </td>
<td> int </td>
<td>

```yaml
2
```

</td>
<td>  </td>
<td> Match PostgreSQL `max_parallel_maintenance_workers` option </td>
</tr>
<tr>
<td> postgres_max_parallel_workers </td>
<td> False </td>
<td> int </td>
<td>

```yaml
8
```

</td>
<td>  </td>
<td> Match PostgreSQL `max_parallel_workers` option </td>
</tr>
<tr>
<td> postgres_parallel_leader_participation </td>
<td> False </td>
<td> str </td>
<td>

```yaml
on
```

</td>
<td>  </td>
<td> Match PostgreSQL `parallel_leader_participation` option </td>
</tr>
<tr>
<td> postgres_old_snapshot_threshold </td>
<td> False </td>
<td> str </td>
<td>

```yaml
-1
```

</td>
<td>  </td>
<td> Match PostgreSQL `old_snapshot_threshold` option </td>
</tr>
<tr>
<td> postgres_wal_level </td>
<td> False </td>
<td> str </td>
<td>

```yaml
replica
```

</td>
<td>  </td>
<td> Match PostgreSQL `wal_level` option </td>
</tr>
<tr>
<td> postgres_wal_log_hints </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `wal_log_hints` option </td>
</tr>
<tr>
<td> postgres_wal_compression </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `wal_compression` option </td>
</tr>
<tr>
<td> postgres_wal_buffers </td>
<td> False </td>
<td> str </td>
<td>

```yaml
-1
```

</td>
<td>  </td>
<td> Match PostgreSQL `wal_buffers` option </td>
</tr>
<tr>
<td> postgres_wal_writer_delay </td>
<td> False </td>
<td> str </td>
<td>

```yaml
200ms
```

</td>
<td>  </td>
<td> Match PostgreSQL `wal_writer_delay` option </td>
</tr>
<tr>
<td> postgres_wal_writer_flush_after </td>
<td> False </td>
<td> str </td>
<td>

```yaml
1MB
```

</td>
<td>  </td>
<td> Match PostgreSQL `wal_writer_flush_after` option </td>
</tr>
<tr>
<td> postgres_wal_skip_threshold </td>
<td> False </td>
<td> str </td>
<td>

```yaml
2MB
```

</td>
<td>  </td>
<td> Match PostgreSQL `wal_skip_threshold` option </td>
</tr>
<tr>
<td> postgres_commit_delay </td>
<td> False </td>
<td> int </td>
<td>

```yaml
0
```

</td>
<td>  </td>
<td> Match PostgreSQL `commit_delay` option </td>
</tr>
<tr>
<td> postgres_commit_siblings </td>
<td> False </td>
<td> int </td>
<td>

```yaml
5
```

</td>
<td>  </td>
<td> Match PostgreSQL `commit_siblings` option </td>
</tr>
<tr>
<td> postgres_checkpoint_timeout </td>
<td> False </td>
<td> str </td>
<td>

```yaml
5min
```

</td>
<td>  </td>
<td> Match PostgreSQL `checkpoint_timeout` option </td>
</tr>
<tr>
<td> postgres_checkpoint_completion_target </td>
<td> False </td>
<td> int </td>
<td>

```yaml
0.9
```

</td>
<td>  </td>
<td> Match PostgreSQL `checkpoint_completion_target` option </td>
</tr>
<tr>
<td> postgres_checkpoint_flush_after </td>
<td> False </td>
<td> str </td>
<td>

```yaml
256kB
```

</td>
<td>  </td>
<td> Match PostgreSQL `checkpoint_flush_after` option </td>
</tr>
<tr>
<td> postgres_checkpoint_warning </td>
<td> False </td>
<td> str </td>
<td>

```yaml
30s
```

</td>
<td>  </td>
<td> Match PostgreSQL `checkpoint_warning` option </td>
</tr>
<tr>
<td> postgres_max_wal_size </td>
<td> False </td>
<td> str </td>
<td>

```yaml
1GB
```

</td>
<td>  </td>
<td> Match PostgreSQL `max_wal_size` option </td>
</tr>
<tr>
<td> postgres_min_wal_size </td>
<td> False </td>
<td> str </td>
<td>

```yaml
80MB
```

</td>
<td>  </td>
<td> Match PostgreSQL `min_wal_size` option </td>
</tr>
<tr>
<td> postgres_enable_gathermerge </td>
<td> False </td>
<td> str </td>
<td>

```yaml
on
```

</td>
<td>  </td>
<td> Match PostgreSQL `enable_gathermerge` option </td>
</tr>
<tr>
<td> postgres_enable_parallel_append </td>
<td> False </td>
<td> str </td>
<td>

```yaml
on
```

</td>
<td>  </td>
<td> Match PostgreSQL `enable_parallel_append` option </td>
</tr>
<tr>
<td> postgres_enable_parallel_hash </td>
<td> False </td>
<td> str </td>
<td>

```yaml
on
```

</td>
<td>  </td>
<td> Match PostgreSQL `enable_parallel_hash` option </td>
</tr>
<tr>
<td> postgres_enable_partition_pruning </td>
<td> False </td>
<td> str </td>
<td>

```yaml
on
```

</td>
<td>  </td>
<td> Match PostgreSQL `enable_partition_pruning` option </td>
</tr>
<tr>
<td> postgres_enable_partitionwise_join </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `enable_partitionwise_join` option </td>
</tr>
<tr>
<td> postgres_enable_partitionwise_aggregate </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `enable_partitionwise_aggregate` option </td>
</tr>
<tr>
<td> postgres_enable_incremental_sort </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `enable_incremental_sort` option </td>
</tr>
<tr>
<td> postgres_enable_async_append </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `enable_async_append` option </td>
</tr>
<tr>
<td> postgres_enable_memoize </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `enable_memoize` option </td>
</tr>
<tr>
<td> postgres_enable_bitmapscan </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `enable_bitmapscan` option </td>
</tr>
<tr>
<td> postgres_enable_hashagg </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `enable_hashagg` option </td>
</tr>
<tr>
<td> postgres_enable_hashjoin </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `enable_hashjoin` option </td>
</tr>
<tr>
<td> postgres_enable_indexscan </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `enable_indexscan` option </td>
</tr>
<tr>
<td> postgres_enable_indexonlyscan </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `enable_indexonlyscan` option </td>
</tr>
<tr>
<td> postgres_enable_material </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `enable_material` option </td>
</tr>
<tr>
<td> postgres_enable_mergejoin </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `enable_mergejoin` option </td>
</tr>
<tr>
<td> postgres_enable_nestloop </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `enable_nestloop` option </td>
</tr>
<tr>
<td> postgres_enable_seqscan </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `enable_seqscan` option </td>
</tr>
<tr>
<td> postgres_enable_sort </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `enable_sort` option </td>
</tr>
<tr>
<td> postgres_enable_tidscan </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `enable_tidscan` option </td>
</tr>
<tr>
<td> postgres_seq_page_cost </td>
<td> False </td>
<td> int </td>
<td>

```yaml
1.0
```

</td>
<td>  </td>
<td> Match PostgreSQL `seq_page_cost` option </td>
</tr>
<tr>
<td> postgres_random_page_cost </td>
<td> False </td>
<td> int </td>
<td>

```yaml
4.0
```

</td>
<td>  </td>
<td> Match PostgreSQL `random_page_cost` option </td>
</tr>
<tr>
<td> postgres_cpu_tuple_cost </td>
<td> False </td>
<td> int </td>
<td>

```yaml
0.01
```

</td>
<td>  </td>
<td> Match PostgreSQL `cpu_tuple_cost` option </td>
</tr>
<tr>
<td> postgres_cpu_index_tuple_cost </td>
<td> False </td>
<td> int </td>
<td>

```yaml
0.005
```

</td>
<td>  </td>
<td> Match PostgreSQL `cpu_index_tuple_cost` option </td>
</tr>
<tr>
<td> postgres_cpu_operator_cost </td>
<td> False </td>
<td> int </td>
<td>

```yaml
0.0025
```

</td>
<td>  </td>
<td> Match PostgreSQL `cpu_operator_cost` option </td>
</tr>
<tr>
<td> postgres_parallel_setup_cost </td>
<td> False </td>
<td> int </td>
<td>

```yaml
1000.0
```

</td>
<td>  </td>
<td> Match PostgreSQL `parallel_setup_cost` option </td>
</tr>
<tr>
<td> postgres_parallel_tuple_cost </td>
<td> False </td>
<td> int </td>
<td>

```yaml
0.1
```

</td>
<td>  </td>
<td> Match PostgreSQL `parallel_tuple_cost` option </td>
</tr>
<tr>
<td> postgres_min_parallel_table_scan_size </td>
<td> False </td>
<td> str </td>
<td>

```yaml
8MB
```

</td>
<td>  </td>
<td> Match PostgreSQL `min_parallel_table_scan_size` option </td>
</tr>
<tr>
<td> postgres_min_parallel_index_scan_size </td>
<td> False </td>
<td> str </td>
<td>

```yaml
512kB
```

</td>
<td>  </td>
<td> Match PostgreSQL `min_parallel_index_scan_size` option </td>
</tr>
<tr>
<td> postgres_effective_cache_size </td>
<td> False </td>
<td> str </td>
<td>

```yaml
4GB
```

</td>
<td>  </td>
<td> Match PostgreSQL `effective_cache_size` option </td>
</tr>
<tr>
<td> postgres_jit_above_cost </td>
<td> False </td>
<td> int </td>
<td>

```yaml
100000
```

</td>
<td>  </td>
<td> Match PostgreSQL `jit_above_cost` option </td>
</tr>
<tr>
<td> postgres_jit_inline_above_cost </td>
<td> False </td>
<td> int </td>
<td>

```yaml
500000
```

</td>
<td>  </td>
<td> Match PostgreSQL `jit_inline_above_cost` option </td>
</tr>
<tr>
<td> postgres_jit_optimize_above_cost </td>
<td> False </td>
<td> int </td>
<td>

```yaml
500000
```

</td>
<td>  </td>
<td> Match PostgreSQL `jit_optimize_above_cost` option </td>
</tr>
<tr>
<td> postgres_geqo </td>
<td> False </td>
<td> str </td>
<td>

```yaml
on
```

</td>
<td>  </td>
<td> Match PostgreSQL `geqo` option </td>
</tr>
<tr>
<td> postgres_geqo_threshold </td>
<td> False </td>
<td> int </td>
<td>

```yaml
12
```

</td>
<td>  </td>
<td> Match PostgreSQL `geqo_threshold` option </td>
</tr>
<tr>
<td> postgres_geqo_effort </td>
<td> False </td>
<td> int </td>
<td>

```yaml
5
```

</td>
<td>  </td>
<td> Match PostgreSQL `geqo_effort` option </td>
</tr>
<tr>
<td> postgres_geqo_pool_size </td>
<td> False </td>
<td> int </td>
<td>

```yaml
0
```

</td>
<td>  </td>
<td> Match PostgreSQL `geqo_pool_size` option </td>
</tr>
<tr>
<td> postgres_geqo_generations </td>
<td> False </td>
<td> int </td>
<td>

```yaml
0
```

</td>
<td>  </td>
<td> Match PostgreSQL `geqo_generations` option </td>
</tr>
<tr>
<td> postgres_geqo_selection_bias </td>
<td> False </td>
<td> int </td>
<td>

```yaml
2.0
```

</td>
<td>  </td>
<td> Match PostgreSQL `geqo_selection_bias` option </td>
</tr>
<tr>
<td> postgres_geqo_seed </td>
<td> False </td>
<td> int </td>
<td>

```yaml
0.0
```

</td>
<td>  </td>
<td> Match PostgreSQL `geqo_seed` option </td>
</tr>
<tr>
<td> postgres_default_statistics_target </td>
<td> False </td>
<td> int </td>
<td>

```yaml
100
```

</td>
<td>  </td>
<td> Match PostgreSQL `default_statistics_target` option </td>
</tr>
<tr>
<td> postgres_constraint_exclusion </td>
<td> False </td>
<td> str </td>
<td>

```yaml
partition
```

</td>
<td>  </td>
<td> Match PostgreSQL `constraint_exclusion` option </td>
</tr>
<tr>
<td> postgres_cursor_tuple_fraction </td>
<td> False </td>
<td> int </td>
<td>

```yaml
0.1
```

</td>
<td>  </td>
<td> Match PostgreSQL `cursor_tuple_fraction` option </td>
</tr>
<tr>
<td> postgres_from_collapse_limit </td>
<td> False </td>
<td> int </td>
<td>

```yaml
8
```

</td>
<td>  </td>
<td> Match PostgreSQL `from_collapse_limit` option </td>
</tr>
<tr>
<td> postgres_join_collapse_limit </td>
<td> False </td>
<td> int </td>
<td>

```yaml
8
```

</td>
<td>  </td>
<td> Match PostgreSQL `join_collapse_limit` option </td>
</tr>
<tr>
<td> postgres_plan_cache_mode </td>
<td> False </td>
<td> str </td>
<td>

```yaml
auto
```

</td>
<td>  </td>
<td> Match PostgreSQL `plan_cache_mode` option </td>
</tr>
<tr>
<td> postgres_recursive_worktable_factor </td>
<td> False </td>
<td> int </td>
<td>

```yaml
10.0
```

</td>
<td>  </td>
<td> Match PostgreSQL `recursive_worktable_factor` option </td>
</tr>
<tr>
<td> postgres_log_destination </td>
<td> False </td>
<td> str </td>
<td>

```yaml
stderr
```

</td>
<td>  </td>
<td> Match PostgreSQL `log_destination` option </td>
</tr>
<tr>
<td> postgres_logging_collector </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `logging_collector` option </td>
</tr>
<tr>
<td> postgres_log_directory </td>
<td> False </td>
<td> str </td>
<td>

```yaml
log
```

</td>
<td>  </td>
<td> Match PostgreSQL `log_directory` option </td>
</tr>
<tr>
<td> postgres_log_filename </td>
<td> False </td>
<td> str </td>
<td>

```yaml
postgresql-%Y-%m-%d_%H%M%S.log
```

</td>
<td>  </td>
<td> Match PostgreSQL `log_filename` option </td>
</tr>
<tr>
<td> postgres_log_file_mode </td>
<td> False </td>
<td> str </td>
<td>

```yaml
0600
```

</td>
<td>  </td>
<td> Match PostgreSQL `log_file_mode` option </td>
</tr>
<tr>
<td> postgres_log_rotation_age </td>
<td> False </td>
<td> str </td>
<td>

```yaml
1d
```

</td>
<td>  </td>
<td> Match PostgreSQL `log_rotation_age` option </td>
</tr>
<tr>
<td> postgres_log_rotation_size </td>
<td> False </td>
<td> str </td>
<td>

```yaml
10MB
```

</td>
<td>  </td>
<td> Match PostgreSQL `log_rotation_size` option </td>
</tr>
<tr>
<td> postgres_log_truncate_on_rotation </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `log_truncate_on_rotation` option </td>
</tr>
<tr>
<td> postgres_syslog_facility </td>
<td> False </td>
<td> str </td>
<td>

```yaml
LOCAL0
```

</td>
<td>  </td>
<td> Match PostgreSQL `syslog_facility` option </td>
</tr>
<tr>
<td> postgres_syslog_ident </td>
<td> False </td>
<td> str </td>
<td>

```yaml
postgres
```

</td>
<td>  </td>
<td> Match PostgreSQL `syslog_ident` option </td>
</tr>
<tr>
<td> postgres_syslog_sequence_numbers </td>
<td> False </td>
<td> str </td>
<td>

```yaml
on
```

</td>
<td>  </td>
<td> Match PostgreSQL `syslog_sequence_numbers` option </td>
</tr>
<tr>
<td> postgres_syslog_split_messages </td>
<td> False </td>
<td> str </td>
<td>

```yaml
on
```

</td>
<td>  </td>
<td> Match PostgreSQL `syslog_split_messages` option </td>
</tr>
<tr>
<td> postgres_log_min_message </td>
<td> False </td>
<td> str </td>
<td>

```yaml
warning
```

</td>
<td>  </td>
<td> Match PostgreSQL `log_min_message` option </td>
</tr>
<tr>
<td> postgres_log_min_error_statement </td>
<td> False </td>
<td> str </td>
<td>

```yaml
error
```

</td>
<td>  </td>
<td> Match PostgreSQL `log_min_error_statement` option </td>
</tr>
<tr>
<td> postgres_log_min_duration_statement </td>
<td> False </td>
<td> int </td>
<td>

```yaml
2000
```

</td>
<td>  </td>
<td> Match PostgreSQL `log_min_duration_statement` option </td>
</tr>
<tr>
<td> postgres_log_min_duration_sample </td>
<td> False </td>
<td> int </td>
<td>

```yaml
-1
```

</td>
<td>  </td>
<td> Match PostgreSQL `log_min_duration_sample` option </td>
</tr>
<tr>
<td> postgres_log_statement_sample_rate </td>
<td> False </td>
<td> int </td>
<td>

```yaml
1.0
```

</td>
<td>  </td>
<td> Match PostgreSQL `log_statement_sample_rate` option </td>
</tr>
<tr>
<td> postgres_log_transaction_sample_rate </td>
<td> False </td>
<td> int </td>
<td>

```yaml
0.0
```

</td>
<td>  </td>
<td> Match PostgreSQL `log_transaction_sample_rate` option </td>
</tr>
<tr>
<td> postgres_log_startup_progress_interval </td>
<td> False </td>
<td> int </td>
<td>

```yaml
10s
```

</td>
<td>  </td>
<td> Match PostgreSQL `log_startup_progress_interval` option </td>
</tr>
<tr>
<td> postgres_debug_print_parse </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `debug_print_parse` option </td>
</tr>
<tr>
<td> postgres_debug_print_rewritten </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `debug_print_rewritten` option </td>
</tr>
<tr>
<td> postgres_debug_print_plan </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `debug_print_plan` option </td>
</tr>
<tr>
<td> postgres_debug_pretty_print </td>
<td> False </td>
<td> str </td>
<td>

```yaml
on
```

</td>
<td>  </td>
<td> Match PostgreSQL `debug_pretty_print` option </td>
</tr>
<tr>
<td> postgres_log_autovacuum_min_durication </td>
<td> False </td>
<td> str </td>
<td>

```yaml
10min
```

</td>
<td>  </td>
<td> Match PostgreSQL `log_autovacuum_min_durication` option </td>
</tr>
<tr>
<td> postgres_log_checkpoints </td>
<td> False </td>
<td> str </td>
<td>

```yaml
on
```

</td>
<td>  </td>
<td> Match PostgreSQL `log_checkpoints` option </td>
</tr>
<tr>
<td> postgres_log_connections </td>
<td> False </td>
<td> str </td>
<td>

```yaml
on
```

</td>
<td>  </td>
<td> Match PostgreSQL `log_connections` option </td>
</tr>
<tr>
<td> postgres_log_disconnections </td>
<td> False </td>
<td> str </td>
<td>

```yaml
on
```

</td>
<td>  </td>
<td> Match PostgreSQL `log_disconnections` option </td>
</tr>
<tr>
<td> postgres_log_duration </td>
<td> False </td>
<td> str </td>
<td>

```yaml
on
```

</td>
<td>  </td>
<td> Match PostgreSQL `log_duration` option </td>
</tr>
<tr>
<td> postgres_log_error_verbosity </td>
<td> False </td>
<td> str </td>
<td>

```yaml
default
```

</td>
<td>  </td>
<td> Match PostgreSQL `log_error_verbosity` option </td>
</tr>
<tr>
<td> postgres_log_hostname </td>
<td> False </td>
<td> str </td>
<td>

```yaml
on
```

</td>
<td>  </td>
<td> Match PostgreSQL `log_hostname` option </td>
</tr>
<tr>
<td> postgres_log_line_prefix </td>
<td> False </td>
<td> str </td>
<td>

```yaml
%m [%p] %q%u@%d 
```

</td>
<td>  </td>
<td> Match PostgreSQL `log_line_prefix` option </td>
</tr>
<tr>
<td> postgres_log_lock_waits </td>
<td> False </td>
<td> str </td>
<td>

```yaml
on
```

</td>
<td>  </td>
<td> Match PostgreSQL `log_lock_waits` option </td>
</tr>
<tr>
<td> postgres_log_recovery_conflict_waits </td>
<td> False </td>
<td> str </td>
<td>

```yaml
on
```

</td>
<td>  </td>
<td> Match PostgreSQL `log_recovery_conflict_waits` option </td>
</tr>
<tr>
<td> postgres_log_parameter_max_lenght </td>
<td> False </td>
<td> int </td>
<td>

```yaml
-1
```

</td>
<td>  </td>
<td> Match PostgreSQL `log_parameter_max_lenght` option </td>
</tr>
<tr>
<td> postgres_log_parameter_max_length_on_error </td>
<td> False </td>
<td> int </td>
<td>

```yaml
-1
```

</td>
<td>  </td>
<td> Match PostgreSQL `log_parameter_max_length_on_error` option </td>
</tr>
<tr>
<td> postgres_log_statement </td>
<td> False </td>
<td> str </td>
<td>

```yaml
none
```

</td>
<td>  </td>
<td> Match PostgreSQL `log_statement` option </td>
</tr>
<tr>
<td> postgres_log_temp_files </td>
<td> False </td>
<td> int </td>
<td>

```yaml
-1
```

</td>
<td>  </td>
<td> Match PostgreSQL `log_temp_files` option </td>
</tr>
<tr>
<td> postgres_cluster_name </td>
<td> False </td>
<td> str </td>
<td>

```yaml
{{ postgres_version }}/main
```

</td>
<td>  </td>
<td> Define PostgreSQL cluster name </td>
</tr>
<tr>
<td> postgres_update_process_title </td>
<td> False </td>
<td> str </td>
<td>

```yaml

```

</td>
<td>  </td>
<td> Match PostgreSQL `update_process_title` option </td>
</tr>
<tr>
<td> postgres_track_activities </td>
<td> False </td>
<td> str </td>
<td>

```yaml
on
```

</td>
<td>  </td>
<td> Match PostgreSQL `track_activities` option </td>
</tr>
<tr>
<td> postgres_track_activity_query_size </td>
<td> False </td>
<td> int </td>
<td>

```yaml
1024
```

</td>
<td>  </td>
<td> Match PostgreSQL `track_activity_query_size` option </td>
</tr>
<tr>
<td> postgres_track_counts </td>
<td> False </td>
<td> str </td>
<td>

```yaml
on
```

</td>
<td>  </td>
<td> Match PostgreSQL `track_counts` option </td>
</tr>
<tr>
<td> postgres_track_io_timing </td>
<td> False </td>
<td> str </td>
<td>

```yaml
on
```

</td>
<td>  </td>
<td> Match PostgreSQL `track_io_timing` option </td>
</tr>
<tr>
<td> postgres_track_wal_io_timing </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `track_wal_io_timing` option </td>
</tr>
<tr>
<td> postgres_track_functions </td>
<td> False </td>
<td> str </td>
<td>

```yaml
none
```

</td>
<td>  </td>
<td> Match PostgreSQL `track_functions` option </td>
</tr>
<tr>
<td> postgres_stats_fetch_consistency </td>
<td> False </td>
<td> str </td>
<td>

```yaml
cache
```

</td>
<td>  </td>
<td> Match PostgreSQL `stats_fetch_consistency` option </td>
</tr>
<tr>
<td> postgres_compute_query_id </td>
<td> False </td>
<td> str </td>
<td>

```yaml
auto
```

</td>
<td>  </td>
<td> Match PostgreSQL `compute_query_id` option </td>
</tr>
<tr>
<td> postgres_log_statement_stats </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `log_statement_stats` option </td>
</tr>
<tr>
<td> postgres_log_parser_stats </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `log_parsers_stats` option </td>
</tr>
<tr>
<td> postgres_log_planner_stats </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `log_planner_stats` option </td>
</tr>
<tr>
<td> postgres_log_executor_stats </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `log_executor_stats` option </td>
</tr>
<tr>
<td> postgres_autovacuum </td>
<td> False </td>
<td> str </td>
<td>

```yaml
on
```

</td>
<td>  </td>
<td> Match PostgreSQL `autovacuum` option </td>
</tr>
<tr>
<td> postgres_autovacuum_max_workers </td>
<td> False </td>
<td> int </td>
<td>

```yaml
3
```

</td>
<td>  </td>
<td> Match PostgreSQL `autovacuum_max_workers` option </td>
</tr>
<tr>
<td> postgres_autovacuum_naptime </td>
<td> False </td>
<td> str </td>
<td>

```yaml
1min
```

</td>
<td>  </td>
<td> Match PostgreSQL `autovacuum_naptime` option </td>
</tr>
<tr>
<td> postgres_autovacuum_vacuum_threshold </td>
<td> False </td>
<td> int </td>
<td>

```yaml
50
```

</td>
<td>  </td>
<td> Match PostgreSQL `autovacuum_vacuum_treshold` option </td>
</tr>
<tr>
<td> postgres_autovacuum_analyze_threshold </td>
<td> False </td>
<td> int </td>
<td>

```yaml
50
```

</td>
<td>  </td>
<td> Match PostgreSQL `autovacuum_analyze_threshold` option </td>
</tr>
<tr>
<td> postgres_autovacuum_vacuum_scale_factor </td>
<td> False </td>
<td> int </td>
<td>

```yaml
0.2
```

</td>
<td>  </td>
<td> Match PostgreSQL `autovacuum_vacuum_scale_factor` option </td>
</tr>
<tr>
<td> postgres_autovacuum_analyze_scale_factor </td>
<td> False </td>
<td> int </td>
<td>

```yaml
0.1
```

</td>
<td>  </td>
<td> Match PostgreSQL `autovacuum_analyze_scale_factor` option </td>
</tr>
<tr>
<td> postgres_autovacuum_freeze_max_age </td>
<td> False </td>
<td> int </td>
<td>

```yaml
200000000
```

</td>
<td>  </td>
<td> Match PostgreSQL `autovacuum_freeze_max_age` option </td>
</tr>
<tr>
<td> postgres_autovacuum_multixact_freeze_max_age </td>
<td> False </td>
<td> int </td>
<td>

```yaml
400000000
```

</td>
<td>  </td>
<td> Match PostgreSQL `autovacuum_multixact_freeze_max_age` option </td>
</tr>
<tr>
<td> postgres_autovacuum_vacuum_cost_delay </td>
<td> False </td>
<td> str </td>
<td>

```yaml
2ms
```

</td>
<td>  </td>
<td> Match PostgreSQL `autovacuum_vacuum_cost_delay` option </td>
</tr>
<tr>
<td> postgres_autovacuum_vacuum_cost_limit </td>
<td> False </td>
<td> int </td>
<td>

```yaml
-1
```

</td>
<td>  </td>
<td> Match PostgreSQL `autovacuum_vacuum_cost_limit` option </td>
</tr>
<tr>
<td> postgres_autovacuum_vacuum_insert_threshold </td>
<td> False </td>
<td> int </td>
<td>

```yaml
1000
```

</td>
<td>  </td>
<td> Match PostgreSQL `autovacuum_vacuum_insert_threshold` option </td>
</tr>
<tr>
<td> postgres_autovacuum_vacuum_insert_scale_factor </td>
<td> False </td>
<td> int </td>
<td>

```yaml
0.2
```

</td>
<td>  </td>
<td> Match PostgreSQL `autovacuum_vacuum_insert_scale_factor` option </td>
</tr>
<tr>
<td> postgres_client_min_message </td>
<td> False </td>
<td> str </td>
<td>

```yaml
notice
```

</td>
<td>  </td>
<td> Match PostgreSQL `client_min_message` option </td>
</tr>
<tr>
<td> postgres_search_path </td>
<td> False </td>
<td> str </td>
<td>

```yaml
"$user", public
```

</td>
<td>  </td>
<td> Match PostgreSQL `search_path` option </td>
</tr>
<tr>
<td> postgres_default_table_access_method </td>
<td> False </td>
<td> str </td>
<td>

```yaml
heap
```

</td>
<td>  </td>
<td> Match PostgreSQL `default_table_access_method` option </td>
</tr>
<tr>
<td> postgres_default_tablespace </td>
<td> False </td>
<td> str </td>
<td>

```yaml

```

</td>
<td>  </td>
<td> Match PostgreSQL `default_tablespace` option </td>
</tr>
<tr>
<td> postgres_default_toast_compression </td>
<td> False </td>
<td> str </td>
<td>

```yaml
pglz
```

</td>
<td>  </td>
<td> Match PostgreSQL `default_toast_compression` option </td>
</tr>
<tr>
<td> postgres_vacuum_failsafe_age </td>
<td> False </td>
<td> int </td>
<td>

```yaml
1600000000
```

</td>
<td>  </td>
<td> Match PostgreSQL `vacuum_failsafe_age` option </td>
</tr>
<tr>
<td> postgres_check_function_bodies </td>
<td> False </td>
<td> str </td>
<td>

```yaml
on
```

</td>
<td>  </td>
<td> Match PostgreSQL `check_function_bodies` option </td>
</tr>
<tr>
<td> postgres_default_transaction_isolation </td>
<td> False </td>
<td> str </td>
<td>

```yaml
read committed
```

</td>
<td>  </td>
<td> Match PostgreSQL `default_transaction_isolation` option </td>
</tr>
<tr>
<td> postgres_default_transaction_read_only </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `default_transaction_read_only` option </td>
</tr>
<tr>
<td> postgres_default_transaction_deferrable </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `default_transaction_deferrable` option </td>
</tr>
<tr>
<td> postgres_session_replication_role </td>
<td> False </td>
<td> str </td>
<td>

```yaml
origin
```

</td>
<td>  </td>
<td> Match PostgreSQL `session_replication_role` option </td>
</tr>
<tr>
<td> postgres_statement_timeout </td>
<td> False </td>
<td> int </td>
<td>

```yaml
0
```

</td>
<td>  </td>
<td> Match PostgreSQL `statement_timeout` option </td>
</tr>
<tr>
<td> postgres_lock_timeout </td>
<td> False </td>
<td> int </td>
<td>

```yaml
0
```

</td>
<td>  </td>
<td> Match PostgreSQL `lock_timeout` option </td>
</tr>
<tr>
<td> postgres_idle_in_transaction_session_timeout </td>
<td> False </td>
<td> int </td>
<td>

```yaml
0
```

</td>
<td>  </td>
<td> Match PostgreSQL `idle_in_transaction_session_timeout` option </td>
</tr>
<tr>
<td> postgres_idle_session_timeout </td>
<td> False </td>
<td> int </td>
<td>

```yaml
0
```

</td>
<td>  </td>
<td> Match PostgreSQL `idle_session_timeout` option </td>
</tr>
<tr>
<td> postgres_vacuum_freeze_table_age </td>
<td> False </td>
<td> int </td>
<td>

```yaml
150000000
```

</td>
<td>  </td>
<td> Match PostgreSQL `vacuum_freeze_table_age` option </td>
</tr>
<tr>
<td> postgres_vacuum_freeze_min_age </td>
<td> False </td>
<td> int </td>
<td>

```yaml
50000000
```

</td>
<td>  </td>
<td> Match PostgreSQL `vacuum_freeze_min_age` option </td>
</tr>
<tr>
<td> postgres_vacuum_multixact_freeze_table_age </td>
<td> False </td>
<td> int </td>
<td>

```yaml
150000000
```

</td>
<td>  </td>
<td> Match PostgreSQL `vacuum_multixact_freeze_table_age` option </td>
</tr>
<tr>
<td> postgres_vacuum_multixact_freeze_min_age </td>
<td> False </td>
<td> int </td>
<td>

```yaml
5000000
```

</td>
<td>  </td>
<td> Match PostgreSQL `vacuum_multixact_freeze_min_age` option </td>
</tr>
<tr>
<td> postgres_vacuum_multixact_failsafe_age </td>
<td> False </td>
<td> int </td>
<td>

```yaml
1600000000
```

</td>
<td>  </td>
<td> Match PostgreSQL `vacuum_multixact_failsafe_age` option </td>
</tr>
<tr>
<td> postgres_bytea_output </td>
<td> False </td>
<td> str </td>
<td>

```yaml
hex
```

</td>
<td>  </td>
<td> Match PostgreSQL `bytea_output` option </td>
</tr>
<tr>
<td> postgres_xmlbinary </td>
<td> False </td>
<td> str </td>
<td>

```yaml
base64
```

</td>
<td>  </td>
<td> Match PostgreSQL `xmlbinary` option </td>
</tr>
<tr>
<td> postgres_xmloption </td>
<td> False </td>
<td> str </td>
<td>

```yaml
content
```

</td>
<td>  </td>
<td> Match PostgreSQL `xmloption` option </td>
</tr>
<tr>
<td> postgres_gin_pending_list_limit </td>
<td> False </td>
<td> str </td>
<td>

```yaml
4MB
```

</td>
<td>  </td>
<td> Match PostgreSQL `gin_pending_list_limit` option </td>
</tr>
<tr>
<td> postgres_datestyle </td>
<td> False </td>
<td> str </td>
<td>

```yaml
iso, mdy
```

</td>
<td>  </td>
<td> Match PostgreSQL `datestyle` option </td>
</tr>
<tr>
<td> postgres_intervalstyle </td>
<td> False </td>
<td> str </td>
<td>

```yaml
postgres
```

</td>
<td>  </td>
<td> Match PostgreSQL `intervalstyle` option </td>
</tr>
<tr>
<td> postgres_timezone </td>
<td> False </td>
<td> str </td>
<td>

```yaml
UTC
```

</td>
<td>  </td>
<td> Define PostgreSQL engine default timezone </td>
</tr>
<tr>
<td> postgres_timezone_abbreviations </td>
<td> False </td>
<td> str </td>
<td>

```yaml
Default
```

</td>
<td>  </td>
<td> Match PostgreSQL `timezone_abbreviations` option </td>
</tr>
<tr>
<td> postgres_client_encoding </td>
<td> False </td>
<td> str </td>
<td>

```yaml
sql_ascii
```

</td>
<td>  </td>
<td> Match PostgreSQL `client_encoding` option </td>
</tr>
<tr>
<td> postgres_locale </td>
<td> False </td>
<td> str </td>
<td>

```yaml
en_US.UTF-8
```

</td>
<td>  </td>
<td> Match PostgreSQL `locale` option </td>
</tr>
<tr>
<td> postgres_default_text_search_config </td>
<td> False </td>
<td> str </td>
<td>

```yaml
pg_catalog.english
```

</td>
<td>  </td>
<td> Match PostgreSQL `default_text_search_config` option </td>
</tr>
<tr>
<td> postgres_local_preload_libraries </td>
<td> False </td>
<td> str </td>
<td>

```yaml

```

</td>
<td>  </td>
<td> Match PostgreSQL `local_preload_libraries` option </td>
</tr>
<tr>
<td> postgres_session_preload_libraries </td>
<td> False </td>
<td> str </td>
<td>

```yaml

```

</td>
<td>  </td>
<td> Match PostgreSQL `session_preload_libraries` option </td>
</tr>
<tr>
<td> postgres_shared_preload_libraries </td>
<td> False </td>
<td> str </td>
<td>

```yaml

```

</td>
<td>  </td>
<td> Match PostgreSQL `shared_preload_libraries` option </td>
</tr>
<tr>
<td> postgres_jit_provider </td>
<td> False </td>
<td> str </td>
<td>

```yaml
llvmjit
```

</td>
<td>  </td>
<td> Match PostgreSQL `jit_provider` option </td>
</tr>
<tr>
<td> postgres_dynamic_library_path </td>
<td> False </td>
<td> str </td>
<td>

```yaml
$libdir
```

</td>
<td>  </td>
<td> Match PostgreSQL `dynamic_library_path` option </td>
</tr>
<tr>
<td> postgres_gin_fuzzy_search_limit </td>
<td> False </td>
<td> int </td>
<td>

```yaml
0
```

</td>
<td>  </td>
<td> Match PostgreSQL `gin_fuzzy_search_limit` option </td>
</tr>
<tr>
<td> postgres_deadlock_timeout </td>
<td> False </td>
<td> str </td>
<td>

```yaml
1s
```

</td>
<td>  </td>
<td> Match PostgreSQL `deadlock_timeout` option </td>
</tr>
<tr>
<td> postgres_max_locks_per_transaction </td>
<td> False </td>
<td> int </td>
<td>

```yaml
64
```

</td>
<td>  </td>
<td> Match PostgreSQL `max_locks_per_transaction` option </td>
</tr>
<tr>
<td> postgres_max_pred_locks_per_transaction </td>
<td> False </td>
<td> int </td>
<td>

```yaml
64
```

</td>
<td>  </td>
<td> Match PostgreSQL `max_pred_locks_per_transaction` option </td>
</tr>
<tr>
<td> postgres_max_pred_locks_per_relation </td>
<td> False </td>
<td> int </td>
<td>

```yaml
-2
```

</td>
<td>  </td>
<td> Match PostgreSQL `max_pred_locks_per_relation` option </td>
</tr>
<tr>
<td> postgres_max_pred_locks_per_page </td>
<td> False </td>
<td> int </td>
<td>

```yaml
2
```

</td>
<td>  </td>
<td> Match PostgreSQL `max_pred_locks_per_page` option </td>
</tr>
<tr>
<td> postgres_array_nulls </td>
<td> False </td>
<td> str </td>
<td>

```yaml
on
```

</td>
<td>  </td>
<td> Match PostgreSQL `array_nulls` option </td>
</tr>
<tr>
<td> postgres_backslash_quote </td>
<td> False </td>
<td> str </td>
<td>

```yaml
safe_encoding
```

</td>
<td>  </td>
<td> Match PostgreSQL `backslash_quote` option </td>
</tr>
<tr>
<td> postgres_escape_string_warning </td>
<td> False </td>
<td> str </td>
<td>

```yaml
on
```

</td>
<td>  </td>
<td> Match PostgreSQL `escape_string_warning` option </td>
</tr>
<tr>
<td> postgres_lo_compat_privileges </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `lo_compat_privileges` option </td>
</tr>
<tr>
<td> postgres_quote_all_identifiers </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `quote_all_identifiers` option </td>
</tr>
<tr>
<td> postgres_standard_conforming_strings </td>
<td> False </td>
<td> str </td>
<td>

```yaml
on
```

</td>
<td>  </td>
<td> Match PostgreSQL `standard_conforming_strings` option </td>
</tr>
<tr>
<td> postgres_synchronize_seqscans </td>
<td> False </td>
<td> str </td>
<td>

```yaml
on
```

</td>
<td>  </td>
<td> Match PostgreSQL `synchronize_seqscans` option </td>
</tr>
<tr>
<td> postgres_transform_null_equals </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `transform_null_equals` option </td>
</tr>
<tr>
<td> postgres_exit_on_error </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `exit_on_error` option </td>
</tr>
<tr>
<td> postgres_restart_after_crash </td>
<td> False </td>
<td> str </td>
<td>

```yaml
on
```

</td>
<td>  </td>
<td> Match PostgreSQL `restart_after_crash` option </td>
</tr>
<tr>
<td> postgres_data_sync_retry </td>
<td> False </td>
<td> str </td>
<td>

```yaml
off
```

</td>
<td>  </td>
<td> Match PostgreSQL `data_sync_retry` option </td>
</tr>
<tr>
<td> postgres_recovery_init_sync_method </td>
<td> False </td>
<td> str </td>
<td>

```yaml
fsync
```

</td>
<td>  </td>
<td> Match PostgreSQL `recovery_init_sync_method` option </td>
</tr>
</table>

### Context variables

Those variables from `vars/*.{yml,json}` are loaded dynamically during task
runtime using the `include_vars` module.

Variables loaded from `vars/main.yml`.

<table>
<tr>
<th> Variable Name </th>
<th> Value </th>
</tr>
<tr>
<td> supported_platforms </td>
<td>

```yaml
- name: Rocky
  versions:
  - 8
  - 9
- name: AlmaLinux
  versions:
  - 8
  - 9
- name: RedHat
  versions:
  - 8
  - 9
- name: Debian
  versions:
  - 11
  - 12

```

</td>
<tr>
<td> packages </td>
<td>

```yaml
debian:
  requirements:
  - apt-transport-https
  - python3-psycopg
rhel:
  requirements:
  - python3-psycopg2

```

</td>
<tr>
<td> debian </td>
<td>

```yaml
repo_config: deb https://apt.postgresql.org/pub/repos/apt {{ ansible_distribution_release
  }}-pgdg main
repo_gpg_url: https://www.postgresql.org/media/keys/ACCC4CF8.asc

```

</td>
<tr>
<td> postgres </td>
<td>

```yaml
debian:
  conf_path: /etc/postgresql
group: postgres
user: postgres

```

</td>
</table>



### Role Requirements File

Additionnals roles requirements
```yaml
---
roles:
  - name: vfricou.validator
    src: git+https://github.com/vfricou/ansible_role_validator.git
    version: master
    scm: git
```


## Additional documentations
#### Variable postgres_acl examples

Example to populate `pg_hba.conf` acls :
```yaml
postgres_acl:
  - database: toto
    type: host
    user: toto
    address: '1.2.3.4/32'
    method: 'scram-sha-256'
```



## Author Information


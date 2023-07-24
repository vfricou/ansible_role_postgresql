### Variable postgres_acl examples

Example to populate `pg_hba.conf` acls :
```yaml
postgres_acl:
  - database: toto
    type: host
    user: toto
    address: '1.2.3.4/32'
    method: 'scram-sha-256'
```

jeffbr13.ipfs-cluster
=====================

Installs and configures the [`ipfs-cluster`](https://github.com/ipfs/ipfs-cluster) daemon.

Unique node IDs and private keys must be configured per-host.

You can use `systemctl status ipfs` and `systemctl status ipfs-cluster` to check the status of the new services.


Requirements
------------

- Ansible 2.2 (for service.use option)


Role Variables
--------------

As in [jeffbr13.ipfs], the IPFS peer ID and private key must be for each host in `host_vars`:

```yaml
ipfs_peer_id: ""      # see below
ipfs_private_key: ""  # ipfs-key | base64
```

You must also generate an `ipfs_cluster_secret` to be shared by all hosts.
The following variables are available across the playbook:

```yaml
ipfs_cluster_secret: ""   # openssl rand -hex 32
ipfs_cluster_dist_url: https://dist.ipfs.io
ipfs_cluster_version: v0.2.1
ipfs_cluster_arch: amd64
ipfs_cluster_replication_factor: -1   # replicate files to all nodes
ipfs_cluster_listen_multiaddress: /ip4/0.0.0.0/tcp/9096
ipfs_cluster_http_api_listen_multiaddress: /ip4/127.0.0.1/tcp/9094
ipfs_cluster_http_gateway_listen_multiaddress: /ip4/127.0.0.1/tcp/9095
```

You can generate the `ipfs_cluster_secret` by running `openssl rand -hex 32`,
or, if you don't have OpenSSL, `od  -vN 32 -An -tx1 /dev/urandom | tr -d ' \n' ; echo`.


Example Playbook
----------------

In your `playbook.yml`:

```yaml
- hosts: ipfs_cluster
  roles:
     - { role: jeffbr13.ipfs-cluster, ipfs_cluster_secret: ed3205fca12ec1584d063f9f16a7b72220f86e49e5c8e94625c0aace6b37d713}
```

For a host in `host_vars/<hostname>.yml`:

```yaml
ipfs_peer_id: Qmagy4195bsbR6YmqwKUtj7j65QdnyDiH3uzVYB8F46r6j
ipfs_private_key: CAASqAkwggSkAgEAAoIBAQDB7ltlNV4QysC3m0HOySU2jjxnmrjZmOX8vi9UU/E6xu+3S6wCe/f1bxVATgqfHMXU4Sk5g4pmM3YocadrMe/WzeSLKGB0QPgcKAtcuBJZO8vQEWmMDxrFg/pOd4Z2LIrLKIQDeRmhBhMmIWQ/M8FNVhzSv6gVs0+X72ZwMQgJ8N5IiJBtzfT0CRddsHaSqiwvRPS2bJSuSUi0Vq1l4+I6sHyP7WgE9IrUQSMVHw3kiKgk8bWKEbW8p5GWXbdYPOfGr+YUd3GtEVvkrpo0OAZcA6H+1DqNAqAQdLu47pA7pzZW4C3nxwisN1wYoEbkE+qXpJQft4+58N1ZAkULbzu/AgMBAAECggEAAnTAV5HLdS78LdcbiEDn5b77aNx+xtK25vKJqum9Pl9SneGpdgaX51XW0Q+r9sPohX+sg/v0fsLcFjsKQcNKJFBLOq/yOMax3blsG2qBYPvu4t21ln6Ceknnm6LL4ydBQr1qnpikCHQJPgxiNqKzKgWTK+AdgtjYgzYW+AjG70lF+t450PtEp2NSPUsYB3EIUTRaPpQeKIQ3z71DkpjReuQ//P+PLLj7/4qzyHH1hkhHP6AgjwCetzH+Tlor0rigpkqY1QTycPmEXoQ5oekEIpGiVaX4LtymHWSIHW/FFEb5dODECwQtLRMulJpu4y86DfAySb9jwfn2JA9NQh5boQKBgQDI7a7DQBP6oJtfmwRhxonMO2L0czTIgZEl32E3JWx49ZY+xnAIvpUB3MZZqAX4vrb8uuvpv2ced4eeSyBAFJHOX8pEpEIfmgV7eg42xMPWr6l4DeXY3sC1SaXUWIzoSQLosD8kBopQNFemskmq5m5/eAdDxLZFa4K27BmmITf9hwKBgQD3FbK6TNoq2yWoxByPY4xmqkTeqh+DME3vBzXUDv8ZKqkVTkF7kFkk3zSsFFk/BS+UALsZKyarERbZ5U9NCscNZeVIukztjJUGCPpntjGM8r8NK3CXtWc+qGHewAgNGXzn6cyNVv29olPJNK0gvDkVou4NwEVMWjzDuFaiLZKeCQKBgQC0Mm1UUCha0iTmBilU4vB8CBqD7ro8w+5/j6kpAtgYVu/q1p5tSTZrWCtPBuBsJ+YGHEEs/eomKb6n2OpQbeIhuki1bLacjs4x4dHTjn2wERQkRhqHd6ZOL4GYQd4FCE2ij0XhMjhjG74sEqL8sPISQXwKa+WntnahRHbwRcRoCwKBgQCERqR5Ih2F5e5iTCLyDJwkdjEKd08Jf3mpZlXF4gVlZrZARrW9vchLegcLvJUOrOsMs9t2HOjFmg9+tUlf+E4Z+RvndH0six9YrMPJc/tQ9r+bAE91mFLec2x5wJpO0P9SdJLic9jBhb6PL9kjdkClOaVxzSYMOx7etLgEeJtOaQKBgAVYOsf2EA3aoukh6mPTKVfKaV71mFRhIPcbT0mADaJ7mYh0fSV/FHahwRioKfweTFNEFVO15x97acBbfInA/ZARc+N08IKVfwr+vopcefXEqgE0PMGsI/fFduXYBbprdns62qGrEYAJkNE8E34AM2Afh9sWt9PJdUYpBagHc+dL
```


License
-------

MIT


Author Information
------------------

This is an Ansible Galaxy distributable role based on <https://github.com/hsanjuan/ansible-ipfs-cluster>.

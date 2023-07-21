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
        postgres_group: postgres
        postgres_user: postgres
        
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
Role default variables from `defaults/main.yml`.

<table>
<tr>
<th> Variable Name </td>
<th> Value </td>
</tr>
<tr>
<td> postgres_user </td>
<td>

```yaml
postgres
```

</td>
</tr>
<tr>
<td> postgres_group </td>
<td>

```yaml
postgres
```

</td>
</tr>
<tr>
<td> pg_bkp_base_path </td>
<td>

```yaml
/srv/exploit/backup/postgres
```

</td>
</tr>
<tr>
<td> pg_bkp_dump_target_dir </td>
<td>

```yaml
{{ pg_bkp_base_path }}/dump
```

</td>
</tr>
<tr>
<td> pg_bkp_conf_target_dir </td>
<td>

```yaml
{{ pg_bkp_base_path }}/conf
```

</td>
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

```

</td>
<tr>
<td> packages </td>
<td>

```yaml
debian:
- apt-transport-https
rhel:
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
</table>



## Role Requirements File

Additionnals roles requirements
```yaml
---
roles:
  - name: vfricou.validator
    src: git+https://github.com/vfricou/ansible_role_validator.git
    version: master
    scm: git
```



## Author Information


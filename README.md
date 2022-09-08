# nftable role

| Branch        | Status          |
| :-----------: | :-------------: |
| [master](https://github.com/devops-works/ansible-nftables) | ![Build status](https://github.com/devops-works/ansible-nftables/actions/workflows/test.yml
/badge.svg) |

## Variables

- `nft_ansible_controllers_v4` (default `[]`): list of ansible/ssh controllers
  to open ssh for (v4)
- `nft_ansible_controllers_v6` (default `[]`): list of ansible/ssh controllers
  to open ssh for (v6)
- `nft_auto_whitelist` (default `false`): whether to auto-whitelist all hosts
  in play
- `nft_ssh_ports` (default `[22,22222]`): SSH ports to open for ansible/ssh
  controllers

## Test

```bash
molecule test
```

## Usage

### Base deploy

You can call this role to install nftables and deploy base rules like so:

```yaml
- hosts: all
  become: true
  gather_facts: true
  roles:
    - ansible-nftables
```

This will deploy base rules, and open SSH for hosts listed in
`nft_ansible_controllers_v4` and  `nft_ansible_controllers_v6`.

If nft_auto_whitelist is set to true, it will also whitelist servers listed in
inventory.

## Custom rule

If you need to add a specific rule for a service, you can call the role in
"single rule mode" by setting `nft_add_input_rule`:

```yaml
# - deploy a web server for instance
- role: ansible-nftables
  nft_add_input_rule:
    - type: 'dport_accept'
      protocol: 'tcp'
      dports: [ '80', '443' ]
      saddrs: [ '0.0.0.0/0', '::/0' ]
      weight: '90'
      comment: "allow HTTP & HTTPS in (v4/v6)"
      name: 'web_clients_accept'
```
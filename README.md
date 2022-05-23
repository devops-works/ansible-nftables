# nftable roles

## Variables

- `nft_ansible_controllers_v4` (default `[]`): list of ansible controllers to open ssh for (v4)
- `nft_ansible_controllers_v6` (default `[]`): list of ansible controllers to open ssh for (v6)
- `nft_auto_whitelist` (default `false`): whether to auto-whitelist all hosts in play
- `nft_ssh_ports` (default `[22,22222]`): SSH ports to open for ansible controllers

## Test

```
molecule test
```
# Ansible Playbook for Aptos Validator, Validator Full Node (VFN), and Public Full Nodes (PFN)

Ansible playbook for Aptos Validators, VFNs and PFNs to be delivered to bare metal servers. This playbook is intended for node runners who utilize bare metal servers and build the aptos binaries from source. This playbook includes specific tweaks to get the best performance out of the aptos-node service. 🚀

## This repo allows the:

- Ability to initialize an aptos validator, vfn and pfn from source, including bootstrapping the node, moving keys and configuration files, etc.
- Ability to upgrade to a new hash when requested for planned upgrades.
- Ability to upgrade to a hotfix binary release when requested.
- Contains tweaks to process CPU prioritization and IO prioritization to ensure aptos-node runs as close to run-time as necessary (without impacting core linux services)
- This playbook does not include core server setup, security, or power management components necessary for server security and performance. These components are the responsibility of the operator.

## How to setup this repository

1. Copy inventory file

    `cp inventory.sample inventory.ini`

    Update information in the inventory file. Mostly like you will need to update the server IP and hostname fields, create groups, all that.

2. In addition, _if you want_, you can include identity files for `validator-full-node-identity.yaml` and `validator-identity.yaml` for each of the networks you use.  

**We highly recommend using Ansible Vault if you want to include these files in the repo and making your fork private.**

3. Review the group_vars values for each network. Update variables as required in `inventory.ini`.

## How to use this repository

- Init'ing a new node:  `ansible-playbook aptos_node_init.yaml --limit nodename-in-inventory`.  The node type is set in the inventory file.

- Upgrading to a new hash as provided by Aptos.  First set the new git hash in the appropriate group_var file under the variable `node_version`.  Then run  `ansible-playbook aptos_node_upgrade.yaml --limit nodename-in-inventory`.

- Hotfix: Sometimes the aptos team releases binaries without providing the source.  In that case, set the variable `hotfix_binary_url` to the location of the .tgz binary in the appropriate group_var file.  Then run `ansible-playbook aptos_node_hotfix_install.yaml --limit nodename-in-inventory`.

Have ideas/changes/additions? Great! Feel free to push a PR to this repo or reach out to [me on Discord](https://discord.gg/SGhQzj5tyz)!

## Who is RHINO?

RHINO is a professionally managed, highly available validator service. Earn rewards and help secure networks by staking your tokens with RHINO. We operate across the Aptos, Cosmos, Chainlink, and Helium ecosystems. Read more at [https://rhinostake.com](https://rhinostake.com).

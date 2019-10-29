# Josh's Satellite 6.x Deployment Playbook

This playbook converts a standard RHEL server into a satellite 6 server. It handles mount points, tuning, packages, repos, and configurations.

# Usage

Configure most settings in roles/satellite/vars/main.yml

# Requirements

- There must be 1500GB of space in the same volume group as /var
- The server should be registered directly to Red Hat's CDN
- The server must meet the [minimum system requirements](https://access.redhat.com/documentation/en-us/red_hat_satellite/6.6/html/installing_satellite_server_from_a_connected_network/preparing_your_environment_for_installation#system_requirements_satellite)
- This was written for Ansible 2.8. Older versions may work but YMMV
- You will need to provide your own manifest generated from the [Red Hat customer portal](https://access.redhat.com/management/subscription_allocations)
- The foreman ansible modules should be available on the system running this playbook. They do not need to be on the satellite server. An example ansible.cfg is included.

# Known Issue

- The task to sync repositories doesn't want to wait
- Need to add a check to make sure composites get promoted
- Activation key section occasionally fails on certain subscriptions

# Comments/Questions/Concerns

- Contact Josh: jswanson@redhat.com

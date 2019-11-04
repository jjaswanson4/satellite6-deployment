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

# Ansible Notes

- This playbook actually generates task files on the fly then includes them. These task files will be placed into the directory where the role runs from. The reason for this is various modules take 0 or more options/arguments, however if they're fed ' | default(omit)' ansible sends an empty dict into the module and it fails.
- On the flip side, the task files can be ratained and source controlled if desired. Behavior can be changed from defaults/main.yml
- Examples of the generated task files can be found in tasks/something.yml.generated.example 

# Known Issues

- The task to sync repositories doesn't want to wait
- Need to add a check to make sure composites get promoted
- Activation key section occasionally fails on certain subscriptions

* Please open issues on GitHub if something else doesn't work as expected

# To-Dos

- Test building more than one satellite at a time
- Add in building capsules
- Add in uploading remote-execution examples
- Day 3 operations, such as creating new versions of content views, promoting the composites, and other "day 3" operations will be added to another repository.

# Comments/Questions/Concerns

- Contact Josh: jswanson@redhat.com

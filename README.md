# Josh's Satellite 6.x Deployment Playbook

##### THIS BRANCH IS NOT STABLE #####

This playbook converts a standard RHEL server into a satellite server. It handles mount points, tuning, packages, repos, and configurations. 

Update 04/01/2020:
- At this point, the satellite code is mostly stable
- Foreman and Katello settings have been broken out into different roles
- The capsule code is included, but will probably not run

Update 03/20/2020:
- Rearchitect vars structure

Update 11/22/2019:
- Ansible collections now supported
- What was one giant role has been broken into more consumable roles
- Most of the groundwork for building capsules is in
- Now supports multiple satellite builds via independent vars files

# Usage

Vars files should be placed in roles/satellite/vars. There should be one vars file per satellite server, named as such: roles/satellite/vars/hostname.vars.yml
- An example vars file is located at roles/satellite/vars/satellite.vars.yml.example

# Requirements

- There must be 1500GB of space in the same volume group as /var
- The server should be registered directly to Red Hat's CDN
- The server must meet the [minimum system requirements](https://access.redhat.com/documentation/en-us/red_hat_satellite/6.6/html/installing_satellite_server_from_a_connected_network/preparing_your_environment_for_installation#system_requirements_satellite)
- This was written for Ansible 2.9
- Install requirements by running 'ansible-galaxy collection install -r requirements.yml'
- You will need to provide your own manifest generated from the [Red Hat customer portal](https://access.redhat.com/management/subscription_allocations)
- apypie is required (install it with pip) | To be added to the pre-flight checks task


# Ansible Notes

- This playbook actually generates task files on the fly then includes them. These task files will be placed into the directory where the role runs from. The reason for this is various modules take 0 or more options/arguments, however if they're fed ' | default(omit)' ansible sends an empty dict into the module and it fails.
- On the flip side, the task files can be ratained and source controlled if desired. Behavior can be changed from defaults/main.yml
- Examples of the generated task files can be found in tasks/something.yml.generated.example 

# Known Issues

- Need to add a check to make sure composites get promoted
- Activation key section occasionally fails on certain subscriptions

* Please open issues on GitHub if something else doesn't work as expected
* Satellite 6.6 will remain the 'master' branch until this playbook is viable front to back without hand-holding

# To-Dos

- Test building more than one satellite at a time
- Add in building capsules
- Add in uploading remote-execution templates
- Day 3 operations, such as creating new versions of content views, promoting the composites, and other "day 3" operations will be added to another repository.

# Comments/Questions/Concerns

- Contact Josh: jswanson@redhat.com

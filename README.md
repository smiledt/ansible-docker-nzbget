Docker-NZBGet
=========

A role to spin up a Sonarr docker container. This role was heavily inspired by (and all credit goes to) [Calvin Bui](https://calvin.me)'s role. This is only being published for integration into my AWX instance. 

Requirements
------------

Docker needs to be installed and configured on the server. 

Role Variables
--------------

Required variables are listed here, along with default example values. Any of these defaults can be overwritten by using the vars role directory. 

    nzbget_name: nzbget

This is the name of the container. 

    nzbget_image: calvinbui/docker-nzbget

The image container. By default this pulls from a custom image that may no longer be maintained. I switched to linuxserver/nzbget to avoid that problem. 

    nzbget_ports:
      - 6789:6789

These are the exported ports of the container. This is a list.

    nzbget_config_directory: /opt/nzbget

This is the directory that config files will be stored. This is mapped to /config in the container. 

    nzbget_main_directory: /tmp/nzbget

This is the directory that NZBGet will use for its main files. My default this is set to /tmp so partially downloaded files will not persist through a reboot. This is mapped to /downloads in the container.  

    nzbget_complete_directory: /mnt/media/downloads

This is where completed downloads will be placed. This ideally is located on a media server, or where a management client like Sonarr/Radarr can manage these downloads.

    nzbget_environment_variables:
      PUID: "1000"
      PGID: "1000"
      TZ: America/Chicago

This is a dictionary of extra environment variables for the container. 

    nzbget_docker_additional_options:
      restart_policy: unless-stopped

Another dictionary, this time of additional options for the container. By default, this sets the container to start on boot unless it was previously stopped. 

    nzbget_config:
      MainDir: '/downloads'
      ScriptDir: '/config/scripts'
      LockFile: '/config/nzbget.lock'
      LogFile: '/config/nzbget.log'
      DestDir: '/completed' 

These are additional configuration options that are set in the nzbget config file. 

Dependencies
------------

None.

Example Playbook
----------------

    - name: Deploy NZBGet Container.
      hosts: nzbget
      become: true
      roles:
      - role: docker-nzbget

License
-------

BSD

Author Information
------------------

Derek Smiley - Aspiring System Administrator/Ansible Automation Engineer

Connect with me on LinkedIn - https://www.linkedin.com/in/derek-smiley/
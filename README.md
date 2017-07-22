WebStorm
=========

This role installs WebStorm and configured plugins. It has been tested on Linux Mint 18 but should wokr on most 
distributions. By default it installs WebStorm 2017.2 and no additional plugins

By default webstorm is installed under the user's home directory and _become_ is not needed.

Requirements
------------

None


Role Variables
--------------

    webstorm_version: 2017.2
    webstorm_download_mirror: https://download.jetbrains.com/webstorm/
    webstorm_plugin_download_mirror: "https://plugins.jetbrains.com/plugin/download?updateId="
    webstorm_plugins: []
    webstorm_download_directory: /tmp
    webstorm_install_directory: "{{ ansible_env['HOME'] }}/Tools"

    # calculated

    webstorm_install_file: "WebStorm-{{ webstorm_version }}.tar.gz"
    webstorm_download_url: "{{ webstorm_download_mirror }}{{ webstorm_install_file }}"
    webstorm_location: "{{ webstorm_install_directory }}/webstorm-{{ webstorm_version }}"
    webstorm_desktop_file_location: "{{ ansible_env['HOME'] }}/.local/share/applications/webstorm-{{ webstorm_version}}.desktop"


webstorm_plugins is a list of names which get appended to webstorm_plugin_download_mirror to form a full download  


Dependencies
------------

None

Example 
-------

__Example playbook__


    - hosts: localhost
      connection: local
    
    roles:
      - henriklyngaard.webstorm
      
__Exmaple inventory for plugins__

The below IDs have been found by going to https://plugins.jetbrains.com/webstorm and searching for the plugin. 
Once found copy the link location for the desired version and use the _updateId=XXXXX_ part at the end        
      
    webstorm_plugins:
      # ignore 1.7.6
      - 32828
      # bash support 1.6.5.171
      - 31610
      # ansible 0.9.4
      - 27616
      # docker 2.5.3
      - 33621
      # markdown 2017.1.20170302
      - 33092      
      
 Alternatively upload the required plugins to a webserver and adjust _webstorm_plugin_download_mirror_ and 
 _webstorm_plugins_ accordingly
      
      
License
-------

MIT

Change log
----------

* 1.0: Initial version

# Nethserver official Vagrant boxes

https://app.vagrantup.com/nethserver

The box contain a vanilla [unattended installation](http://docs.nethserver.org/en/v7/installation.html#installation-unattended) of Nethsever

## Requirements

 * [virtualbox](https://www.virtualbox.org/)
 * [ansible](https://www.ansible.com/)
 * [packer](https://www.packer.io/)

## Publish a box

1. Create new vagrant box : https://app.vagrantup.com/boxes/new
1. Generate new token: https://app.vagrantup.com/settings/security
1. Export `VAGRANT_CLOUD_TOKEN` env variable: `# export VAGRANT_CLOUD_TOKEN="<TOKEN>"`
1. Build and upload vagrant box:
	* `$ packer build -only=nethserver nehtserver.json` for nethserver stable
	* `$ packer build -only=nethserver-testing nehtserver.json` for nethserver testing
	* `$ packer build nehtserver.json` for both

## Release a new version

Edit `variables` section of  `nehtserver.json` file
```json
  "variables":
    {
      "version": "1804.01",
      "iso_url": "https://sourceforge.net/projects/nethserver/files/nethserver-7.5.1804-x86_64.iso/download",
      "iso_checkmsum": "cdb9e302d563d5abb500286946e88e33ec81058d"
    }
```
1. Replace the fields with the new values:
	* `version` with the new version
	* `iso_url` with the new url of iso file
	* `iso_checkmsum` with the new url checkmsum of the iso file
1. Build and upload new vagrant boxes: `$ packer build nehtserver.json`

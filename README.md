Ansible role: Netboot
=====================

Install and configure a TFTP server for netbooting.

Role Variables
--------------

```
ENTRY POINT: main - Install and configure a TFTP server for netbooting

OPTIONS (= is mandatory):

- debian_mirror
        URL for apt mirror where the debian images will be fetched
        from
        [Default: http://deb.debian.org/debian/]
        type: str

- netboot_default_boot_delay
        Time (in seconds) to wait before netbooted machine boots into
        default boot entry
        [Default: 20]
        type: int

- netboot_grub_default_boot_entry
        Default boot entry for grub, if no specifc host boot
        configuration file exists
        (Choices: local_chain_hd0, local_chain_legacy_hd0,
        local_chain_legacy_hd1)[Default: local_chain_hd0]
        type: str

- netboot_images
        List of debian-based images to download and serve over TFTP
        [Default: (null)]
        elements: dict
        type: list

        OPTIONS:

        - checksum_type
            Type of checksums in the checksums file
            [Default: sha256]
            type: str

        - checksums
            Relative path from the base URL to the checksums file
            [Default: SHA256SUMS]
            type: str

        = initrd
            Relative path from the base URL to the initial ramdisk
            image

            type: str

        = kernel
            Relative path from the base URL to the kernel image

            type: str

        = name
            Name of the image

            type: str

        = url
            Base URL for the images available for the distribution
            version

            type: str

- netboot_preseed_dir
        Directory for the debian preseed files
        [Default: /srv/https/preseed]
        type: str

- netboot_pxelinux_default_boot_entry
        Default boot entry for pxelinux, if no specifc host boot
        configuration file exists
        (Choices: local, local_primary, local_skip, local_chain_hd0,
        local_chain_hd1)[Default: local]
        type: str

- netboot_tftp_config
        TFTP configuration
        [Default: {'TFTP_USERNAME': 'tftp', 'TFTP_DIRECTORY':
        '/srv/tftp', 'TFTP_ADDRESS': '0.0.0.0:69', 'TFTP_OPTIONS': '--
        secure'}]
        type: dict

- netboot_tftp_dir
        Directory containing the files served over TFTP
        [Default: /srv/tftp]
        type: str

- ubuntu_mirror
        URL for apt mirror where the ubuntu images will be fetched
        from
        [Default: http://archive.ubuntu.com/ubuntu/]
        type: str
```

Installation
------------

This role can either be installed manually with the ansible-galaxy CLI tool:

    ansible-galaxy install git+https://github.com/wandansible/netboot,main,wandansible.netboot
     
Or, by adding the following to `requirements.yml`:

    - name: wandansible.netboot
      src: https://github.com/wandansible/netboot

Roles listed in `requirements.yml` can be installed with the following ansible-galaxy command:

    ansible-galaxy install -r requirements.yml

Example Playbook
----------------

    - hosts: netboot_servers
      roles:
         - role: wandansible.netboot
           become: true

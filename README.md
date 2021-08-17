# rhvm-check-ovfstore

This role checks whether the disks in each VM match the same disks in the OVF Store.
For each VM, it obtains its disks' uuid from API and from OVF dumps, and then verifies they're the same list.

The disks' uuids from the API XML are taken from the node `//disk`, attribute `id`.

The disks' uuids from the OVF dumps are taken from the node `//Disk`, attribute `ovf:fileRef`, first part before the slash `/`.

## Requirements

* Ansible v2.8+
* A proper inventory (see example)

## Variables

| Name | Default | Description |
|--------------------------|---------|-------------|
|`force_dump`          | `false`  | If `true`, dumps the OVF disks even if they already exist in the `ovf_dump_dir`. |
|`ovf_dump_dir`        | `/var/tmp/ovf_dumps` | The path on the Ansible Controller where to put the OVF dumps and extract them. |


## Use

The playbook runs mainly on the controller, except the dumps which are run on the hypervisors.

To run the Role:

```
$ ansible-playbook -i inventory.yml rhvm-check-ovfstore.yml
```

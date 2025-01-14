---
page_title: "talos_machine_disks Data Source - talos"
subcategory: ""
description: |-
  Generate a machine configuration for a node type
---

# talos_machine_disks (Data Source)

Generate a machine configuration for a node type

-> **Note:** Since Talos natively supports `.machine.install.diskSelector`, the `talos_machine_disks` data source maybe just used to query disk information that could be used elsewhere. It's recommended to use `machine.install.diskSelector` in Talos machine configuration.

## Example Usage

```terraform
resource "talos_machine_secrets" "this" {}

data "talos_machine_disks" "this" {
  client_configuration = talos_machine_secrets.this.client_configuration
  node                 = "10.5.0.2"
  filters = {
    size = "> 100GB"
    type = "nvme"
  }
}

# for example this could be used to pass in list of disks to rook-ceph
output "nvme_disks" {
  value = data.talos_machine_disks.this.disks.*.name
}
```
<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `client_configuration` (Attributes) The client configuration data (see [below for nested schema](#nestedatt--client_configuration))
- `node` (String) controlplane node to retrieve the kubeconfig from

### Optional

- `endpoint` (String) endpoint to use for the talosclient. if not set, the node value will be used
- `filters` (Attributes) Filters to apply to the disks (see [below for nested schema](#nestedatt--filters))
- `timeouts` (Attributes) (see [below for nested schema](#nestedatt--timeouts))

### Read-Only

- `disks` (Attributes List) The disks that match the filters (see [below for nested schema](#nestedatt--disks))
- `id` (String) The generated ID of this resource

<a id="nestedatt--client_configuration"></a>
### Nested Schema for `client_configuration`

Required:

- `ca_certificate` (String) The client CA certificate
- `client_certificate` (String) The client certificate
- `client_key` (String, Sensitive) The client key


<a id="nestedatt--filters"></a>
### Nested Schema for `filters`

Optional:

- `bus_path` (String) Filter disks by bus path
- `modalias` (String) Filter disks by modalias
- `model` (String) Filter disks by model
- `name` (String) Filter disks by name
- `serial` (String) Filter disks by serial number
- `size` (String) Filter disks by size
- `type` (String) Filter disks by type
- `uuid` (String) Filter disks by uuid
- `wwid` (String) Filter disks by wwid


<a id="nestedatt--timeouts"></a>
### Nested Schema for `timeouts`

Optional:

- `read` (String) A string that can be [parsed as a duration](https://pkg.go.dev/time#ParseDuration) consisting of numbers and unit suffixes, such as "30s" or "2h45m". Valid time units are "s" (seconds), "m" (minutes), "h" (hours). Read operations occur during any refresh or planning operation when refresh is enabled.


<a id="nestedatt--disks"></a>
### Nested Schema for `disks`

Read-Only:

- `bus_path` (String) The bus path of the disk
- `modalias` (String) The modalias of the disk
- `model` (String) The model of the disk
- `name` (String) The name of the disk
- `serial` (String) The serial number of the disk
- `size` (String) The size of the disk
- `type` (String) The type of the disk
- `uuid` (String) The uuid of the disk
- `wwid` (String) The wwid of the disk

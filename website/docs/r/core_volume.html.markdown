---
layout: "oci"
page_title: "OCI: oci_core_volume"
sidebar_current: "docs-oci-resource-core-volume"
description: |-
  Creates and manages an OCI Volume
---

# oci_core_volume
The `oci_core_volume` resource creates and manages an OCI Volume

Creates a new volume in the specified compartment. Volumes can be created in sizes ranging from
50 GB (51200 MB) to 32 TB (33554432 MB), in 1 GB (1024 MB) increments. By default, volumes are 1 TB (1048576 MB).
For general information about block volumes, see
[Overview of Block Volume Service](https://docs.us-phoenix-1.oraclecloud.com/Content/Block/Concepts/overview.htm).

A volume and instance can be in separate compartments but must be in the same Availability Domain.
For information about access control and compartments, see
[Overview of the IAM Service](https://docs.us-phoenix-1.oraclecloud.com/Content/Identity/Concepts/overview.htm). For information about
Availability Domains, see [Regions and Availability Domains](https://docs.us-phoenix-1.oraclecloud.com/Content/General/Concepts/regions.htm).
To get a list of Availability Domains, use the `ListAvailabilityDomains` operation
in the Identity and Access Management Service API.

You may optionally specify a *display name* for the volume, which is simply a friendly name or
description. It does not have to be unique, and you can change it. Avoid entering confidential information.


## Example Usage

```hcl
resource "oci_core_volume" "test_volume" {
	#Required
	availability_domain = "${var.volume_availability_domain}"
	compartment_id = "${var.compartment_id}"

	#Optional
	backup_policy_id = "${oci_core_backup_policy.test_backup_policy.id}"
	defined_tags = {"Operations.CostCenter"= "42"}
	display_name = "${var.volume_display_name}"
	freeform_tags = {"Department"= "Finance"}
	size_in_gbs = "${var.volume_size_in_gbs}"
	size_in_mbs = "${var.volume_size_in_mbs}"
	source_details {
		#Required
		id = "${var.volume_source_details_id}"
		type = "${var.volume_source_details_type}"
	}
}
```

## Argument Reference

The following arguments are supported:

* `availability_domain` - (Required) The Availability Domain of the volume.  Example: `Uocm:PHX-AD-1` 
* `backup_policy_id` - (Optional) If provided, specifies the ID of the volume backup policy to assign to the newly created volume. If omitted, no policy will be assigned. 
* `compartment_id` - (Required) The OCID of the compartment that contains the volume.
* `defined_tags` - (Optional) (Updatable) Defined tags for this resource. Each key is predefined and scoped to a namespace. For more information, see [Resource Tags](https://docs.us-phoenix-1.oraclecloud.com/Content/General/Concepts/resourcetags.htm).  Example: `{"Operations.CostCenter": "42"}` 
* `display_name` - (Optional) (Updatable) A user-friendly name. Does not have to be unique, and it's changeable. Avoid entering confidential information. 
* `freeform_tags` - (Optional) (Updatable) Free-form tags for this resource. Each tag is a simple key-value pair with no predefined name, type, or namespace. For more information, see [Resource Tags](https://docs.us-phoenix-1.oraclecloud.com/Content/General/Concepts/resourcetags.htm).  Example: `{"Department": "Finance"}` 
* `size_in_gbs` - (Optional) The size of the volume in GBs.
* `size_in_mbs` - (Optional) The size of the volume in MBs. The value must be a multiple of 1024. This field is deprecated. Use `size_in_gbs` instead. 
* `source_details` - (Optional) Specifies the volume source details for a new Block volume. The volume source is either another Block volume in the same Availability Domain or a Block volume backup. This is an optional field. If not specified or set to null, the new Block volume will be empty. When specified, the new Block volume will contain data from the source volume or backup. 
	* `id` - (Required) The OCID of the volume or volume backup.
	* `type` - (Required) The type of volume source. It should be set to either `volumeBackup` or `volume`.
* `volume_backup_id` - (Optional) The OCID of the volume backup from which the data should be restored on the newly created volume. This field is deprecated. Use the `source_details` field instead to specify the backup for the volume. 


** IMPORTANT **
Any change to a property that does not support update will force the destruction and recreation of the resource with the new property values

## Attributes Reference

The following attributes are exported:

* `availability_domain` - The Availability Domain of the volume.  Example: `Uocm:PHX-AD-1` 
* `compartment_id` - The OCID of the compartment that contains the volume.
* `defined_tags` - Defined tags for this resource. Each key is predefined and scoped to a namespace. For more information, see [Resource Tags](https://docs.us-phoenix-1.oraclecloud.com/Content/General/Concepts/resourcetags.htm).  Example: `{"Operations.CostCenter": "42"}` 
* `display_name` - A user-friendly name. Does not have to be unique, and it's changeable. Avoid entering confidential information. 
* `freeform_tags` - Free-form tags for this resource. Each tag is a simple key-value pair with no predefined name, type, or namespace. For more information, see [Resource Tags](https://docs.us-phoenix-1.oraclecloud.com/Content/General/Concepts/resourcetags.htm).  Example: `{"Department": "Finance"}` 
* `id` - The OCID of the volume.
* `is_hydrated` - Specifies whether the cloned volume's data has finished copying from the source volume or backup.
* `size_in_gbs` - The size of the volume in GBs.
* `size_in_mbs` - The size of the volume in MBs. This field is deprecated. Use `size_in_gbs` instead.
* `source_details` - The volume source, either an existing volume in the same Availability Domain or a volume backup. If null, an empty volume is created. 
	* `id` - The OCID of the volume or volume backup.
	* `type` - The type of volume source. It should be set to either `volumeBackup` or `volume`.
* `state` - The current state of a volume.
* `time_created` - The date and time the volume was created. Format defined by RFC3339.
* `volume_group_id` - The OCID of the source volume group.

## Import

Volumes can be imported using the `id`, e.g.

```
$ terraform import oci_core_volume.test_volume "id"
```

# oci_identity_smtp_credential

## SmtpCredential Resource

### SmtpCredential Reference

The following attributes are exported:

* `description` - The description you assign to the SMTP credential. Does not have to be unique, and it's changeable.
* `id` - The OCID of the SMTP credential.
* `inactive_state` - The detailed status of INACTIVE lifecycleState.
* `state` - The credential's current state.
* `time_created` - Date and time the `SmtpCredential` object was created, in the format defined by RFC3339.  Example: `2016-08-25T21:10:29.600Z` 
* `time_expires` - Date and time when this credential will expire, in the format defined by RFC3339. Null if it never expires.  Example: `2016-08-25T21:10:29.600Z` 
* `user_id` - The OCID of the user the SMTP credential belongs to.
* `username` - The SMTP user name.
* `password` - The SMTP password.




### Create Operation
Creates a new SMTP credential for the specified user. An SMTP credential has an SMTP user name and an SMTP password.
You must specify a *description* for the SMTP credential (although it can be an empty string). It does not
have to be unique, and you can change it anytime with
[UpdateSmtpCredential](https://docs.us-phoenix-1.oraclecloud.com/api/#/en/identity/20160918/SmtpCredentialSummary/UpdateSmtpCredential).


The following arguments are supported:

* `description` - (Required) The description you assign to the SMTP credentials during creation. Does not have to be unique, and it's changeable. 
* `user_id` - (Required) The OCID of the user.


### Update Operation
Updates the specified SMTP credential's description.


The following arguments support updates:
* `description` - The description you assign to the SMTP credentials during creation. Does not have to be unique, and it's changeable. 


** IMPORTANT **
Any change to a property that does not support update will force the destruction and recreation of the resource with the new property values

### Example Usage

```hcl
resource "oci_identity_smtp_credential" "test_smtp_credential" {
	#Required
	description = "${var.smtp_credential_description}"
	user_id = "${oci_identity_user.test_user.id}"
}

output "SMTP Credentials are as following:"{
value = ["\n\tThe OCID of the SMTP credential - ${oci_identity_smtp_credential.test_smtp_credential.id}\n\tThe SMTP password - ${oci_identity_smtp_credential.test_smtp_credential.password}\n"]
}
```

# oci_identity_smtp_credentials

## SmtpCredential DataSource

Gets a list of smtp_credentials.

### List Operation
Lists the SMTP credentials for the specified user. The returned object contains the credential's OCID, 
the SMTP user name but not the SMTP password. The SMTP password is returned only upon creation.

The following arguments are supported:

* `user_id` - (Required) The OCID of the user.


The following attributes are exported:

* `smtp_credentials` - The list of smtp_credentials.

### Example Usage

```hcl
data "oci_identity_smtp_credentials" "test_smtp_credentials" {
	#Required
	user_id = "${oci_identity_user.test_user.id}"
}
```

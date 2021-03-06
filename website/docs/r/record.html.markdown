---
layout: "digitalocean"
page_title: "DigitalOcean: digitalocean_record"
sidebar_current: "docs-do-resource-record"
description: |-
  Provides a DigitalOcean DNS record resource.
---

# digitalocean\_record

Provides a DigitalOcean DNS record resource.

## Example Usage

```hcl
# Create a new domain
resource "digitalocean_domain" "default" {
  name       = "www.example.com"
  ip_address = "${digitalocean_droplet.foo.ipv4_address}"
}

# Add a record to the domain
resource "digitalocean_record" "foobar" {
  domain = "${digitalocean_domain.default.name}"
  type   = "A"
  name   = "foobar"
  value  = "192.168.0.11"
}
```

## Argument Reference

The following arguments are supported:

* `type` - (Required) The type of record
* `domain` - (Required) The domain to add the record to
* `value` - (Optional) The value of the record
* `name` - (Optional) The name of the record
* `weight` - (Optional) The weight of the record, for SRV records.
* `port` - (Optional) The port of the record, for SRV records.
* `priority` - (Optional) The priority of the record, for MX and SRV
   records.
* `ttl` - (Optional) The time to live for the record, in seconds.
* `flags` - (Optional) The flags of the record (integer between 0-255), for CAA records.
* `tag` - (Optional) The tag of the record (one of `issue`, `wildissue`, or `iodef`), for CAA records.

## Attributes Reference

The following attributes are exported:

* `id` - The record ID
* `fqdn` - The FQDN of the record

## Import

Records can be imported using the domain name and record `id` when joined with a comma.  See the following example:

```
terraform import digitalocean_record.example_record example.com,12345678
```

---
title: System on Grid API Reference

language_tabs:
  - shell: cURL
  - python

includes:
  - errors

search: true
---

# Introduction

Welcome to the System on Grid API, you can use our API to access create/modify/delete orbits and volumes along with other actions.

You can view response examples in the dark area to the right in JSON format, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/tripit/slate). 


# Orbits

## Get All Orbits

```python
import requests

url = "http://127.0.0.1:8001/vms/"

response = requests.request("GET", url)

print(response.text)
```

```shell
curl --request GET --url http://127.0.0.1:8001/vms/
```

> The above command returns JSON structured like this:

```json
[
  {
    "availability_zone": "xx",
    "created_at": "2016-10-25T15:54:14Z",
    "delete_root": false,
    "description": null,
    "id": 13,
    "ipaddr": "192.168.x.x",
    "is_active": true,
    "progress": 6,
    "ram": 2,
    "status": "PAUSING",
    "vcpus": 2,
    "vm_name": "xx"
  },
]
```

This endpoint retrieves all orbits/VM's.

### HTTP Request

`GET /vms HTTP/1.1`

## Get a particular Orbit

```python
import requests

url = "http://127.0.0.1:8001/vms/vm_details/15/"

response = requests.request("GET", url)

print(response.text)
```

```shell
curl --request GET --url http://127.0.0.1:8001/vms/vm_details/15/
```

> The above command returns JSON structured like this:

```json
{
  "admin_pwd": "xxx",
  "availability_zone": "xx",
  "created_at": "2016-10-25T15:55:39Z",
  "delete_root": false,
  "description": null,
  "id": 15,
  "ipaddr": "192.168.222.40",
  "is_active": true,
  "progress": 6,
  "ram": 2,
  "ssh_key_value": "xx",
  "status": "RUNNING",
  "vcpus": 2,
  "vm_name": "xx",
  "volume_model": [
    {
      "created_at": "2016-10-25T15:56:05Z",
      "id": 3,
      "is_root": true,
      "nickname": "xx",
      "partition": null,
      "size": "20 GB",
      "source_image": "Ubuntu 16.04 X64",
      "status": "RUNNING"
    },
  ]
}
```

This endpoint retrieves a specific Orbit.

### HTTP Request

`GET /vms/vm_details/<pk>/ HTTP/1.1`

### Template Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
pk | string | Yes | Primary key of the orbit(orbit_id)

## Modify a particular Orbit

```python
import requests

url = "http://127.0.0.1:8001/vms/vm_details/15/"

querystring = {"vm_name":"xxx", "delete_root":"true", "description":"xxx"}

response = requests.request("PUT", url, params=querystring)

print(response.text)
```

```shell
curl --request PUT --url 'http://127.0.0.1:8001/vms/vm_details/15/?description=hi&vm_name=d%60&delete_root=false/'
```

> The above command returns JSON structured like this:

```json
{
  "admin_pwd": "xxx",
  "availability_zone": "xx",
  "created_at": "2016-10-25T15:55:39Z",
  "delete_root": false,
  "description": "hi",
  "id": 15,
  "ipaddr": "192.168.222.40",
  "is_active": true,
  "progress": 6,
  "ram": 2,
  "ssh_key_value": "xx",
  "status": "RUNNING",
  "vcpus": 2,
  "vm_name": "xx",
  "volume_model": [
    {
      "created_at": "2016-10-25T15:56:05Z",
      "id": 3,
      "is_root": true,
      "nickname": "xx",
      "partition": null,
      "size": "20 GB",
      "source_image": "Ubuntu 16.04 X64",
      "status": "RUNNING"
    },
  ]
}
```

This endpoint modifies name, description or delete_root for a specific Orbit.

### HTTP Request

`PUT /vms/vm_details/<pk>/?description=hi&amp;vm_name=<Name>;delete_root=false HTTP/1.1`

### Template Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
pk | string | Yes | Primary key of the orbit(orbit_id)

### Query Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
vm_name | string | Yes | Name of the orbit
description | string | No | Description of the orbit
delete_root | Bool | No | Whether root can be deleted

## Patch a particular Orbit

```python
import requests

url = "http://127.0.0.1:8001/vms/vm_details/15/"

querystring = {"vm_name":"xxx", "delete_root":"true", "description":"xxx"}

response = requests.request("PATCH", url, params=querystring)

print(response.text)
```

```shell
curl --request PATCH --url 'http://127.0.0.1:8001/vms/vm_details/15/?description=hi&vm_name=d%60&delete_root=false'
```

> The above command returns JSON structured like this:

```json
{
  "admin_pwd": "xxx",
  "availability_zone": "xx",
  "created_at": "2016-10-25T15:55:39Z",
  "delete_root": false,
  "description": "hi",
  "id": 15,
  "ipaddr": "192.168.222.40",
  "is_active": true,
  "progress": 6,
  "ram": 2,
  "ssh_key_value": "xx",
  "status": "RUNNING",
  "vcpus": 2,
  "vm_name": "xx",
  "volume_model": [
    {
      "created_at": "2016-10-25T15:56:05Z",
      "id": 3,
      "is_root": true,
      "nickname": "xx",
      "partition": null,
      "size": "20 GB",
      "source_image": "Ubuntu 16.04 X64",
      "status": "RUNNING"
    },
  ]
}
```

This endpoint patches name, description or delete_root for a specific Orbit.

### HTTP Request

`PATCH /vms/vm_details/15/?vm_name=xxx&amp;description=hi&amp;delete_root=true HTTP/1.1`

### Template Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
pk | string | Yes | Primary key of the orbit(orbit_id)

### Query Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
vm_name | string | No | Name of the orbit
description | string | No | Description of the orbit
delete_root | Bool | No | Whether root can be deleted

## Create an orbit

```python
import requests

url = "http://127.0.0.1:8001/vms/create/"

querystring = {"vm_name":"xxx","vm_count":"1","flavor":"2","root_size":"20","availability_zone":"xx","ssh_key_value":"xx","admin_pwd":"xx","transaction_id":"xx","booting_image":"3"}

response = requests.request("POST", url, params=querystring)

print(response.text)
```

```shell
curl --request POST --url 'http://127.0.0.1:8001/vms/create/?vm_name=xxx&vm_count=1&flavor=2&root_size=20&availability_zone=xx&ssh_key_value=xx&admin_pwd=xx&transaction_id=xx&booting_image=3'
```

> The above command returns JSON structured like this:

```json
{
  "admin_pwd": "xx",
  "availability_zone": "xx",
  "created_at": "2016-11-08T16:32:46.124412Z",
  "delete_root": false,
  "description": null,
  "id": 30,
  "ipaddr": null,
  "is_active": false,
  "progress": 0,
  "ram": 2,
  "ssh_key_value": "xx",
  "status": "CREATING",
  "vcpus": 2,
  "vm_name": "xx",
  "volume_model": []
}
```

This endpoint creates an Orbit.

### HTTP Request

`POST /vms/create/?vm_name=xx&amp;vm_count=1&amp;flavor=2&amp;root_size=20&amp;availability_zone=xx&amp;ssh_key_value=xx&amp;admin_pwd=xx&amp;transaction_id=xx&amp;booting_image=3 HTTP/1.1`

### Query Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
vm_name | string | Yes | Name of the orbit
vm_count | Int | Yes | Number of orbits
flavor | Int | Yes | Type of Flavor
root_size | Int | Yes | Size of root
availability_zone | string | No | zone where orbit is created
ssh_key_value | string | Yes | ssh key
admin_pwd | string | Yes | Administrator password
transaction_id | string | Yes | Transaction ID
delete_root | Bool | No | Whether root can be deleted
booting_image | Int | Either booting image or booting_volume required | Image to boot from
booting_volume | Int | Either booting image or booting_volume required | Volume to boot from
description | string | No | Description of the orbit

## Get All Images

```python
import requests

url = "http://127.0.0.1:8001/vms/images/"

response = requests.request("GET", url)

print(response.text)
```

```shell
curl --request GET --url http://127.0.0.1:8001/vms/images/
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "image_name": "Fedora 24",
    "os_distro": "Fedora"
  },
  {
    "id": 2,
    "image_name": "Ubuntu 16.04 X64",
    "os_distro": "Ubuntu"
  },
  {
    "id": 3,
    "image_name": "Ubuntu 14.04 X64",
    "os_distro": "Ubuntu"
  },
  {
    "id": 4,
    "image_name": "Ubuntu 15.10 X64",
    "os_distro": "Ubuntu"
  },
  {
    "id": 5,
    "image_name": "CentOS 7.2 X64",
    "os_distro": "Centos"
  }
]
```

This endpoint retrieves all images.

### HTTP Request

GET /vms/images/ HTTP/1.1

## Get All Flavors

```python
import requests

url = "http://127.0.0.1:8001/vms/flavors/"

response = requests.request("GET", url)

print(response.text)
```

```shell
curl -X GET "http://127.0.0.1:8001/vms/flavors/"
```

> The above command returns JSON structured like this:

```json
[
  {
    "flavor_code": "01001",
    "hourly": 0.014,
    "id": 1,
    "is_configurable": false,
    "name": "Meteor",
    "network_usage": 2000,
    "ram": 1,
    "vcpus": 1
  },
  {
    "flavor_code": "02002",
    "hourly": 0.031,
    "id": 2,
    "is_configurable": false,
    "name": "Asteroid",
    "network_usage": 3000,
    "ram": 2,
    "vcpus": 2
  },
]
```

This endpoint retrieves all flavors.

### HTTP Request

GET /vms/flavors/ HTTP/1.1

## Get Payloads

```python
import requests

url = "http://127.0.0.1:8001/vms/payload/"

response = requests.request("GET", url)

print(response.text)
```

```shell
curl -X GET "http://127.0.0.1:8001/vms/payload/"
```

> The above command returns JSON structured like this:

```json
{
  "flavors": [
    {
      "flavor_code": "01001",
      "hourly": 0.014,
      "id": 1,
      "is_configurable": false,
      "name": "Meteor",
      "network_usage": 2000,
      "ram": 1,
      "vcpus": 1
    },
  ],
  "volumes": [
    {
      "capacity": 20,
      "hourly": 0.002,
      "id": 1,
      "monthly": 1
    },
  ]
```

This endpoint retrieves the payload information.

### HTTP Request

GET /vms/payload/ HTTP/1.1

## Delete an Orbit

```python
import requests

url = "http://127.0.0.1:8001/vms/13/delete/"

response = requests.request("POST", url, headers=headers)

print(response.text)
```

```shell
curl --request POST --url http://127.0.0.1:8001/vms/13/delete/
```

> The above command returns the following response:

```json
"Virtual Machine is in pausing status, please wait until it finish."
```

This endpoint deletes a specific Orbit.

### HTTP Request

`POST /vms/<orbit_id>/delete/ HTTP/1.1`

### Template Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
orbit_id | string | Yes | Primary key of the orbit

## Get all Resize options

```python
import requests

url = "http://127.0.0.1:8001/vms/14/resize"

response = requests.request("GET", url)

print(response.text)
```

```shell
curl --request GET --url http://127.0.0.1:8001/vms/14/resize
```

> The above command returns JSON structured like this:

```json
[
  {
    "flavor_code": "02004",
    "hourly": 0.066,
    "id": 3,
    "is_configurable": false,
    "name": "Comet",
    "network_usage": 3000,
    "ram": 4,
    "vcpus": 2
  },
  {
    "flavor_code": "04008",
    "hourly": 0.145,
    "id": 4,
    "is_configurable": false,
    "name": "Nova",
    "network_usage": 5000,
    "ram": 8,
    "vcpus": 4
  },
]
```

This endpoint retrieves the resize options available for a particular orbit.

### HTTP Request

`GET /vms/<orbit_id>/resize HTTP/1.1`

### Template Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
orbit_id | string | Yes | Primary key of the orbit

## Resize an orbit

```python
import requests

url = "http://127.0.0.1:8001/vms/15/resize/"

querystring = {"flavor_id":"5"}

response = requests.request("POST", url, params=querystring)

print(response.text)
```

```shell
curl --request POST --url 'http://127.0.0.1:8001/vms/15/resize/?flavor_id=5'
```

> The above command returns the following response:

```json
"Please boot up the Virtual Machine before resizing"
```

This endpoint resizes an orbit given a flavor_id retrieved from GET Resize API.

### HTTP Request

`POST /vms/15/resize/?flavor_id=<flavor id> HTTP/1.1`

### Template Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
orbit_id | string | Yes | Primary key of the orbit

### Query Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
flavor_id | Int | Yes | Flavor to resize to

## Start/Pause/Reboot Orbit

```python
import requests

url = "http://127.0.0.1:8001/vms/action/"

querystring = {"action":"reboot","orbit_id":"20"}

response = requests.request("POST", url, params=querystring)

print(response.text)
```

```shell
curl --request POST --url 'http://127.0.0.1:8001/vms/action/?action=reboot&orbit_id=20'
```

> The above command returns the following response:

```json
"\"Virtual Machine is in booting status, please wait until it finish.\""
```

This endpoint performs an action(Pause/Reboot/Start) on an orbit.

### HTTP Request

`POST /vms/action/?action=<action_name>&amp;orbit_id=<orbit_id> HTTP/1.1`

### Query Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
action | string("start", "pause", reboot) | Yes | Action which can be applied to the orbit
orbit_id | Int | Yes | Orbit ID
transaction_id | string | No | Transaction ID

# Volumes

## Get All Volumes

```python
import requests

url = "http://127.0.0.1:8001/volume/"

response = requests.request("GET", url)

print(response.text)
```

```shell
curl --request GET --url http://127.0.0.1:8001/volume/
```

> The above command returns JSON structured like this:

```json
[
  {
    "attached_to": "xxx",
    "created_at": "2016-10-25T15:53:19Z",
    "id": 1,
    "is_bootable": true,
    "is_root": true,
    "nickname": "xxx",
    "partition": null,
    "size": "20 GB",
    "source_image": "Fedora 24",
    "status": "RUNNING"
  },
]
```

This endpoint retrieves all the volumes.

### HTTP Request

`GET /volume/ HTTP/1.1`

## Create a volume

```python
import requests

url = "http://127.0.0.1:8001/volume/create/"

querystring = {"nickname":"xxx","capacity":"20","attach_to":"23"}

response = requests.request("POST", url, params=querystring)

print(response.text)
```

```shell
curl -X POST "http://127.0.0.1:8001/volume/create/?nickname=xxx&capacity=20&attach_to=23"
```

> The above command returns JSON structured like this:

```json
{
  "attached_to": "xxx",
  "created_at": "2016-11-09T15:53:46.263823Z",
  "id": 18,
  "is_bootable": false,
  "is_root": false,
  "nickname": "xxx",
  "partition": null,
  "size": "20 GB",
  "source_image": null,
  "status": "CREATING"
}
```

This endpoint retrieves a specific Orbit.

### HTTP Request

`POST /volume/create/?nickname=<nickname>&amp;capacity=20&amp;attach_to=<orbit ID> HTTP/1.1`

### Query Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
nickname | string | Yes | Nickname for the volume
capacity | Int | Yes | Volume capacity in GB
attach_to | Int | No | orbit ID of the VM to which volume will be attached
partition | string | No | -

## Get details for a particular Volume

```python
import requests

url = "http://127.0.0.1:8001/volume/18"

response = requests.request("GET", url)

print(response.text)
```

```shell
curl --request GET --url http://127.0.0.1:8001/volume/18
```

> The above command returns JSON structured like this:

```json
{
  "attached_to": "xxx",
  "created_at": "2016-11-09T15:53:46Z",
  "id": 18,
  "is_bootable": false,
  "is_root": false,
  "nickname": "xxx",
  "partition": null,
  "size": 20,
  "source_image": null,
  "status": "CREATING",
  "virtual_machine": {
    "availability_zone": "xxx",
    "created_at": "2016-10-31T13:34:13Z",
    "delete_root": false,
    "description": null,
    "id": 23,
    "ipaddr": "192.168.222.158",
    "is_active": true,
    "progress": 6,
    "ram": 2,
    "status": "RUNNING",
    "vcpus": 2,
    "vm_name": "xxx"
  }
}
```

This endpoint retrieves details for a specific volume.

### HTTP Request

`GET /volume/<volume ID> HTTP/1.1`

### Template Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
id | string | Yes | Primary key of the volume(volume_id)

## Get details for a particular Volume(Update)

```python
import requests

url = "http://127.0.0.1:8001/volume/18/update/"

response = requests.request("GET", url)

print(response.text)
```

```shell
curl --request GET --url http://127.0.0.1:8001/volume/18/update/
```

> The above command returns JSON structured like this:

```json
{
  "attached_to": "xxx",
  "created_at": "2016-11-09T15:53:46Z",
  "id": 18,
  "is_bootable": false,
  "is_root": false,
  "nickname": "xxx",
  "partition": null,
  "size": "20 GB",
  "source_image": null,
  "status": "CREATING"
}
```

This endpoint retrieves details for a specific volume(Update).

### HTTP Request

`GET /volume/<volume ID>/update/ HTTP/1.1`

### Template Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
pk | string | Yes | Primary key of the volume(volume_id)


## Modify a particular Volume

```python
import requests

url = "http://127.0.0.1:8001/volume/18/update/"

querystring = {"nickname":"xxx"}

response = requests.request("PUT", url, params=querystring)

print(response.text)
```

```shell
curl --request PUT --url 'http://127.0.0.1:8001/volume/18/update/?nickname=raghav'
```

> The above command returns JSON structured like this:

```json
{
  "attached_to": "xxx",
  "created_at": "2016-11-09T15:53:46Z",
  "id": 18,
  "is_bootable": false,
  "is_root": false,
  "nickname": "xxx",
  "partition": null,
  "size": "20 GB",
  "source_image": null,
  "status": "CREATING"
}
```

This endpoint modifies nickname for a specific Volume.

### HTTP Request

`PUT /volume/<volume ID>/update/?nickname=raghav HTTP/1.1`

### Template Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
pk | string | Yes | Primary key of the volume(volume_id)

### Query Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
nickname | string | Yes | Nickname of the volume

## Patch a particular Volume

```python
import requests

url = "http://127.0.0.1:8001/volume/18/update/"

querystring = {"nickname":"xxx"}

response = requests.request("PATCH", url, params=querystring)

print(response.text)
```

```shell
curl --request PATCH --url 'http://127.0.0.1:8001/volume/18/update/?nickname=raghav'
```

> The above command returns JSON structured like this:

```json
{
  "attached_to": "xxx",
  "created_at": "2016-11-09T15:53:46Z",
  "id": 18,
  "is_bootable": false,
  "is_root": false,
  "nickname": "xxx",
  "partition": null,
  "size": "20 GB",
  "source_image": null,
  "status": "CREATING"
}
```

This endpoint patches a specific Volume.

### HTTP Request

`PUT /volume/<volume ID>/update/?nickname=raghav HTTP/1.1`

### Template Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
pk | string | Yes | Primary key of the volume(volume_id)

### Query Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
nickname | string | No | Nickname of the volume

## Attach a volume

```python
import requests

url = "http://127.0.0.1:8001/volume/2/attach/12/"

response = requests.request("POST", url)

print(response.text)
```

```shell
curl --request POST --url http://127.0.0.1:8001/volume/18/attach/12/
```

> The above command returns the following response:

```json
"Volume is already attached to Virtual Machine."
```

This endpoint attaches a Volume to an Orbit.

### HTTP Request

`POST /volume/<volume ID>/attach/<orbit ID>/ HTTP/1.1`

### Template Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
id | string | Yes | Volume ID
orbit_id | string | Yes | Orbit ID

## Detach a volume

```python
import requests

url = "http://127.0.0.1:8001/volume/2/attach/12/"

response = requests.request("POST", url)

print(response.text)
```

```shell
curl --request POST --url http://127.0.0.1:8001/volume/18/attach/12/
```

> The above command returns the following response:

```json
"Volume is in Creating status, please wait until it finish."
```

This endpoint detaches a Volume.

### HTTP Request

`POST /volume/<Volume ID>/detach/ HTTP/1.1`

### Template Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
id | string | Yes | Volume ID

## Get All Templates

```python
import requests

url = "http://127.0.0.1:8001/volume/templates"

response = requests.request("GET", url)

print(response.text)
```

```shell
curl --request GET --url http://127.0.0.1:8001/volume/templates
```

> The above command returns JSON structured like this:

```json
[
  {
    "capacity": 20,
    "hourly": 0.002,
    "id": 1,
    "monthly": 1
  },
  {
    "capacity": 40,
    "hourly": 0.0041,
    "id": 2,
    "monthly": 2
  },
  {
    "capacity": 80,
    "hourly": 0.0083,
    "id": 3,
    "monthly": 4
  },
  {
    "capacity": 120,
    "hourly": 0.0125,
    "id": 4,
    "monthly": 6
  },
  {
    "capacity": 240,
    "hourly": 0.025,
    "id": 5,
    "monthly": 12
  },
  {
    "capacity": 500,
    "hourly": 0.052,
    "id": 6,
    "monthly": 25
  },
  {
    "capacity": 1000,
    "hourly": 0.104,
    "id": 7,
    "monthly": 50
  }
]
```

This endpoint retrieves all Volume templates.

### HTTP Request

GET /vms/images/ HTTP/1.1

## Get all Resize options

```python
import requests

url = "http://127.0.0.1:8001/volume/2/resize/"

response = requests.request("GET", url)

print(response.text)
```

```shell
curl -X GET "http://127.0.0.1:8001/volume/2/resize/"
```

> The above command returns JSON structured like this:

```json
[
  {
    "capacity": 40,
    "hourly": 0.0041,
    "id": 2,
    "monthly": 2
  },
  {
    "capacity": 80,
    "hourly": 0.0083,
    "id": 3,
    "monthly": 4
  },
]
```

This endpoint retrieves the resize options available for a particular volume

### HTTP Request

`GET /volume/<Volume ID>/resize/ HTTP/1.1`

### Template Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
id | string | Yes | Volume ID

## Resize a Volume

```python
import requests

url = "http://127.0.0.1:8001/volume/4/resize/"

querystring = {"template_id":"3"}

response = requests.request("POST", url, params=querystring)

print(response.text)
```

```shell
curl --request POST --url 'http://127.0.0.1:8001/volume/4/resize/?template_id=3'
```

> The above command returns the following response:

```json
"Please Pause the VM first"
```

This endpoint resizes a volume according to a template_id retrieved from GET Resize API.

### HTTP Request

`POST /volume/<Volume ID>/resize/?template_id=<Template ID> HTTP/1.1`

### Template Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
id | string | Yes | Volume ID

### Query Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
template_id | Int | Yes | Template to resize to


## Delete a Volume

```python
import requests

url = "http://127.0.0.1:8001/volume/18/delete/"

response = requests.request("POST", url)

print(response.text)
```

```shell
curl --request POST --url http://127.0.0.1:8001/volume/18/delete/
```

> The above command returns the following response:

```json
"Please detach the volume before delete it"
```

This endpoint deletes a specific Volume.

### HTTP Request

`POST /volume/<volume ID>/delete/ HTTP/1.1`

### Template Parameters

Parameter | Type | Required | Description
--------- | ------- | ------- | -----------
id | string | Yes | Volume ID


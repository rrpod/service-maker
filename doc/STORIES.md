# User Stories

## `I` Creating a new Instance

### `Ia` With default AMI and instance type
1. The User wants to create a new instance, with a default AMI and instance size.

2. The User posts to `/v1/instances` with no payload.

3. The user receives a response:
```
201 Created
Location: https://my-servicemaker.com/v1/instances/instanceId1
{
    "id" : "instanceId1",
    "type" : "t2.micro",
    "ami" : "ami-d05e75b8",
    "state" : "pending",
    "uri" : "https://ec2-127-0-0-1.compute-1.amazonaws.com"
}
```
4. The user begins polling on `https://my-servicemaker.com/v1/instances/instanceId1` until the resource `state` changes to `ready`.

5. The user begins using his new EC2 instance.

### `Ib` With a valid AMI and the default instance type
1. The User wants to create a new instance, provisioned with the `ami-myapp` image.

2. The User posts to `/v1/instances` with the payload:
```
  {
    "ami" : "ami-myapp"
  }
```

3. The user receives a response:
```
201 Created
Location: https://my-servicemaker.com/v1/instances/instanceId1
{
    "id"    : "instanceId1",
    "type"  : "t2.micro",
    "ami"   : "ami-myapp",
    "state" : "pending",
    "uri"   : "https://ec2-127-0-0-1.compute-1.amazonaws.com"
}
```

4. The user begins polling on `https://my-servicemaker.com/v1/instances/instanceId1` until the resource `state` changes to `ready`.

5. The user begins using her new EC2 instance.

### `Ic` With a valid AMI and a specified instance type
1. The User wants to create a new `m1.medium` instance, provisioned with the `ami-myapp` image.

2. The User posts to `/v1/instances` with the payload:
```
  {
    "ami"  : "ami-myapp",
    "type" : "m1.medium"
  }
```

3. The user receives a response:
```
201 Created
Location: https://my-servicemaker.com/v1/instances/instanceId1
  {
    "id"    : "instanceId1",
    "type"  : "m1.medium",
    "ami"   : "ami-myapp",
    "state" : "pending",
    "uri"   : "https://ec2-127-0-0-1.compute-1.amazonaws.com"
  }
```

4. The user begins polling on `https://my-servicemaker.com/v1/instances/instanceId1` until the resource `state` changes to `ready`.

5. The user begins using his new EC2 instance.

### `Id` With an invalid AMI
1. The User wants to create a new instance, provisioned with the `ami-invalid` image, which does not exist.

2. The User posts to `/v1/instances` with the payload:
```
  {
    "ami" : "ami-invalid"
  }
```

3. The User receives a response:
```
400 Bad Request
  {
    "message" : "The specified AMI does not exist."
  }
```

### `Ie` With an invalid instance type
1. The User wants to create a new instance, provisioned with the `ami-myapp` image, with the nonexistent `z1.gigantic` instance type.

2. The User posts to `/v1/instances` with the payload:
```
  {
    "ami"  : "ami-myapp",
    "type" : "z1.gigantic"
  }
```

3. The User receives a response:
```
400 Bad Request
  {
    "message" : "The specified instance type does not exist."
  }
```
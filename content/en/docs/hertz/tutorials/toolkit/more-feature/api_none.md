---
title: 'api.none annotation usage'
date: 2023-04-23
weight: 5
description: >
---
## Introduction

The code generated by hz automatically adds a go tag to the `struct`, thus facilitating parameter binding.
However, some "fields" of the user structure may not want to participate in the parameter binding or serialization process, so we provide the "api.none" annotation to make the go tag of the generated structure's "fields" be "-", thus avoiding parameter binding.

## Thrift

Definition:

```
struct HelloReq{
  1: string Hertz (api.none="true");
}
```

Generated Content:

```go
type HelloReq struct {
	Hertz string `thrift:"Hertz,1" form:"-" json:"-" query:"-"`
}
```

## Protobuf

Definition:

```
message HelloReq {
  optional string Hertz = 1 [(api.none) = "true"];
}
```

Generated Content:

```go
type HelloReq struct {
	state         protoimpl.MessageState
	sizeCache     protoimpl.SizeCache
	unknownFields protoimpl.UnknownFields

	Hertz *string `protobuf:"bytes,1,opt,name=Hertz" json:"-" form:"-" query:"-"`
}
```

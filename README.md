# optexample

We have following shema:
```yaml
Example:
  type: object
  required:
    - Required
    - NullableRequired
  properties:
    Optional:
      type: string
    NullableOptional:
      type: string
      nullable: true
    Required:
      type: string
      example: "example"
    NullableRequired:
      type: string
      nullable: true
```

## ogen

```go
type Example struct {
	Optional         OptString    `json:"Optional"`
	NullableOptional OptNilString `json:"NullableOptional"`
	Required         string       `json:"Required"`
	NullableRequired NilString    `json:"NullableRequired"`
}

type OptString struct {
	Value string
	Set   bool
}

type OptNilString struct {
	Value string
	Set   bool
	Null  bool
}

type NilString struct {
	Value string
	Null  bool
}
```

## oapi-codegen

```go
type Example struct {
	NullableOptional nullable.Nullable[string] `json:"NullableOptional,omitempty"`
	NullableRequired nullable.Nullable[string] `json:"NullableRequired"`
	Optional         *string                   `json:"Optional,omitempty"`
	Required         string                    `json:"Required"`
}

// from nullable package
type Nullable[T any] map[bool]T
```
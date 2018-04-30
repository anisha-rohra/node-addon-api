# Object

Object is a Javascript object value. A common usecase is to assign many values to a single object. 

Object is extended by [Value](value.md) and extends [Array](array.md), [ArrayBuffer](arraybuffer.md), [Buffer<T>](buffer.md), [Function](function.md), and [TypedArray](typedarray.md). 

## Methods

### Empty Constructor 

```cpp
Napi::Object::Object();
```
Creates a new empty Object instance. 

### Constructor

```cpp
Napi::Object::Object(napi_env env, napi_value value);
```
- `[in] env`: The `napi_env` environment in which to construct the Value object.

- `[in] value`: The C++ primitive from which to instantiate the Value. `value` may be any of:
  - bool
  - Any integer type
  - Any floating point type
  - const char* (encoded using UTF-8, null-terminated)
  - const char16_t* (encoded using UTF-16-LE, null-terminated)
  - std::string (encoded using UTF-8)
  - std::u16string
  - napi::Value
  - napi_value

Creates a non-empty Object instance

### New()

```cpp
Object Napi::Object::New (napi_env env);
```
- `[in] env`: The `napi_env` environment in which to construct the Value object.

Creates a new Object value.

### Operator[]()

```cpp
PropertyLValue<std::string> Napi::Object::operator[] (const char* utf8name);
```
- `[in] utf8name`: UTF-8 encoded null-terminated property name.

Returns a [PropertyLValue](propertylvalue.md) as the named property or sets the named property.

```cpp
PropertyLValue<std::string> Napi::Object::operator[] (const std::string& utf8name);
```
- `[in] utf8name`: UTF-8 encoded property name.

Returns a [PropertyLValue](propertylvalue.md) as the named property or sets the named property.

```cpp
PropertyLValue<uint32_t> Napi::Object::operator[] (uint32_t index);
```
- `[in] index`: Element index.

Returns a [PropertyLValue](propertylvalue.md) or sets an indexed property or array element. 

```cpp
Value Napi::Object::operator[] (const char* utf8name) const;
```
- `[in] utf8name`: UTF-8 encoded null-terminated property name.

Returns the named property as a [Value](value.md).

```cpp
Value Napi::Object::operator[] (const std::string& utf8name) const;
```
- `[in] utf8name`: UTF-8 encoded property name.

Returns the named property as a [Value](value.md).

```cpp
Value Napi::Object::operator[] (uint32_t index) const;
```
- `[in] index`: Element index.

Returns an indexed property or array element as a [Value](value.md).

### Set() 

```cpp
void Napi::Object::Set (____ key, ____ value);
```
- `[in] key`: The key property that is being assigned a value.
- `[in] value`: The value property that is being assigned to a key.

Sets the value to the key. The key-value potential pairs are as follows:
- `napi_value` key, `napi_value` value
- [Value](value.md) key, [Value](value.md) value

Alternatively, the key can be any of the following types:
- `const char*`
- `const std::string&`
- `uint32_t`
While the value must be any of the following types:
- `napi_value`
- [Value](value.md)
- `const char*`
- `std::string&`
- `bool`
- `double`

### Get()

```cpp
Value Napi::Object::Get(____ key);
```
- `[in] key`: The property whose assigned value is being returned.

Returns the [Value](value.md) associated with the key property.
The `key` can be any of the following types:
- `napi_value`
- [Value](value.md)
- `const char *`
- `const std::string &`
- `uint32_t`

### Has()

```cpp
bool Napi::Object::Has (____ key) const;
```
- `[in] key`: The property that is being checked for having an assigned value.

Returns a `bool` that is true if the `key` has a value property associated with it and false if the `key` does not have a value property associated with it.

### InstanceOf()

```cpp
bool Napi::Object::InstanceOf (const Function& constructor) const
```
- `[in] constructor`: The constructor [Function](function.md) of the value that is being compared with the object.

Returns a `bool` that is true if the Object is an instance created by the `constructor` and false otherwise.
Note: This is equivalent to the JavaScript instanceof operator.

### DefineProperty()

```cpp
void Napi::Object::DefineProperty (const PropertyDescriptor& property);
```
- `[in] property`: A [PropertyDescriptor](propertydescriptor.md) for the property.

Define a property on the object.

### DefineProperties()

```cpp
void Napi::Object::DefineProperties (____ properties)
```
- `[in] properties`: A list of [PropertyDescriptor](propertydescriptor.md) for the properties. Can be one of the following types:
	- const std::initializer_list<PropertyDescriptor>&
	- const std::vector<PropertyDescriptor>&

Defines properties on the object.


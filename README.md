# `jss::strong_typedef<Tag,ValueType,Properties>`

[![Build Status](https://travis-ci.com/anthonywilliams/strong_typedef.svg?branch=master)](https://travis-ci.com/anthonywilliams/strong_typedef)

This is an implementation of a class template that provides a wrapper type that is convertible to
and from the underlying type, but is distinct from it.

The purpose of this is primarily to enable things like indexes and IDs to be unique types. This is
achieved by specifying a `Tag` type for each `jss::strong_typedef` use. This can be an incomplete
type, and can be forward-declared in the template parameter directly. For example:

~~~cplusplus
#include "strong_typedef.hpp"

using FirstIndex=jss::strong_typedef<struct FirstTag,int>;
using SecondIndex=jss::strong_typedef<struct SecondTag,int>;
~~~

`FirstIndex` and `SecondIndex` are both explicitly convertible to/from `int`, but they are separate
types and are thus not inter-convertible. They also have no additional operations beyond retrieving
the underlying value, as no properties are specified.

## Behaviour properties

The third template parameter (`Properties`) specifies behavioural properties for the new type. It
must be one of the values of `jss::strong_typedef_properties`, or a value obtained by or-ing them
together (e.g. `jss::strong_typedef_properties::hashable |
jss::strong_typedef_properties::streamable | jss::strong_typedef_properties::comparable`). Each
property adds some behaviour. The available properties are:

* `jss::strong_typedef_properties::equality_comparable` => Can be compared for equality (`st==st2`) and
  inequality (`st!=st2`)
* `jss::strong_typedef_properties::pre_incrementable` => Supports preincrement (`++st`)
* `jss::strong_typedef_properties::post_incrementable` => Supports postincrement (`st++`)
* `jss::strong_typedef_properties::pre_decrementable` => Supports predecrement (`--st`)
* `jss::strong_typedef_properties::post_decrementable` => Supports postdecrement (`st--`)
* `jss::strong_typedef_properties::addable` => Supports addition (`st+value`, `value+st`, `st+st2`)
  where the result is convertible to the underlying type. The result is a new instance of the strong typedef.
* `jss::strong_typedef_properties::subtractable` => Supports subtraction (`st-value`, `value-st`,
  `st-st2`) where the result is convertible to the underlying type. The result is a new instance of the strong typedef.
* `jss::strong_typedef_properties::ordered` => Supports ordering comparisons (`st<st2`, `st>st2`,
  `st<=st2`, `st>=st2`)
* `jss::strong_typedef_properties::mixed_ordered` => Supports ordering comparisons where only one of
  the values is a strong typedef
* `jss::strong_typedef_properties::hashable` => Supports hashing with `std::hash`
* `jss::strong_typedef_properties::streamable` => Can be written to a `std::ostream` with `operator<<`
* `jss::strong_typedef_properties::incrementable` =>
  `jss::strong_typedef_properties::pre_incrementable | jss::strong_typedef_properties::post_incrementable`
* `jss::strong_typedef_properties::decrementable` => `jss::strong_typedef_properties::pre_decrementable | jss::strong_typedef_properties::post_decrementable`
* `jss::strong_typedef_properties::comparable` => `jss::strong_typedef_properties::ordered | jss::strong_typedef_properties::equality_comparable`

## License

This code is released under the [Boost Software License](https://www.boost.org/LICENSE_1_0.txt):

> Boost Software License - Version 1.0 - August 17th, 2003
>
> Permission is hereby granted, free of charge, to any person or organization
> obtaining a copy of the software and accompanying documentation covered by
> this license (the "Software") to use, reproduce, display, distribute,
> execute, and transmit the Software, and to prepare derivative works of the
> Software, and to permit third-parties to whom the Software is furnished to
> do so, all subject to the following:
>
> The copyright notices in the Software and this entire statement, including
> the above license grant, this restriction and the following disclaimer,
> must be included in all copies of the Software, in whole or in part, and
> all derivative works of the Software, unless such copies or derivative
> works are solely in the form of machine-executable object code generated by
> a source language processor.
>
> THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
> IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
> FITNESS FOR A PARTICULAR PURPOSE, TITLE AND NON-INFRINGEMENT. IN NO EVENT
> SHALL THE COPYRIGHT HOLDERS OR ANYONE DISTRIBUTING THE SOFTWARE BE LIABLE
> FOR ANY DAMAGES OR OTHER LIABILITY, WHETHER IN CONTRACT, TORT OR OTHERWISE,
> ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER
> DEALINGS IN THE SOFTWARE.


# Quick Start

A **quantity** is a concrete amount of a unit representing a quantity type of a specified dimension with a
specific representation. It is represented in the library with a `quantity` class template.


## Creating a quantity

The [SI Brochure](../appendix/references.md#SIBrochure) says:

!!! quote "SI Brochure"

    The value of the quantity is the product of the number and the unit. The space between the number
    and the unit is regarded as a multiplication sign (just as a space between units implies
    multiplication).


Following the above, the value of a quantity in the **mp-units** library is created by multiplying
a number with a predefined unit:

```cpp
#include <mp-units/systems/si/si.h>

using namespace mp_units;

quantity q = 42 * si::metre;
```

!!! note

    The above spelling of `metre` is not a typo. For motivation, please check our
    [FAQ](faq.md#why-do-we-spell-metre-instead-of-meter).

The above creates an instance of `quantity<si::metre(), int>`. The same can be obtained using
an optional unit symbol:

```cpp
#include <mp-units/systems/si/si.h>

using namespace mp_units;
using namespace mp_units::si::unit_symbols;

quantity q = 42 * m;
```

!!! tip

    Unit symbols introduce a lot of short identifiers into the current scope, and that is
    why they are opt-in. A user has to explicitly "import" them from a dedicated `unit_symbols`
    namespace.

In case someone doesn't like the multiply syntax or there is an ambiguity between `operator*`
provided by this and other libraries, a quantity can also be created with a two-parameter
constructor:

```cpp
#include <mp-units/systems/si/si.h>

using namespace mp_units;

quantity q{42, si::metre};
```


## User-provided unit wrappers

Sometimes it might be awkward to type some derived units:

```cpp
quantity speed = 60 * km / h;
```

In case such a unit is used a lot in the project, a user can easily provide a nicely named
wrapper for it with:

```cpp
constexpr auto kmph = km / h;
quantity speed = 60 * kmph;
```

!!! note

    In case you wonder why this library does not use UDLs to create quantities, please check
    our [FAQ](faq.md#why-dont-we-use-udls-to-create-quantities).

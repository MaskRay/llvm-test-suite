# mp-units

An example from [mp-units](https://github.com/mpusz/mp-units), a physical
quantities and units library (MIT, see `LICENSE`), at commit
`132b590d25a18bebd099c27aa064cbbf40946b7d`.

The library relies on concepts, class-type non-type template parameters and
`consteval`, and enables C++23 features such as explicit object parameters
when available. Most of the compile time is spent in the frontend.

* `currency/currency.cpp` is `example/currency.cpp`.
* `include/` holds the headers from `src/core/include` that the example
  needs, plus `bits/constexpr_format.h` and `bits/double_width_int.h`, which
  are only included in some configurations (e.g. targets without
  `__int128`).

The files are unmodified. The example is built as C++23 with
`MP_UNITS_HOSTED=1 MP_UNITS_API_STD_FORMAT=1 MP_UNITS_API_CONTRACTS=0`, and
needs a standard library with `<format>`.

Most other upstream examples are rejected by Clang 22.

To update, check out a new upstream commit, copy the example, and
collect the headers it includes with `-MM`.

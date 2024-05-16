C++ 20 introduces **modules**.

A module is a *set* of source files that are independently compiled. It has several advantages over header files:
- Reduced compilation time.
- Hide visibility of macros, preprocessor directives, and non-exported names.
- We can import modules in any order without concern for macro redefinitions, etc.

Here is an article that [compares header files, header units, modules and precompiled header](https://learn.microsoft.com/en-us/cpp/build/compare-inclusion-methods?view=msvc-170). Support for modules of different compiler vendors can be found [here](https://en.cppreference.com/w/cpp/compiler_support) (the Modules row in the 'C++20 core language features' table).
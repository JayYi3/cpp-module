C++ 20 introduces **modules**, which allow compilers to use "semantic imports" instead of the old text inclusion model.

Modules allow shared declarations and definitions across translation units. A module is a *set* of source files that are compiled independently and only once. It has several advantages over header files:
- Reduced compilation time.
- Hide visibility of internal implementations like macros, preprocessor directives, and non-exported names.
- Modules can be imported in any order without concern for dependencies between headers.

There is a simple example inside the *examples* folder, and a script containing the commands to run it.

Here is an article that [compares header files, header units, modules and precompiled header](https://learn.microsoft.com/en-us/cpp/build/compare-inclusion-methods?view=msvc-170). Support for modules of different compiler vendors can be found [here](https://en.cppreference.com/w/cpp/compiler_support) (the Modules row in the 'C++20 core language features' table). [This video](https://www.youtube.com/watch?v=_x9K9_q2ZXE) gives a great introduction to modules.

Modules can be structured into several ways:
- Primary Module Interface Unit
  
  Both module interface and implementation goes into a single file(like a header-only library).

  ```c++
  // File: my_module.cpp
  export module my_module;

  export char const* my_func() {
    return "Hello Modules!";
  }
  ```

- Module Implementation Unit

  Module interface and implementation goes into a separate file(similar to header files and source files).

  ```c++
  // File: my_module.cpp
  export module my_module;

  export char const* my_func();

  // File: my_module_impl.cpp
  module my_module;

  char const* my_func() {
    return "Hello Modules!";
  }
  ```

- Module Interface Partitions

  This is used for structuring the internal of a module
  
  ```c++
  // File: my_module.cpp
  export module m;

  export import :p1;
  export import :p2;

  // File: my_module_p1.cpp
  export module m:p1;
  export void p1_func() {}

  // File: my_module_p2.cpp
  export module m:p2;
  export void p2_func() {}
  ```
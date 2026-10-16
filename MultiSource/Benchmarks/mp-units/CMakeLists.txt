# An example from mp-units, a C++20/23 physical units library that relies on
# concepts, class-type non-type template parameters and consteval. See
# README.md.

# CMAKE_CXX_STANDARD 23 needs CMake 3.20.
if(CMAKE_VERSION VERSION_LESS 3.20)
  message(STATUS "Skipping mp-units: it needs CMake 3.20")
  return()
endif()
set(CMAKE_CXX_STANDARD 23)

include(CheckCXXSourceCompiles)
check_cxx_source_compiles("
#include <concepts>
#include <format>
#include <string>
#if __cplusplus < 202302L || !defined(__cpp_concepts) || __cpp_concepts < 202002L
#error
#endif
int main() { return std::format(\"{}\", 42).size() == 2 ? 0 : 1; }
" MP_UNITS_HAVE_CXX23_FORMAT)
if(NOT MP_UNITS_HAVE_CXX23_FORMAT)
  message(STATUS "Skipping mp-units: it needs C++23 with concepts and <format>")
  return()
endif()

list(APPEND CPPFLAGS -I${CMAKE_CURRENT_SOURCE_DIR}/include
     -DMP_UNITS_HOSTED=1 -DMP_UNITS_API_STD_FORMAT=1 -DMP_UNITS_API_CONTRACTS=0)
set(FP_TOLERANCE 0.000001)

add_subdirectory(currency)

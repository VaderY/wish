

## Wish - A CMake library for simplicity

NOTICE: Wish was just created, documentation, features and more info will be coming "soon"

TODO: Documentation

-----

#### Setup

Grab the latest wish hook script from your project's root
TODO: More documentation
```
mkdir -p cmake && wget https://raw.githubusercontent.com/VaderY/wish/master/cmake/wish.cmake -O cmake/wish.cmake
# OR
wget https://raw.githubusercontent.com/VaderY/wish/master/cmake/wish.cmake -P cmake/
```

Inside your root CMakeLists.txt file just set the version and include the primary script:
TODO: More documentation
```
set(WISH_REQUEST_VERSION v5.1.0)
include(cmake/wish.cmake)
```

-----

#### Release notes

TODO: Format, place
TODO: Auto self update the wish.cmake script

- v5.2.0
  - Feature: Add OUTPUT_NAME support for wish_create_executable
- v5.1.0
  - Fix: Resolve the error during first configure
- v5.0.5
  - Feature: Add automated library alias naming
  - Fix: Change lockfile placement to be ignored by git
- v5.0.4
  - Improvement: Use a lockfile during wish install and update
- v5.0.3
  - Feature: Add support for library aliases
  - Improvement: Make wish_group usage optional
- v5.0.2
  - Improvement: Enable USES_TERMINAL_DOWNLOAD for externals
- v5.0.0
  - Feature: Automated wish install and update
- v4.2
  - Feature: Add wish_linker_flags
- v4.1
  - Improvement: Fix double globbing during newly created generated files
- v4.0
  - Release: Initial release in this format (history)

-----

### API Reference

TODO: Reference documentation

include(cmake/wish.cmake)
```
include(cmake/wish.cmake)
wish_version
```

wish_configurations
```
wish_configurations(DEFAULT <default mode> <other modes>...)

# Example
wish_configurations(DEFAULT Release Dev Debug)
```

wish_force_colored_output
```
wish_force_colored_output(<bool>)

# Example
option(FORCE_COLORED_OUTPUT "Always produce ANSI-colored output (GNU/Clang only)." FALSE)
wish_force_colored_output(${FORCE_COLORED_OUTPUT})
```

wish_skip_external_configures
```
wish_skip_external_configures(<bool>)

# Example
option(SKIP_EXTERNAL_CONFIGURES "Do not configure external projects only use the fake interface targets" FALSE)
wish_skip_external_configures(${SKIP_EXTERNAL_CONFIGURES})
```

wish_warning
```
TODO

# Example
wish_warning(
	MSVC /Wall
	Clang -Weverything
	GNU -Wall
	GNU VERSION_GREATER 12.0 -Wno-array-bounds
)
```

wish_compiler_flags
```
TODO

# Example
wish_compiler_flags(
	GNU -fcoroutines
	GNU -m64
	GNU -std=c++23
)
```

wish_linker_flags
```
TODO

# Example
wish_linker_flags(
	Release GNU -mwindows
)
```

wish_optimization_flags
```
wish_optimization_flags()
```

wish_group
```
wish_group(<group_name> <aliases...>)

# Example
wish_group(group_library lib)
```

wish_create_external
```
TODO

# Example
wish_create_external(
	NAME catch
	GIT_REPOSITORY https://github.com/catchorg/Catch2
	GIT_TAG v3.0.1
	CMAKE_ARGS
		-DCATCH_INSTALL_DOCS=OFF
		-DCATCH_INSTALL_EXTRAS=OFF
	LINK Catch2Main Catch2
)
```

wish_generator
```
TODO

# Example
wish_generator(
	TARGET  codegen
	COMMAND codegen
#	OUTPUT  REPLACE ".in.lua" ".hpp"
	OUTPUT  REPLACE ".ins.lua" ".hpp"
	OUTPUT  REPLACE ".ins.lua" ".cpp"
)
```

wish_create_executable
```
wish_create_executable(
	TARGET <target name>
	SOURCE <source glob pattern>...
	OBJECT <object targets>...
	OUTPUT_NAME <output name>
	GENERATE <generator name> <input glob pattern>...
	LINK <link targets or libraries>...
	[NO_GROUP]
	[DEBUG]
)

# Example
wish_create_executable(
	TARGET codegen
	SOURCE app/codegen/codegen_main.cpp
	LINK   ext_fmt ext_sol
)
```


wish_create_library
```
wish_create_library(
	TARGET <target or alias::name> (STATIC | SHARED | INTERFACE)
	ALIAS <alias::name>...
	SOURCE <source glob pattern>...
	OBJECT <object targets>...
	GENERATE <generator name> <input glob pattern>...
	LINK <link targets or libraries>...
	[NO_GROUP]
	[DEBUG]
)

# Example
wish_create_library(
	TARGET libA STATIC
	ALIAS lib::A
	SOURCE src/libA/*.cpp
#	GENERATE codegen src/libA/*.in.lua
	GENERATE codegen src/libA/*.ins.lua
	LINK   Threads::Threads
)
```

wish_create_ide_target
```
wish_create_ide_target()
```

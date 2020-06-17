# Naming Conventions {#ref_naming_conventions}

## User defined global variable {#ref_user_defined_global_variable}

### Rule 3.1

Do use underscores with upper case for user defined global variable declaration.

Why? There are accepted coding styles for variable naming conventions. This style is chosen, because system variables also declares in the same way.

@code
TARGET_ANDROID="android"
TARGET_IOS="ios"
TARGET_WINDOWS="windows"
@endcode

## Function name {#ref_function_name}

### Rule 3.2

Do use camelCase style for function names.

Do put parentheses after the function name.

Why? This style is chosen within other accepted styles for function naming conventions to differentiate variable and
function names.

Why? Parentheses after name indicates that it is a function.

@code
function nvmInstallNode () {
  echo "=> Installing Node.js version ${NODE_VERSION}"
  nvm install "${NODE_VERSION}"

  CURRENT_NVM_NODE="$(nvm_version current)"
  if [[ "$(nvm_version "${NODE_VERSION}")" == "${CURRENT_NVM_NODE}" ]]; then
    echo "=> Node.js version $NODE_VERSION has been successfully installed"
  else
    echo >&2 "Failed to install Node.js ${NODE_VERSION}"
  fi
}
@endcode

## User defined local variable {#ref_user_defined_local_variable}

### Rule 3.3

Do use underscores with lower case to declare local variable.

Why? This style is chosen to differentiate global and local variables.

@code
function verify () {
  for item in $(ls *.$1) ; do
    name="${item%.*}"
    if [[ ! -f "${name.$2}" ]]; then
      echo "Error: $2 file for '$NAME' does not exist. Aborting."
      exit 1
    fi
  done
}
@endcode

## Define a path {#ref_define_a_path}

### Rule 3.4

Do use suffix <b>_DIR</b> or <b>_PATH</b> for variable to define a path.

Do not use suffix <b>_DIR</b> when declared object is not a drectory.

Why? Adding suffixes, makes variable more visible and readable that it is describes path or directory.

@code
LIBRARIES_PATH="${EXECUTABLE_DIR}/../../libraries"
CPPUNIT_LIB_PATH="${LIBRARIES_PATH}/cppunit-1.12.1"
CPPUNIT_PREBUILT_PATH="${LIBRARIES_PATH}/cppunit-prebuilt/${PLATFORM_DIR}"
CPPUNIT_INCLUDE_PATH="${CPPUNIT_LIB_PATH}/include"
@endcode

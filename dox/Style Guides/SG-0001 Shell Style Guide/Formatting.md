# Formatting {#ref_formatting}

## Indentation {#ref_indentation}


### Rule 2.1

Do use 2 spaces for indentation.

Do not use tabs.

Why? A tab could be a different number of columns depending on environment, but a space is always one column.

```
find ${DOX_DIR} -type f -name 'Doxyfile' -print0 |  while IFS= read -r -d $'\0' DOXYFILE; do

  spec_dir="${DOXYFILE%/*}"
  spec_name="${SPEC_DIR##*/}"

  revision_history=RevisionHistory
  revision_history_md="${revision_history.md}"
  revision_history_tex="latex/${revision_history.tex}"

  # Generate latex for Revision History
  cd "${SPEC_DIR}"

  if [[ ! -d latex ]]; then
    mkdir latex
  fi

  # ...
done
```

## User defined variable {#ref_formatting_user_defined_variable}

### Rule 2.2

Do declare all global varables at the top of a script file.

Why? Shell script allows to use variables after declaration.

Why? Grouping of the variables at the top of the script is important for someone else to be informed which variables are used in the script and in order to change the value of any variable.

@code
#!/bin/bash

PLANTUML_STYLE=$1
if [[ -z "${PLANTUML_STYLE}" ]]; then
  PLANTUML_STYLE=classic
fi

TARGET=$2
# Some checkings for TARGET

TARGET_ANDROID="android"
TARGET_IOS="ios"
TARGET_WINDOWS="windows"

if [[ "${TARGET}" == "${TARGET_ANDROID}" ]]; then
  CMAKE="$ANDROID_PATH/cmake/$CMAKE_VERSION/bin/cmake"
else
  CMAKE=cmake
fi
@endcode

# Paths {#ref_paths}

## Current directory {#ref_current_directory}

### Rule 4.1

Do use an example script to get current directory path.

Why? In this example it checks operating system and gets current directory, to enable scripts to operate in cross-platform environment.

@code
#!/bin/bash
DARWIN="Darwin"
LINUX="Linux"
if [[ $(uname -s) != "${DARWIN}" && $(uname -s) != "${LINUX}" ]]; then
  CURRENT_DIR=$(pwd -W)
else
  CURRENT_DIR=$(pwd)
fi
@endcode

## Path of the executable {#ref_path_of_the_executable}

### Rule 4.2

Do use the example script to get the path of the executable.

Why? Example gets the relative path, which is necessary to get a full paths. (See [Relative Paths](@ref ref_relative_paths))

@code
#!/bin/bash

EXECUTABLE_DIR=$(dirname $0);
@endcode

## Paths concatination {#ref_paths_concatination}

### Rule 4.3

Do use double quotes <b>""</b> for path concatination.

Why? In order to avoid problems when path contains files/folders with space, the double quotes is always used in path concatination.

@code
STYLE_GUIDES_DIR="Dox/Style Guides"
SHELL_STYLE_GUIDE_PATH="${STYLE_GUIDES_DIR}/SG-0003 Shell Style"
@endcode

## Relative paths {#ref_relative_paths}

### Rule 4.4

Do use _relative path_ relative to the executable path.

Do add _executable path_ to the _relative path_.

Why? Adding executable path to the relative path gets the absolute path.

Why? Using absolute path, there is no need to resolve any problems of path.

@code
#!/bin/bash

DARWIN="Darwin"
LINUX="Linux"
EXECUTABLE_DIR=$(dirname $0)

if [[ ! "${EXECUTABLE_DIR}" = "/*" ]]; then
  if [[ $(uname -s) != "${DARWIN}" && $(uname -s) != "${LINUX}" ]]; then
    CURRENT_DIR=$(pwd -W)
  else
    CURRENT_DIR=$(pwd)
  fi
  EXECUTABLE_DIR="${CURRENT_DIR}/${EXECUTABLE_DIR}"
fi

TEMPLATES_DIR="${EXECUTABLE_DIR}/../Templates"

for file in $(ls "${TEMPLATES_DIR/*.html}"); do
  base=${file##*/}
  name=${base%.*}

  echo ${base}
  echo ${name}
done
@endcode

## Path in expression {#ref_path_in_expression}

### Rule 4.5

Do use double quotes "" for the path in expressions.

Why? When defined path has a space, without quotes path does not work correctly.

@code
DATABASE="${EXECUTABLE_DIR}/Database Sqlite/screens.sqlite"
SOURCE="${EXECUTABLE_DIR}/Database Sqlite/screens.xml"
TEMP="${EXECUTABLE_DIR}/Database Sqlite/screens.csv"
REMOVE_DB_IF_NOT_UP_TO_DATE="${EXECUTABLE_DIR}/Database Sqlite/remove_screens_db_if_not_up_to_date.make"

if [[ ! -e "${SOURCE}" ]]; then
  echo "${SOURCE} does not exist. Aborting."
  exit 1
fi

if [[ -e "${DATABASE}" ]; then
  make -f "${REMOVE_DB_IF_NOT_UP_TO_DATE}"
  if [[ -e "${DATABASE}" ]]; then
    echo "Database $(basename ${DATABASE}) exists and is up to date."
    exit 0
  fi
fi
@endcode

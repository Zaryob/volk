#
# Copyright 2013, 2014 Free Software Foundation, Inc.
#
# This file is part of VOLK
#
# SPDX-License-Identifier: LGPL-3.0-or-later
#

########################################################################
# Write the python helper script that generates byte code files
########################################################################
file(
    WRITE ${CMAKE_BINARY_DIR}/python_compile_helper.py
    "
import sys, py_compile
files = sys.argv[1:]
srcs, gens = files[:len(files)//2], files[len(files)//2:]
for src, gen in zip(srcs, gens):
    py_compile.compile(file=src, cfile=gen, doraise=True)
")

########################################################################
# Install python files and apps
########################################################################
include(VolkPython)

volk_python_install(
    FILES
    __init__.py
    cfg.py
    volk_modtool_generate.py
    DESTINATION
    ${VOLK_PYTHON_DIR}/volk_modtool
    COMPONENT
    "volk")

volk_python_install(PROGRAMS volk_modtool DESTINATION ${VOLK_RUNTIME_DIR} COMPONENT
                    "volk")

# Automake file

# Nonstandard package files for distribution
EXTRA_DIST = \
  CHANGES \
  CONTRIBUTORS \
  scripts/gen_gtest_pred_impl.py

# TODO(wan@google.com): integrate scripts/gen_gtest_pred_impl.py into
#   the build system such that a user can specify the maximum predicate
#   arity here and have the script automatically generate the
#   corresponding .h and .cc files.

# Scripts and utilities
bin_SCRIPTS = scripts/gtest-config
CLEANFILES = $(bin_SCRIPTS)

# Distribute and install M4 macro
m4datadir = $(datadir)/aclocal
m4data_DATA = m4/gtest.m4
EXTRA_DIST += $(m4data_DATA)

# We define the global AM_CPPFLAGS as everything we compile includes from these
# directories.
AM_CPPFLAGS = -I$(srcdir) -I$(srcdir)/include

# Build rules for libraries.
lib_LTLIBRARIES = lib/libgtest.la lib/libgtest_main.la

lib_libgtest_la_SOURCES = src/gtest.cc \
                          src/gtest-death-test.cc \
                          src/gtest-filepath.cc \
                          src/gtest-internal-inl.h \
                          src/gtest-port.cc

pkginclude_HEADERS = include/gtest/gtest.h \
                     include/gtest/gtest-death-test.h \
                     include/gtest/gtest-message.h \
                     include/gtest/gtest-spi.h \
                     include/gtest/gtest_pred_impl.h \
                     include/gtest/gtest_prod.h

pkginclude_internaldir = $(pkgincludedir)/internal
pkginclude_internal_HEADERS = \
  include/gtest/internal/gtest-death-test-internal.h \
  include/gtest/internal/gtest-filepath.h \
  include/gtest/internal/gtest-internal.h \
  include/gtest/internal/gtest-port.h \
  include/gtest/internal/gtest-string.h

lib_libgtest_main_la_SOURCES = src/gtest_main.cc
lib_libgtest_main_la_LIBADD = lib/libgtest.la

# Bulid rules for samples and tests. Automake's naming for some of
# these variables isn't terribly obvious, so this is a brief
# reference:
#
# TESTS -- Programs run automatically by "make check"
# check_PROGRAMS -- Programs built by "make check" but not necessarily run

noinst_LTLIBRARIES = samples/libsamples.la

samples_libsamples_la_SOURCES = samples/sample1.cc \
                                samples/sample1.h \
                                samples/sample2.cc \
                                samples/sample2.h \
                                samples/sample3-inl.h \
                                samples/sample4.cc \
                                samples/sample4.h

TESTS=
TESTS_ENVIRONMENT = GTEST_SOURCE_DIR="$(srcdir)/test" \
                    GTEST_BUILD_DIR="$(top_builddir)/test"
check_PROGRAMS=

TESTS += samples/sample1_unittest
check_PROGRAMS += samples/sample1_unittest
samples_sample1_unittest_SOURCES = samples/sample1_unittest.cc
samples_sample1_unittest_LDADD = lib/libgtest_main.la \
                                 samples/libsamples.la

TESTS += samples/sample2_unittest
check_PROGRAMS += samples/sample2_unittest
samples_sample2_unittest_SOURCES = samples/sample2_unittest.cc
samples_sample2_unittest_LDADD = lib/libgtest_main.la \
                                 samples/libsamples.la

TESTS += samples/sample3_unittest
check_PROGRAMS += samples/sample3_unittest
samples_sample3_unittest_SOURCES = samples/sample3_unittest.cc
samples_sample3_unittest_LDADD = lib/libgtest_main.la \
                                 samples/libsamples.la

TESTS += samples/sample4_unittest
check_PROGRAMS += samples/sample4_unittest
samples_sample4_unittest_SOURCES = samples/sample4_unittest.cc
samples_sample4_unittest_LDADD = lib/libgtest_main.la \
                                 samples/libsamples.la

TESTS += samples/sample5_unittest
check_PROGRAMS += samples/sample5_unittest
samples_sample5_unittest_SOURCES = samples/sample5_unittest.cc
samples_sample5_unittest_LDADD = lib/libgtest_main.la \
                                 samples/libsamples.la

TESTS += test/gtest_unittest
check_PROGRAMS += test/gtest_unittest
test_gtest_unittest_SOURCES = test/gtest_unittest.cc
test_gtest_unittest_LDADD = lib/libgtest.la

TESTS += test/gtest-death-test_test
check_PROGRAMS += test/gtest-death-test_test
test_gtest_death_test_test_SOURCES = test/gtest-death-test_test.cc
test_gtest_death_test_test_CXXFLAGS = $(AM_CXXFLAGS) -pthread
test_gtest_death_test_test_LDADD = -lpthread lib/libgtest_main.la

TESTS += test/gtest-filepath_test
check_PROGRAMS += test/gtest-filepath_test
test_gtest_filepath_test_SOURCES = test/gtest-filepath_test.cc
test_gtest_filepath_test_LDADD = lib/libgtest_main.la

TESTS += test/gtest-message_test
check_PROGRAMS += test/gtest-message_test
test_gtest_message_test_SOURCES = test/gtest-message_test.cc
test_gtest_message_test_LDADD = lib/libgtest_main.la

TESTS += test/gtest-options_test
check_PROGRAMS += test/gtest-options_test
test_gtest_options_test_SOURCES = test/gtest-options_test.cc
test_gtest_options_test_LDADD = lib/libgtest_main.la

TESTS += test/gtest_pred_impl_unittest
check_PROGRAMS += test/gtest_pred_impl_unittest
test_gtest_pred_impl_unittest_SOURCES = test/gtest_pred_impl_unittest.cc
test_gtest_pred_impl_unittest_LDADD = lib/libgtest_main.la

TESTS += test/gtest_environment_test
check_PROGRAMS += test/gtest_environment_test
test_gtest_environment_test_SOURCES = test/gtest_environment_test.cc
test_gtest_environment_test_LDADD = lib/libgtest.la

TESTS += test/gtest_no_test_unittest
check_PROGRAMS += test/gtest_no_test_unittest
test_gtest_no_test_unittest_SOURCES = test/gtest_no_test_unittest.cc
test_gtest_no_test_unittest_LDADD = lib/libgtest.la

TESTS += test/gtest_main_unittest
check_PROGRAMS += test/gtest_main_unittest
test_gtest_main_unittest_SOURCES = test/gtest_main_unittest.cc
test_gtest_main_unittest_LDADD = lib/libgtest_main.la

TESTS += test/gtest_prod_test
check_PROGRAMS += test/gtest_prod_test
test_gtest_prod_test_SOURCES = test/gtest_prod_test.cc \
                               test/production.cc \
                               test/production.h
test_gtest_prod_test_LDADD = lib/libgtest_main.la

TESTS += test/gtest_repeat_test
check_PROGRAMS += test/gtest_repeat_test
test_gtest_repeat_test_SOURCES = test/gtest_repeat_test.cc
test_gtest_repeat_test_LDADD = lib/libgtest.la

TESTS += test/gtest_stress_test
check_PROGRAMS += test/gtest_stress_test
test_gtest_stress_test_SOURCES = test/gtest_stress_test.cc
test_gtest_stress_test_LDADD = lib/libgtest.la

# The following tests depend on the presence of a Python installation and are
# keyed off of it. TODO(chandlerc@google.com): While we currently only attempt
# to build and execute these tests if Autoconf has found Python v2.4 on the
# system, we don't use the PYTHON variable it specified as the valid
# interpreter. The problem is that TESTS_ENVIRONMENT is a global variable, and
# thus we cannot distinguish between C++ unit tests and Python unit tests.
if HAVE_PYTHON
check_SCRIPTS =

# These two Python modules are used by multiple Pythong tests below.
check_SCRIPTS += test/gtest_test_utils.py \
                 test/gtest_xml_test_utils.py

check_PROGRAMS += test/gtest_output_test_
test_gtest_output_test__SOURCES = test/gtest_output_test_.cc
test_gtest_output_test__LDADD = lib/libgtest.la
check_SCRIPTS += test/gtest_output_test.py
EXTRA_DIST += test/gtest_output_test_golden_lin.txt \
              test/gtest_output_test_golden_win.txt
TESTS += test/gtest_output_test.py

check_PROGRAMS += test/gtest_color_test_
test_gtest_color_test__SOURCES = test/gtest_color_test_.cc
test_gtest_color_test__LDADD = lib/libgtest.la
check_SCRIPTS += test/gtest_color_test.py
TESTS += test/gtest_color_test.py

check_PROGRAMS += test/gtest_env_var_test_
test_gtest_env_var_test__SOURCES = test/gtest_env_var_test_.cc
test_gtest_env_var_test__LDADD = lib/libgtest.la
check_SCRIPTS += test/gtest_env_var_test.py
TESTS += test/gtest_env_var_test.py

check_PROGRAMS += test/gtest_filter_unittest_
test_gtest_filter_unittest__SOURCES = test/gtest_filter_unittest_.cc
test_gtest_filter_unittest__LDADD = lib/libgtest.la
check_SCRIPTS += test/gtest_filter_unittest.py
TESTS += test/gtest_filter_unittest.py

check_PROGRAMS += test/gtest_break_on_failure_unittest_
test_gtest_break_on_failure_unittest__SOURCES = \
  test/gtest_break_on_failure_unittest_.cc
test_gtest_break_on_failure_unittest__LDADD = lib/libgtest.la
check_SCRIPTS += test/gtest_break_on_failure_unittest.py
TESTS += test/gtest_break_on_failure_unittest.py

check_PROGRAMS += test/gtest_list_tests_unittest_
test_gtest_list_tests_unittest__SOURCES = test/gtest_list_tests_unittest_.cc
test_gtest_list_tests_unittest__LDADD = lib/libgtest.la
check_SCRIPTS += test/gtest_list_tests_unittest.py
TESTS += test/gtest_list_tests_unittest.py

check_PROGRAMS += test/gtest_xml_output_unittest_
test_gtest_xml_output_unittest__SOURCES = test/gtest_xml_output_unittest_.cc
test_gtest_xml_output_unittest__LDADD = lib/libgtest_main.la
check_SCRIPTS += test/gtest_xml_output_unittest.py
TESTS += test/gtest_xml_output_unittest.py

check_PROGRAMS += test/gtest_xml_outfile1_test_
test_gtest_xml_outfile1_test__SOURCES = test/gtest_xml_outfile1_test_.cc
test_gtest_xml_outfile1_test__LDADD = lib/libgtest_main.la
check_PROGRAMS += test/gtest_xml_outfile2_test_
test_gtest_xml_outfile2_test__SOURCES = test/gtest_xml_outfile2_test_.cc
test_gtest_xml_outfile2_test__LDADD = lib/libgtest_main.la
check_SCRIPTS += test/gtest_xml_outfiles_test.py
TESTS += test/gtest_xml_outfiles_test.py

check_PROGRAMS += test/gtest_uninitialized_test_
test_gtest_uninitialized_test__SOURCES = test/gtest_uninitialized_test_.cc
test_gtest_uninitialized_test__LDADD = lib/libgtest.la
check_SCRIPTS += test/gtest_uninitialized_test.py
TESTS += test/gtest_uninitialized_test.py

# TODO(wan@google.com): make the build script compile and run the
#   negative-compilation tests.  (The test/gtest_nc* files are unfinished
#   implementation of tests for verifying that certain kinds of misuse
#   of Google Test don't compile.)
EXTRA_DIST += $(check_SCRIPTS) \
              test/gtest_nc.cc \
              test/gtest_nc_test.py

endif

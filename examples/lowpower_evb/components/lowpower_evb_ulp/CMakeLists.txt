
set(COMPONENT_SRCS "lowpower_evb_ulp_opt.cpp")

set(COMPONENT_ADD_INCLUDEDIRS ". include")

set(COMPONENT_REQUIRES soc lowpower_framework ulp)

register_component()

#
# ULP support additions to component makefile.
#
# 1. ULP_APP_NAME must be unique (if multiple components use ULP)
#    Default value, override if necessary:
set(ULP_APP_NAME ulp_${COMPONENT_NAME})
#
# 2. Specify all assembly source files here.
#    Files should be placed into a separate directory (in this case, ulp/),
#    which should not be added to COMPONENT_SRCS.
set(ULP_S_SOURCES "ulp/bh1750.S"
                    "ulp/hts221.S"
                    "ulp/i2c_dev.S"
                    "ulp/i2c.S"
                    "ulp/stack.S")
#
# 3. List all the component source files which include automatically
#    generated ULP export file, $(ULP_APP_NAME).h:
set(ULP_EXP_DEP_SRCS "lowpower_evb_ulp_opt.cpp")
#
# 4. Include build rules for ULP program
# End of ULP support additions to component makefile.
#
include($ENV{IDF_PATH}/components/ulp/component_ulp_common.cmake)

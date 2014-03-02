# We define a set here to hold all of the source files we want to compile. This
# is done mostly for convenience and future-proofing

set(shadoe_srcs main.c)

# Here, we compile all of the source files into the shadoe executable.

add_executable(shadoe ${shadoe_srcs})

# And finally, we tell cmake to install the shadoe executable into 
# /usr/local/bin. Note that we label shadoe as RUNTIME which is used for 
# when we install executable files.

install(TARGETS shadoe RUNTIME DESTINATION ${CMAKE_INSTALL_PREFIX}/bin)


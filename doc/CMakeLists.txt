# For this one, we install the man page, stjerm.8 into the correct man page
# directory.  We classify this as a FILE since it doesn't fit into the TARGETS
# type. That is, this is basically just a regular file and not an executable,
# library, source, etc.

install(FILES shadoe-qt.8 DESTINATION ${CMAKE_INSTALL_PREFIX}/share/man/man8/)

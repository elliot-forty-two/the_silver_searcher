cmake_minimum_required (VERSION 2.8)
message ("-- Configuring man pages")
set (man_FILES ag.1)

install (FILES ${man_FILES} DESTINATION man/man1)


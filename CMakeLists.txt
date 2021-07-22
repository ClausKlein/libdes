cmake_minimum_required(VERSION 3.14...3.21)

# libdes-l-4.01a from
# https://agentpp.com/download/libdes-l-4.01a.tar.gz
#
project(
  des
  VERSION 4.1.1
  LANGUAGES C
)

add_library(
  des STATIC
  des.h
  cbc_enc.c
  ncbc_enc.c
  ecb_enc.c
  ede_enc.c
  fcrypt.c
  set_key.c
  des_enc.c
)
target_compile_definitions(des PRIVATE LIBDES_LIT)

install(TARGETS des LIBRARY)
install(FILES des.h TYPE INCLUDE)


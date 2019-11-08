add_library(mylib
   my_args.F90
   )

target_link_libraries(mylib PUBLIC FLAP::FLAP)
#target_link_libraries(mylib PUBLIC FLAP)

add_executable(main.exe main.F90)
target_link_libraries(main.exe LINK_PUBLIC mylib)

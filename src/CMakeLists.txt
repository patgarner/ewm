cmake_minimum_required(VERSION 3.9)
project(EWM)

set(CMAKE_C_FLAGS "-O3 -flto")
set(LINKER_FLAGS "-flto")

include_directories(AFTER SYSTEM /usr/local/include)
link_directories(/usr/local/lib)

set(CPU_SOURCES cpu.c mem.c fmt.c ins.c utl.c)
set(SDL_SOURCES sdl.c)

set(BOO_SOURCES boo.c tty.c chr.c)
set(ONE_SOURCES one.c tty.c chr.c pia.c)
set(TWO_SOURCES two.c scr.c dsk.c chr.c alc.c)

add_executable(cpu_test ${CPU_SOURCES} cpu_test.c)

add_executable(cpu_bench ${CPU_SOURCES} cpu_bench.c)

add_executable(ewm ${CPU_SOURCES} ${BOO_SOURCES} ${ONE_SOURCES} ${TWO_SOURCES} ${SDL_SOURCES} ewm.c)
target_link_libraries(ewm SDL2)

add_executable(tty_test ${CPU_SOURCES} ${ONE_SOURCES} ${SDL_SOURCES} tty_test.c)
target_link_libraries(tty_test SDL2)

add_executable(scr_test ${CPU_SOURCES} ${TWO_SOURCES} ${SDL_SOURCES} scr_test.c)
target_link_libraries(scr_test SDL2)

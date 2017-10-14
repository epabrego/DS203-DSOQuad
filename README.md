WildcatV5.6 for HW 2.72 and older DEVICES ONLY
=
WildcatV6.5 for HW 2.81 and later DEVICES ONLY
=
How to compile on a Windows Machine
===================================
Choice an option:
- Option 1. Download Exe Installer
   https://sourcery.mentor.com/public/gnu_toolchain/arm-none-eabi/arm-2014.05-28-arm-none-eabi.exe

- Option 2. Download Standalone archive
   https://sourcery.mentor.com/public/gnu_toolchain/arm-none-eabi/arm-2014.05-28-arm-none-eabi-i686-mingw32.tar.bz2
   Add C:\arm-2008q1\bin to system PATH


Download DS203 source and extract 
-
- click the green [Clone or download] button on github, then [Download zip]
- Extract the dso203-master.zip somewhere

Open a new Command Prompt Window
-
- in the Command Prompt, CD into Wildcat directory with all the source files from above step

Test the compiler
-
- type: arm-none-eabi-gcc.exe -v
- output:
Using built-in specs.
COLLECT_GCC=arm-none-eabi-gcc
COLLECT_LTO_WRAPPER=c:/arm-2014.05/bin/../libexec/gcc/arm-none-eabi/4.8.3/lto-wrapper.exe
Target: arm-none-eabi
Configured with: /scratch/maciej/arm-eabi-2014.05-rel/src/gcc-4.8-2014.05/configure --build=i686-pc-linux-gnu --host=i686-mingw32 --target=arm-none-eabi --enable-threads --disable-libmudflap --disable-libssp --disable-libstdcxx-pch --enable-extra-sgxxlite-multilibs --with-gnu-as
--with-gnu-ld --with-specs='%{save-temps: -fverbose-asm} -D__CS_SOURCERYGXX_MAJ__=2014 -D__CS_SOURCERYGXX_MIN__=5 -D__CS_SOURCERYGXX_REV__=28' --enable-languages=c,c++ --disable-shared --enable-lto --with-newlib --with-pkgversion='Sourcery CodeBench Lite 2014.05-28' --with-bugurl
=https://sourcery.mentor.com/GNUToolchain/ --disable-nls --prefix=/opt/codesourcery --with-headers=yes --with-sysroot=/opt/codesourcery/arm-none-eabi --with-build-sysroot=/scratch/maciej/arm-eabi-2014.05-rel/install/host-i686-mingw32/opt/codesourcery/arm-none-eabi --with-libiconv
-prefix=/scratch/maciej/arm-eabi-2014.05-rel/obj/pkg-2014.05-28-arm-none-eabi/arm-2014.05-28-arm-none-eabi.extras/host-libs-i686-mingw32/usr --with-gmp=/scratch/maciej/arm-eabi-2014.05-rel/obj/pkg-2014.05-28-arm-none-eabi/arm-2014.05-28-arm-none-eabi.extras/host-libs-i686-mingw32
/usr --with-mpfr=/scratch/maciej/arm-eabi-2014.05-rel/obj/pkg-2014.05-28-arm-none-eabi/arm-2014.05-28-arm-none-eabi.extras/host-libs-i686-mingw32/usr --with-mpc=/scratch/maciej/arm-eabi-2014.05-rel/obj/pkg-2014.05-28-arm-none-eabi/arm-2014.05-28-arm-none-eabi.extras/host-libs-i68
6-mingw32/usr --with-isl=/scratch/maciej/arm-eabi-2014.05-rel/obj/pkg-2014.05-28-arm-none-eabi/arm-2014.05-28-arm-none-eabi.extras/host-libs-i686-mingw32/usr --with-cloog=/scratch/maciej/arm-eabi-2014.05-rel/obj/pkg-2014.05-28-arm-none-eabi/arm-2014.05-28-arm-none-eabi.extras/hos
t-libs-i686-mingw32/usr --disable-libgomp --disable-libitm --disable-libatomic --disable-libssp --enable-poison-system-directories --with-build-time-tools=/scratch/maciej/arm-eabi-2014.05-rel/obj/tools-i686-pc-linux-gnu-2014.05-28-arm-none-eabi-i686-mingw32/arm-none-eabi/bin --wi
th-build-time-tools=/scratch/maciej/arm-eabi-2014.05-rel/obj/tools-i686-pc-linux-gnu-2014.05-28-arm-none-eabi-i686-mingw32/arm-none-eabi/bin SED=sed
Thread model: single
gcc version 4.8.3 20140320 (prerelease) (Sourcery CodeBench Lite 2014.05-28)


Lets build the binary
-
- type: cs-make
- output:
arm-none-eabi-gcc -Wall -O2 -I. -Iinc  -Werror -mcpu=cortex-m3 -mthumb -fno-common -fzero-initialized-in-bss -msoft-float -MD -I FWLib/inc -c -o Calibrat.o Calibrat.c
arm-none-eabi-gcc -Wall -O2 -I. -Iinc  -Werror -mcpu=cortex-m3 -mthumb -fno-common -fzero-initialized-in-bss -msoft-float -MD -I FWLib/inc -c -o Draw.o Draw.c
arm-none-eabi-gcc -Wall -O2 -I. -Iinc  -Werror -mcpu=cortex-m3 -mthumb -fno-common -fzero-initialized-in-bss -msoft-float -MD -I FWLib/inc -c -o Files.o Files.c
arm-none-eabi-gcc -Wall -O2 -I. -Iinc  -Werror -mcpu=cortex-m3 -mthumb -fno-common -fzero-initialized-in-bss -msoft-float -MD -I FWLib/inc -c -o Function.o Function.c
arm-none-eabi-gcc -Wall -O2 -I. -Iinc  -Werror -mcpu=cortex-m3 -mthumb -fno-common -fzero-initialized-in-bss -msoft-float -MD -I FWLib/inc -c -o Interrupt.o Interrupt.c
arm-none-eabi-gcc -Wall -O2 -I. -Iinc  -Werror -mcpu=cortex-m3 -mthumb -fno-common -fzero-initialized-in-bss -msoft-float -MD -I FWLib/inc -c -o Main.o Main.c
arm-none-eabi-gcc -Wall -O2 -I. -Iinc  -Werror -mcpu=cortex-m3 -mthumb -fno-common -fzero-initialized-in-bss -msoft-float -MD -I FWLib/inc -c -o Menu.o Menu.c
arm-none-eabi-gcc -Wall -O2 -I. -Iinc  -Werror -mcpu=cortex-m3 -mthumb -fno-common -fzero-initialized-in-bss -msoft-float -MD -I FWLib/inc -c -o Process.o Process.c
arm-none-eabi-gcc    -c -o BIOS.o BIOS.S
arm-none-eabi-gcc -Wall -O2 -I. -Iinc  -Werror -mcpu=cortex-m3 -mthumb -fno-common -fzero-initialized-in-bss -msoft-float -MD -I FWLib/inc -c -o startup.o startup.c
arm-none-eabi-gcc -Wall -O2 -I. -Iinc  -Werror -mcpu=cortex-m3 -mthumb -fno-common -fzero-initialized-in-bss -msoft-float -MD -I FWLib/inc -c -o stm32f10x_nvic.o stm32f10x_nvic.c
arm-none-eabi-gcc -mcpu=cortex-m3 -mthumb  -c -o cortexm3_macro.o cortexm3_macro.S
arm-none-eabi-gcc -o app1.elf Calibrat.o Draw.o Files.o Function.o Interrupt.o Main.o Menu.o Process.o BIOS.o startup.o stm32f10x_nvic.o cortexm3_macro.o -mcpu=cortex-m3 -lc -mthumb -march=armv7 -mfix-cortex-m3-ldrd -msoft-float -nostartfiles -Wl,-Map,app1.map -T app1.lds
arm-none-eabi-objcopy -O ihex app1.elf app1.hex
rm app1.elf


You should find the compiled firmware file app1.hex (428,496 bytes)
-
- Put your DS203 into DFU mode (press and hold >|| button and power on) and copy the app1.hex to drive.

Optional for HW 2.81 and later DEVICES ONLY
-
-To get full speed oversampling, copy FPGA_281.ADR then FPGA_281.BIN in DFU mode to the device.

Credits and contributors:
======================
- jakub.jelinek
- Wildcat
- Seeed-Studio
- Marco Sinatti (marcosin)
- Gabriel Valky (gabonator1)
- pmoss69
- JackTheVendicator
- bobtidey 
- JPA 
- Jerson 
- original authors minidso

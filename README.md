# VC6-SP6-Enterprise

This repository contains a portable installation of Visual Studio 6.0 Enterprise with the latest Service Packs and updates included. 
Using this, it is possible to build VC6 projects on modern Windows versions without going through the hassle of manually installing VC6 first. Any files not essential for building VC6 projects were excluded to save space.

Besides the base Visual Studio 6.0 Enterprise installation, additional updates were installed in the following order:
- Visual Studio 6.0 Service Pack 6.0
- KB3096896
- Visual C++ 6.0 Processor Pack (vcpp5.exe)

## Usage instruction
After cloning the VC6-SP6-Enterprise repository, run the `VC98\Bin\VCVARS32.BAT` script in a command-line window. 
The common build tools such as `NMAKE`, `CL`, `LINK`, `RC`, and `LIB` should now be available during the command-line session. 
Works without issues on Windows 11 25H2 as of 16/06/2026.

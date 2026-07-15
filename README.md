# VC6-SP6-Enterprise

This repository contains a portable installation of Visual Studio 6.0 Enterprise with the latest Service Packs and updates included. 
Using this, it is possible to build VC6 projects on modern Windows versions without going through the hassle of manually installing VC6 first. Any files not essential for building VC6 projects were excluded to save space.

Besides the base Visual Studio 6.0 Enterprise installation, additional updates were installed in the following order:
1. Visual Studio 6.0 Service Pack 6
2. KB3096896
3. Visual C++ 6.0 Processor Pack (vcpp5.exe)

## Usage instructions
After cloning the VC6-SP6-Enterprise repository, run the `VC98\Bin\VCVARS32.BAT` script in a command-line window. 
The common build tools such as `NMAKE`, `CL`, `LINK`, `RC`, and `LIB` should now be available during the command-line session. 
These tools work without issues on Windows 11 25H2 as of 16/06/2026.

Here is a GitHub workflow script that can be used to compile VC6 project and upload their binaries as artifacts:
```yml
name: Build release

on:
  push:
    branches:
      - main
  pull_request:
  workflow_dispatch:

jobs:
  build:
    runs-on: windows-latest
    defaults:
      run:
        shell: cmd
    steps:
      - uses: actions/checkout@v6
        with:
          path: project
          ref: ${{ github.ref }}

      - name: Checkout VC6 build tools
        uses: actions/checkout@v6
        with:
          repository: FLHDE/VC6-SP6-Enterprise
          path: VC6

      - name: Build project with VC6
        run: |
          call "${{ github.workspace }}\VC6\VC98\Bin\VCVARS32.BAT"
          cd project
          nmake /nologo

      - name: Upload release build as artifact
        uses: actions/upload-artifact@v7
        with:
          name: Release build
          path: |
            project/*.exe
			project/*.dll
```

This workflow works on the `windows-latest` runner as of 15/07/2026.

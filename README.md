--------------------------------------------------------------------
  Super Tux Kart (STK2) – Quick-Start Cheat-Sheet
────────────────────────────────────────────────────────────────────
  Folder layout expected:

    STK2/
      ├─ stk-code2/     ←  build this engine
      ├─ stk-assets/    ←  game data (tracks, music, etc.)
      └─ stk-code/      ←  Ignore/delete

  Copy-paste the sections that match your OS.
--------------------------------------------------------------------

────────────────────────────────────────────────────────────────────
1. ONE-TIME PREREQUISITES
────────────────────────────────────────────────────────────────────

macOS:

  • Install Apple command-line tools
    xcode-select --install
  • Homebrew + dev libs:

    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

    brew install git cmake \
         sdl2 sdl2_image sdl2_mixer sdl2_ttf \
         glew eigen harfbuzz libogg libvorbis libpng jpeg-turbo \
         openal-soft

Windows:

  1. Visual Studio 2022 → workload “Desktop development with C++”
  2. Git for Windows
  3. Download dependencies pack
       https://github.com/supertuxkart/dependencies/releases/latest
       choose dependencies-win-x86_64.zip
       unzip inside stk-code2\ and rename folder to dependencies-win64

────────────────────────────────────────────────────────────────────
2. CLONE THE REPO
────────────────────────────────────────────────────────────────────
    Go to directory you want the repo to exist in

macOS:

    git clone https://github.com/gurrahmed/STK2.git
    cd STK2

Windows (PowerShell / CMD):

    git clone https://github.com/gurrahmed/STK2.git
    cd STK2

Directory check:

    STK2/
     ├─ stk-code2/
     ├─ stk-assets/
     └─ stk-code/ ←  Ignore/delete


────────────────────────────────────────────────────────────────────
3. CONFIGURE & BUILD stk-code2
────────────────────────────────────────────────────────────────────

macOS:

    cd stk-code2
    mkdir build && cd build
    cmake .. -DCMAKE_BUILD_TYPE=Release -DNO_SHADERC=ON
    make -j"$(sysctl -n hw.logicalcpu)"

Windows  (x64 Native Tools Prompt):

    cd stk-code2
    mkdir build & cd build
    cmake .. -G "Visual Studio 17 2022" -A x64 -DNO_SHADERC=ON
    cmake --build . --config Release

────────────────────────────────────────────────────────────────────
4. RUN THE GAME
────────────────────────────────────────────────────────────────────

macOS:

    open bin/SuperTuxKart.app         # or: ./bin/supertuxkart

Windows:

    .\bin\Release\supertuxkart.exe

If assets are not found
    macOS    export STK_ASSETS=~/Dev/STK2/stk-assets
    Windows  set STK_ASSETS=C:\STK\STK2\stk-assets

────────────────────────────────────────────────────────────────────
5. DAILY UPDATE WORKFLOW
────────────────────────────────────────────────────────────────────

    cd STK2/stk-code2
    git pull origin main              # or master
    cd build
    macOS      make -j"$(sysctl -n hw.logicalcpu)"
    Windows    cmake --build . --config Release

────────────────────────────────────────────────────────────────────
6. QUICK CARDS
────────────────────────────────────────────────────────────────────

Best Practice:

Create shortcuts for your-folder\STK2\stk-code2\build\bin\Release\supertuxkart.exe (NONE TERMINAL)

macOS:

    cd ~/Dev/STK2/stk-code2/build
    open bin/SuperTuxKart.app

Windows:

    cd C:\STK\STK2\stk-code2\build
    .\bin\Release\supertuxkart.exe

────────────────────────────────────────────────────────────────────
7. OBS
────────────────────────────────────────────────────────────────────
• Install OBS Studio  
  macOS   →  `brew install --cask obs`  
  Windows →  download installer from https://obsproject.com

• First run ⇒ Auto-Configuration Wizard  
  – Pick “Optimize for recording”.

• Add a Source For STK 
      +  ➜  “Window Capture” (best with STK in fullscreen)

• Add D-Pad Overlay  
  macOS:  
      ➜  Open System Settings → Keyboard → “Keyboard Viewer”.  
         – The on-screen keyboard pops up; drag it to a corner, resize small.  
         – In OBS ➜  +  ➜  “Window Capture” → pick “KeyboardViewer”.  
         – (Optional) Right-click source → Filters → Crop/Pad to trim empty edges.

  Windows:  
       ➜  Download & unzip * NohBoard * (<https://github.com/ThoNohT/NohBoard/releases>).  
         – Run NohBoard.exe → Layout → “Console (White)” or any D-Pad layout.  
         – Settings → Background opacity 0 %, Key opacity 100 %.  
         – In OBS ➜  +  ➜  “Window Capture” → choose the “NohBoard” window.  
         – Use “Alt + Drag” in OBS to crop to just the D-Pad if needed.

      +  ➜  Position the D-Pad source above the game feed; lock the layer.

• Hotkeys  
  Settings ➜ Hotkeys → assign “Start Recording” / “Stop Recording”.

• Output folder  
  Settings ➜ Output → Recording Path (default: Videos).  
  Recommended format: MKV (safer) then “Remux” to MP4 inside OBS if needed.


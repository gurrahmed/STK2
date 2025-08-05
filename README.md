# ────────────────────────────────────────────────────────────────────
#  SuperTuxKart (STK2) – Quick-Start Cheat-Sheet
# ────────────────────────────────────────────────────────────────────

# Folder layout expected:
#   STK2/
#     ├─ stk-code2/     ←  build this engine
#     ├─ stk-assets/    ←  game data (tracks, music, etc.)
#     └─ stk-code/      ←  Ignore/delete

# --------------------------------------------------------------------
# 1. ONE-TIME PREREQUISITES
# --------------------------------------------------------------------

# ───── macOS ─────

# Install Xcode CLI tools
xcode-select --install

# Install Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install dev dependencies
brew install git cmake \
     sdl2 sdl2_image sdl2_mixer sdl2_ttf \
     glew eigen harfbuzz libogg libvorbis libpng jpeg-turbo \
     openal-soft

# ───── Windows ─────

# 1. Install Visual Studio 2022 with “Desktop development with C++”
# 2. Install Git for Windows
# 3. Download dependencies pack:
#    https://github.com/supertuxkart/dependencies/releases/latest
#    → Choose dependencies-win-x86_64.zip
#    → Extract into stk-code2/ and rename to: dependencies-win64


# --------------------------------------------------------------------
# 2. CLONE THE REPO
# --------------------------------------------------------------------

# Clone repo
git clone https://github.com/gurrahmed/STK2.git
cd STK2

# Verify structure
#   STK2/
#     ├─ stk-code2/
#     ├─ stk-assets/
#     └─ stk-code/ ← ignore or delete


# --------------------------------------------------------------------
# 3. CONFIGURE & BUILD stk-code2
# --------------------------------------------------------------------

# ───── macOS ─────
cd stk-code2
mkdir build && cd build
cmake .. -DCMAKE_BUILD_TYPE=Release -DNO_SHADERC=ON
make -j"$(sysctl -n hw.logicalcpu)"

# ───── Windows (x64 Native Tools Prompt) ─────
cd stk-code2
mkdir build & cd build
cmake .. -G "Visual Studio 17 2022" -A x64 -DNO_SHADERC=ON
cmake --build . --config Release


# --------------------------------------------------------------------
# 4. RUN THE GAME
# --------------------------------------------------------------------

# ───── macOS ─────
open bin/SuperTuxKart.app     # or:
./bin/supertuxkart

# ───── Windows ─────
.\bin\Release\supertuxkart.exe

# If assets are not found:

# macOS:
export STK_ASSETS=~/Dev/STK2/stk-assets

# Windows:
set STK_ASSETS=C:\STK\STK2\stk-assets


# --------------------------------------------------------------------
# 5. DAILY UPDATE WORKFLOW
# --------------------------------------------------------------------

cd STK2/stk-code2
git pull origin main         # or: master
cd build

# macOS:
make -j"$(sysctl -n hw.logicalcpu)"

# Windows:
cmake --build . --config Release


# --------------------------------------------------------------------
# 6. QUICK LAUNCH SHORTCUTS
# --------------------------------------------------------------------

# ───── macOS ─────
cd ~/Dev/STK2/stk-code2/build
open bin/SuperTuxKart.app

# ───── Windows ─────
cd C:\STK\STK2\stk-code2\build
.\bin\Release\supertuxkart.exe


# --------------------------------------------------------------------
# 7. OBS OVERLAY SETUP
# --------------------------------------------------------------------

# ───── Install OBS ─────
# macOS:
brew install --cask obs

# Windows:
# Download installer: https://obsproject.com

# First Run → Auto-Configuration Wizard → Pick “Optimize for recording”

# ───── Add Game Source ─────
# In OBS: ➕ → “Window Capture” → select STK (fullscreen recommended)

# ───── Add D-Pad Overlay ─────

# macOS:
# - Open System Settings → Keyboard → “Keyboard Viewer”
# - On-screen keyboard appears → resize & position
# - In OBS: ➕ → “Window Capture” → select “KeyboardViewer”
# - (Optional) Right-click → Filters → Crop/Pad

# Windows:
# - Download: https://github.com/ThoNohT/NohBoard/releases
# - Run NohBoard.exe
#   → Layout: “Console (White)” or any D-Pad layout
#   → Settings: Background opacity 0%, Key opacity 100%
# - In OBS: ➕ → “Window Capture” → select NohBoard window
# - Use Alt + Drag in OBS to crop
# - Position above game feed and lock layer

# ───── Hotkeys ─────
# OBS: Settings → Hotkeys → assign “Start Recording” / “Stop Recording”

# ───── Output Folder ─────
# OBS: Settings → Output → Recording Path (default: Videos)
# Format: MKV (safer) → “Remux” to MP4 inside OBS if needed


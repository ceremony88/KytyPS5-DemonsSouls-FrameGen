# Third-party notices

This build of KytyPS5 is built with the software below (some of it only as headers or optional parts). Each one's license text is in `LICENSES\` (KytyPS5 and the
libraries of upstream's release) and `LICENSES\third-party\`; NVIDIA's are in `streamline\`.

## Source code

- **KytyPS5** (**GPL 2.0**, `LICENSE`; it grew from Kyty, MIT, `LICENSES\Kyty-MIT.txt`):
  https://github.com/chenxiao07/KytyPS5, release tag `v20261012`.
- **The complete source of this build**: the release's second download, `KytyPS5-DemonsSouls-FrameGen-source.zip`
  (the libraries under `3rdparty\` are git submodules there: their sources are at the links below).
- **This build's changes** alone: `source\local-changes.patch` in this package (apply with
  `git apply` in a checkout of `v20261012` with LF line endings, e.g. `git clone -c core.autocrlf=false`; then build as upstream describes, with `-DKYTY_STREAMLINE_SDK=<the
  NVIDIA Streamline SDK folder>` for frame generation and `-DKYTY_MARCH=x86-64-v3` for other PCs).

## Built into kyty_emulator.exe / kyty_shader_precompile.exe

| Library | License | Source |
|---|---|---|
| FFmpeg (libavcodec, libavformat, libavutil, libswresample, libswscale), statically linked | **LGPL 2.1 or later** (`third-party\FFmpeg-LGPL-2.1.txt`) | Prebuilt by shadPS4: https://github.com/shadps4-emu/ext-ffmpeg-core (commit `94dde08c8a9e4271a93a2a7e4159e9fb05d30c0a`, its `ffmpeg-windows` release; FFmpeg's own source at https://ffmpeg.org). To use a different FFmpeg build, rebuild KytyPS5 from the source above with that build in its place |
| SDL2 | zlib | https://github.com/libsdl-org/SDL |
| SPIRV-Tools, SPIRV-Headers | Apache 2.0 / MIT | https://github.com/KhronosGroup |
| Vulkan-Headers | Apache 2.0 / MIT | https://github.com/KhronosGroup/Vulkan-Headers |
| Vulkan Memory Allocator | MIT | https://github.com/GPUOpen-LibrariesAndSDKs/VulkanMemoryAllocator |
| Zydis | MIT | https://github.com/zyantific/zydis |
| xbyak | BSD 3-Clause | https://github.com/herumi/xbyak |
| zstd | BSD | https://github.com/facebook/zstd |
| ZArchive | MIT-0 | https://github.com/Exzap/ZArchive |
| fmt | MIT | https://github.com/fmtlib/fmt |
| spdlog | MIT | https://github.com/gabime/spdlog |
| nlohmann/json | MIT | https://github.com/nlohmann/json |
| Dear ImGui | MIT | https://github.com/ocornut/imgui |
| magic_enum | MIT | https://github.com/Neargye/magic_enum |
| xxHash | BSD 2-Clause | https://github.com/Cyan4973/xxHash |
| LibAtrac9 | MIT | https://github.com/Thealexbarney/LibAtrac9 |
| cpuinfo | BSD 2-Clause | https://github.com/pytorch/cpuinfo |
| stb | MIT / public domain | https://github.com/nothings/stb |
| Tracy (client) | BSD 3-Clause | https://github.com/wolfpld/tracy |
| RenderDoc API header | MIT | https://github.com/baldurk/renderdoc |

## Shipped next to the programs

| File | License |
|---|---|
| `libwinpthread-1.dll` (MinGW-w64 winpthreads) | MIT-style, `third-party\winpthread-COPYING` |
| `msvcp140*.dll`, `vcruntime140*.dll` | Microsoft Visual C++ Redistributable files, redistributable with applications under the Visual Studio license |
| `streamline\bin\x64\*` (NVIDIA Streamline, DLSS Frame Generation, Reflex) | Streamline MIT (`streamline\license.txt`, `streamline\3rd-party-licenses.md`); DLSS and Reflex runtime under NVIDIA's terms (`nvngx_dlss.license.txt`, `reflex.license.txt`) |


"%" means not tested by me personally.

## Reference material
- [syscall.sh](https://syscall.sh/): Linux ARMv7/AArch64/x86/x86_64 ABI and syscall tables
- %[C8051F34x_Glitch](https://github.com/debug-silicon/C8051F34x_Glitch): silicon glitching tutorial

## Disassemblers and decompilers
- [Binary Ninja](binary.ninja): interactive native code disassembler, decompiler, and debugger
	- [BinExport](https://github.com/google/binexport): companion tool for BinDiff
		- when building, replace the BN SDK it downloads with a path to BN API library
	- [SENinja](https://github.com/borzacchiello/seninja): symbolic execution engine for BN with a debugger-like API, based on Z3
	- [hexfiles](https://github.com/toolCHAINZ/hexfiles): Intel HEX / Motorola SREC / TI-TXT file loader
	- %[binja-8051](https://github.com/8051Enthusiast/binja-8051): 8051 architecture
	- [binja-avnera](https://github.com/whitequark/binja-avnera): Avnera architecture
	- [binja-m16c](https://github.com/whitequark/binja-m16c): Renesas M16C architecture
	- [cryptoscan](https://github.com/Rami114/cryptoscan): detector of common cryptographic algorithms
	- [Rust string slicer](https://github.com/cxiao/rust_string_slicer): detect Rust strings in code and data
	- [blob extractor](https://github.com/Vector35/blob_extractor/): frontend for [unblob](https://unblob.org/)
	- %[mole](https://github.com/cyber-defence-campus/mole): static backward slicing through MLIL
- %[binsync](https://github.com/binsync/binsync): cross-decompiler (Binary Ninja / Ghidra / IDA) collaboration tool
- [BinDiff](https://github.com/google/bindiff): comparison tool operating on control flow graphs
- %[ReGenny](https://github.com/cursey/regenny): interactive C/C++ structure reconstruction tool and SDK generator
	- %[UE4Genny](https://github.com/cursey/ue4genny): late Unreal Engine 4 and Unreal Engine 5 SDK generator
	- %[Source2Gen](https://github.com/neverlosecc/source2gen): Source 2 SDK generator
- [dnSpyEx](https://github.com/dnSpyEx/dnSpy): interactive CLR decompiler and debugger
- %[hal](https://github.com/emsec/hal): interactive netlist analysis and manipulation tool
- %[Pylingual](https://pylingual.io/): Python bytecode decompiler and patcher

## Debuggers
- [WinDbg](https://learn.microsoft.com/en-us/windows-hardware/drivers/debugger/): Windows kernel and user-mode debugger
- [x64dbg](https://x64dbg.com/): OllyDbg if it was maintained; Windows user-mode x86/x64 debugger
- %[BugChecker](https://github.com/vitoplantamura/BugChecker): SoftICE if it was maintained; preemptive Windows kernel and user-mode debugger; requires PS/2 keyboard and linear framebuffer
- %[libdebug](https://github.com/libdebug/libdebug): GDB if it had an API; Python interface to GDB with a CTF/RE focus 
- [rr](https://rr-project.org/): deterministic record/replay debugger for Linux x86/x64/arm64

## Machine code emulation
- [Unicorn](https://www.unicorn-engine.org/): CPU emulator with fine-grained instrumentation, hooks for memory accesses, Python API, ...
- %[PANDA](https://github.com/panda-re/panda): fork of QEMU with support for whole system record/replay and a plugin system for taint analysis, callgraph tracing, ...
- %[Pydgin](https://github.com/cornell-brg/pydgin): Python DSL for generating instruction set simulators

## API emulation
- %[usersim](https://github.com/microsoft/usersim): implementation of Windows kernel APIs on top of Windows user-mode APIs, for KMDF driver testing, fuzzing, ...
- %[Qiling](https://github.com/qilingframework/qiling): emulator for Windows, Linux, macOS, Android, BSD, UEFI, ... kernel and user-mode APIs based on Unicorn
- %[Limbo](https://github.com/meme/limbo): XNU (Darwin) userspace syscall emulator for Linux

## Dynamic binary analysis and instrumentation
- [ExtremeDumper](https://github.com/wwh1004/ExtremeDumper): online .NET assembly dumper
- %[Triton](https://github.com/JonathanSalwan/Triton): dynamic symbolic execution and LLVM/SMT lifting; "like doing heart surgery with a blender"
- %[Shiva](https://github.com/advanced-microcode-patching/shiva): ELF dynamic linker that performs just-in-time symbol (function, data) interposition; AArch64 only
- %[wsh](https://github.com/endrazine/wcc#wsh--the-witchcraft-shell): loads ET_DYN ELF files and makes API available for scripting
- %[mesos](https://github.com/gamozolabs/mesos): basic block coverage collector for unmodified Windows user-mode binaries; requires IDA
- [NtLua](https://github.com/can1357/NtLua): Windows kernel mode driver with a Lua interpreter, including ntoskrnl exports and x86 intrinsics
- [Detours](https://github.com/microsoft/Detours): Windows user-mode API hooking library
- %[Frida](https://frida.re/): Windows/macOS/Linux/Android API tracing and instrumentation tool
- %[Avatar2](https://github.com/avatartwo/avatar2): toplevel runner for other tools (qemu, angr, openocd, ...), primarily for embedded system analysis, debugging, record/replay, ...
- [CSharpRepl](https://github.com/waf/CSharpRepl): C# REPL

## Static binary analysis and modification
- [readpe](https://github.com/mentebinaria/readpe): PE file reader, like `objdump -p` but works better on malware
- %[wld](https://github.com/endrazine/wcc#wld--the-witchcraft-linker): transforms ELF executables into ELF shared libraries; arch-independent
- %[wcc](https://github.com/endrazine/wcc#wcc--the-witchcraft-compiler): transforms ELF/PE/COFF binaries into ELF relocatable object files (unlinker)
- [superlinker](https://github.com/whitequark/superlinker): combines ET_DYN ELF files with each other and the program interpreter
- %[dll-merger](https://github.com/ytk2128/dll-merger): merges PE libraries into executables
- [ApplyDeltaB](https://github.com/whitequark/ApplyDeltaB): applies forward/reverse delta patches from Windows Update .msu files or WinSxS
- [Detect it Easy](https://github.com/horsicq/Detect-It-Easy): Windows/Linux/macOS/Android/DOS/... executable and archive analysis tool with a focus on malware analysis and protection/compression/... detection
- %[Microwalk](https://github.com/microwalk-project/Microwalk): static/dynamic microarchitectural leakage detection framework
- %[GoReSym](https://github.com/mandiant/GoReSym): Go symbol recovery based on Go compiler internals
- %[Zydis](https://github.com/zyantific/zydis): x86/x64 disassembler with no dependencies or allocations
- %[LIEF](https://github.com/lief-project/LIEF): ELF/PE/MachO parsing and modification library
- [pefile](https://github.com/erocarrera/pefile): PE parsing library for Python
- %[seer](https://github.com/krsh/seer): byte histogram based CPU architecture recognition tool
- [cpu_rec](https://github.com/airbus-seclab/cpu_rec): Markov chain based CPU architecture recognition tool
- %[allyourbase](https://github.com/8051Enthusiast/allyourbase): fast, FFT-based firmware base address detection tool
- %[at51](https://github.com/8051Enthusiast/at51): 8051 firmware reverse engineering tools with a focus on Keil C51
- [bingrep](https://github.com/m4b/rdr): ELF/PE/MachO binary printer, like colorful `objdump` that works well with PE/MachO; not a search tool!
- %[miasm](https://github.com/cea-sec/miasm): disassembly, lifting, symbolic and dynamic execution library
- %[angr](https://angr.io/): disassembly, lifting, and symbolic execution library
- %[IAT patcher](https://hasherezade.github.io/IAT_patcher/): replaces an imported function in a PE file with exports from another file
- [PE-bear](https://github.com/hasherezade/pe-bear): interactive PE file viewer and editor
- [FLOSS](https://github.com/mandiant/flare-floss): `strings` if it was good and not based on libbfd; searches for C/Rust/Go strings in read-only data sections, stack-allocated strings, strings in vector registers; PE-only
- [revng](https://github.com/revng/revng): tool to convert machine code fragments into equivalent compilable C code; made by crackheads??
- %[angrop](https://github.com/angr/angrop): automated ROP gadget search and chain construction
- %[Ropper](https://github.com/sashs/Ropper): ROP gadget search and display tool
- [apktool](https://apktool.org/): Android application decompiler/recompiler; emits/consumes smali
- [jadx](https://github.com/skylot/jadx): Android application decompiler; emits Java
- [de4js](https://lelinhtinh.github.io/de4js/): JavaScript deobfuscator and unpacker
- %[unpac.me](https://www.unpac.me/): automated malware unpacking

## Filesystem and archive manipulation
- [binwalk](https://github.com/ReFirmLabs/binwalk): firmware/filesystem/archive/executable/... analysis tool with an emphasis on semi-unstructured vendor blobs
- [unblob](https://github.com/onekey-sec/unblob): filesystem/archive analysis tool
- %[UEFITool](https://github.com/LongSoft/UEFITool): UEFI firmware viewer and editor
- [fiedka](https://fiedka.app/): SoC firmware viewer (UEFI FFS, coreboot CBFS, AMD PSP/ASP)
- [UBI Reader](https://github.com/onekey-sec/ubi_reader): Python library for Linux UBI/UBIFS extraction and analysis
- %[lessmsi](https://github.com/activescott/lessmsi): MSI interactive viewer and batch extractor
- %[innoextract](https://github.com/dscharrer/innoextract): Inno Setup installer extractor
- [jefferson](https://github.com/onekey-sec/jefferson/): Python JFFS2 extractor
- %[pyinstxtractor-ng](https://github.com/pyinstxtractor/pyinstxtractor-ng): PyInstaller extractor (has a [web version](https://pyinstxtractor-web.netlify.app/))
- %[diffoscope](https://diffoscope.org/): recursive diff tool for archives (developed for debugging reproducible builds)

## Data format manipulation
- [delsum](https://github.com/8051Enthusiast/delsum): checksum (modular, Fletcher, and CRC) reverse engineering tools
- [biodiff](https://github.com/8051Enthusiast/biodiff): alignment based file comparison tool
- %[yabo](https://github.com/8051Enthusiast/yabo): functional heapless binary parser language
- %[bgrep](https://github.com/tmbinc/bgrep): search binary files for data with mask specified as hex
- %[MultiRipper](https://github.com/matteobaccan/MultiRipper): game data archive extraction tool
- %[vgmstream](https://github.com/vgmstream/vgmstream/): game music playback tool
- %[binxelview](https://github.com/bbbradsmith/binxelview): tool for extracting pixel arrays from binary files
- %[polyfile](https://github.com/trailofbits/polyfile): libmagic/`file` replacement tailored for polyglot and recursive files

## Signal analysis
- [Wireshark](https://www.wireshark.org/): network protocol analyzer
- %[Modlishka](https://github.com/drk1wi/Modlishka): HTTP reverse proxy capable of intercepting TLS
- [Universal Radio Hacker](https://github.com/jopohl/urh): RF demodulation and protocol analysis tool
- %[Signalspec](https://github.com/signalspec/signalspec): composable digital/analog/radio signal analysis framework
- %[bettercap](https://github.com/bettercap/bettercap): WiFi/Ethernet/BLE/CAN recoinassance and attack tool

## Event tracing
- %[DecodeWheaRecord](https://github.com/ralish/DecodeWheaRecord): _Windows Hardware Error Architecture (WHEA)_ record decoder (PCIe errors, firmware errors, machine check errors, ...)
- %[ply](https://github.com/iovisor/ply): Linux kprobe/tracepoint tracer with a custom language and compiler (not dependent on LLVM/BCC)
- [System Informer](https://systeminformer.com/): Windows Task Manager if it was good; displays modules (+ a PE viewer), threads (+ stack trace symbolication), security tokens, environment, memory regions (+ hex dump), handles, named pipes, win32k windows, services and drivers, NT objects, NT memory pools, UEFI/SMBIOS tables, ...
- [API Monitor](http://www.rohitab.com/apimonitor): interactive Windows API tracing tool
- %[UIforETW](https://github.com/google/UIforETW): captures ETW logs without making you remember `tracelog` incantations

## Hardware instrumentation
- %[usbrply](https://github.com/JohnDMcMaster/usbrply): converter from USB `.pcap` packet captures to Python libusb calls
- %[hgdb](https://github.com/Kuree/hgdb): waveform trace based reversible debugger

## Silicon reverse engineering
- %[zorrom](https://github.com/JohnDMcMaster/zorrom): physical <> logical mask ROM layout converter
- %[rompar](https://github.com/AdamLaurie/rompar): mask ROM optical extraction tool
- %[maskromtool](https://github.com/travisgoodspeed/maskromtool): mask ROM optical extraction tool and layout converter

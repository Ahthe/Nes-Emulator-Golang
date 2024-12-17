# 🎮 NES Emulator in Golang  

Dive into the nostalgia of classic gaming with this NES emulator built entirely in Go! ⚡ Experience the charm of 8-bit gaming by running NES ROMs on this emulator.  

---

## 🚀 How to Run  

1. **Install Dependencies**:  
   ```bash  
   go mod tidy  
   ```  

2. **Run the Emulator**:  
   ```bash  
   go run main.go  
   ```  

3. **Start Gaming**:  
   Drag and drop any compatible NES ROM (with a supported mapper) into the GUI, and you're good to go! 🎉  

---

## 🛠️ Future Plans  

- 🎵 **Enhance Audio**: Expand APU functionality beyond the basic pulse oscillator.  
- 📦 **Add More Mappers**: Increase compatibility with more NES ROMs.  
- 🖥️ **Dynamic Screen Upscaling**: Improve display resolution for modern screens.  

---

## 🧩 Architecture Overview  

### 🛡️ **Core Components**  
- **64KB RAM**: The NES system views 2KB of physical RAM as a mirrored 8KB block.  
- **6502 CPU**: Features registers (A, X, Y), a stack pointer, a program counter (PC), and a status register.  
  - Instructions may vary in size and cycles.  
- **olc2c02 PPU (Picture Processing Unit)**:  
  - 8KB Pattern Memory: Stores sprite and background graphics.  
  - 2KB Nametable: Holds layout data for the background.  
  - Color Palettes: Manage graphical color schemes.  

### 🗂️ **Memory Layout**  
- **Programmable ROM (P-ROM)**: Contains both program and graphical data for the PPU.  
- **Mapper**: Dynamically switches ROM banks and recognizes writable memory regions.  

### 🎨 **Graphics Rendering**  
- Understand patterns, nametables, and palettes to see how tiles are rendered on the screen:  
  - [PPU Memory Map](https://www.nesdev.org/wiki/PPU_memory_map)  
  - [Pattern Tables](https://www.nesdev.org/wiki/PPU_pattern_tables): Define sprite shapes in CHR ROM/RAM.  
  - [Nametable Layout](https://www.nesdev.org/wiki/PPU_nametables): Details the complex display system and scrolling.  

### 🕹️ **Input Controls**  
- The NES uses **8 buttons** mapped to a single byte, with memory-mapped controls for reading and writing:  
  - Parallel write, serial read.  
  - Supports 2 controllers.  

### 🖼️ **Sprites**  
- Stored in **Object Attribute Memory (OAM)**.  
- Each sprite requires 4 bytes (x, y, tile ID, attributes).  
- Only **64 sprites** in total, with a max of 8 sprites per scanline.  

### 🎵 **Audio Processing Unit (APU)**  
- Integrated into the CPU, the APU acts like a "fire-and-forget" sound system for music and effects.  

---

## 📝 Developer Notes  

- ✅ Ensure the CPU operates independently. Test using updated versions of **nestest**.  
- 🖌️ PPU is complex—build it step by step. Start with loading and displaying the pattern table.  
- 🔧 Components need careful synchronization (e.g., CPU & PPU with vertical blank status).  

---

## 📚 Resources  

- **Video Tutorials**: [javidx9 NES Emulator Series](https://www.youtube.com/watch?v=8XmxKPJDGU0&list=PLrOv9FMX8xJHqMvSGB_9G9nZZ_4IgteYf&index=3)  
- **Datasheets**:  
  - [6502 CPU](https://www.princeton.edu/~mae412/HANDOUTS/Datasheets/6502.pdf)  
  - [6502 Guide](https://www.nesdev.org/obelisk-6502-guide/)  
  - [Addressing Modes](https://www.nesdev.org/wiki/CPU_addressing_modes)  
- **Testing**:  
  - [Emulator Tests](https://www.nesdev.org/wiki/Emulator_tests)  
  - [Nestest Log](https://github.com/nwidger/nintengo/blob/master/m65go2/test-roms/nestest/nestest.log)  
- **NES Architecture**: [Diagram & Explanation](https://taywee.github.io/NerdyNights/nerdynights/nesarchitecture.html)  


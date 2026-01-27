# Operating Systems Lecture 6: Computer Boot Process

## Introduction
What happens when you turn on your computer? This lecture explains the complete boot process from pressing the power button to seeing your GUI.

---

## The 5 Steps of Computer Boot Process

### Step 1: Power On
- User presses the power button
- Electrical supply goes to the **Power Supply Unit (PSU)**
- PSU is a component that distributes power to all hardware components:
  - Motherboard
  - Hard disk/SSD
  - GPU
  - Other peripherals

---

### Step 2: CPU Loads BIOS/UEFI

#### What is BIOS?
- **BIOS** = Basic Input Output System
- Small program stored in a non-volatile chip (ROM) on the motherboard
- Traditionally used in older systems

#### What is UEFI?
- **UEFI** = Unified Extensible Firmware Interface
- Advanced version of BIOS used in modern systems
- Additional capabilities:
  - Better management of computers connected on LAN
  - More advanced features (e.g., Intel UEFI)

#### Process
1. CPU receives power
2. CPU is initialized
3. CPU goes to BIOS/UEFI chip to load the boot program

---

### Step 3: BIOS/UEFI Initialization

#### CMOS Battery and Settings
- **CMOS** = Complementary Metal Oxide Semiconductor
- Small battery in the CPU that maintains:
  - BIOS settings
  - System clock
  - Configuration data
- Keeps running even when the computer is off
- **Important**: If CMOS battery is removed, the system won't boot properly (will beep)

#### Power-On Self-Test (POST)
BIOS runs hardware tests to ensure all components are working:
- **RAM test**: Checks if RAM is available and functioning
- **Hardware initialization**: Verifies all essential hardware is present
- **Error handling**: Shows error messages if critical hardware is missing

#### What POST Tests
- Memory availability
- Storage devices
- Essential hardware components
- System integrity

---

### Step 4: Handing Over to Boot Device

#### What is a Boot Device?
A boot device is the storage location where OS boot instructions are stored (also called **boot loader**).

#### Types of Boot Devices
- Hard Disk Drive (HDD)
- Solid State Drive (SSD)
- CD/DVD Drive
- USB Drive (used when installing OS)

#### Boot Loader Locations

##### 1. MBR (Master Boot Record)
- **Used by**: BIOS (older systems)
- **Location**: 0th index of the disk
- **Structure**: Special area at the beginning of the disk
- Still in use but mostly in legacy systems

##### 2. EFI (Extensible Firmware Interface)
- **Used by**: UEFI (modern systems)
- **Location**: Separate partition on the disk (EFI partition)
- **Structure**: Dedicated partition containing boot loader files
- More flexible than MBR

#### Process
1. BIOS/UEFI confirms all hardware is initialized
2. Searches for boot loader in MBR or EFI partition
3. Locates the boot loader program
4. Hands over control to the boot loader

---

### Step 5: Boot Loader Loads the Full OS

#### What is a Boot Loader?
A program that initializes and starts the actual operating system.

#### Boot Loader Programs by OS

| Operating System | Boot Loader Program |
|-----------------|---------------------|
| Windows | bootmgr.exe |
| macOS | boot.efi |
| Linux | GRUB (Grand Unified Bootloader) |

#### Boot Loader Responsibilities
- Initialize the operating system kernel
- Load GUI components
- Start system services and daemons
- Initialize device drivers
- Mount file systems
- Start essential programs and processes

#### Why Different Boot Loaders?
- Each OS initializes differently
- Every manufacturer writes their own boot program
- OS-specific requirements and architecture

---

## Summary Flow Diagram

```
Power Button Pressed
         ↓
[Step 1] Power Supply Unit Distributes Power
         ↓
[Step 2] CPU Loads BIOS/UEFI from ROM
         ↓
[Step 3] BIOS/UEFI Performs:
         - Load settings from CMOS
         - Run POST (Power-On Self-Test)
         - Initialize hardware
         ↓
[Step 4] BIOS/UEFI Finds Boot Loader
         - In MBR (BIOS systems)
         - In EFI Partition (UEFI systems)
         ↓
[Step 5] Boot Loader Starts Operating System
         - Loads OS kernel
         - Initializes GUI
         - Starts system services
         ↓
Operating System Fully Loaded
```

---

## Key Terminology

### BIOS (Basic Input Output System)
- Firmware interface for PCs
- Stored in ROM chip on motherboard
- Initializes hardware during boot
- Legacy system, being replaced by UEFI

### UEFI (Unified Extensible Firmware Interface)
- Modern replacement for BIOS
- More features and capabilities
- Better security
- Supports larger disk sizes

### CMOS Battery
- Small battery maintaining BIOS settings
- Keeps system clock running
- Essential for boot process
- Typically lasts 5-10 years

### POST (Power-On Self-Test)
- Diagnostic testing sequence
- Checks hardware functionality
- Runs before OS loads
- Produces beep codes for errors

### MBR (Master Boot Record)
- Boot sector at the beginning of a disk
- Contains boot loader code
- Limited to 2TB disk size
- Used by BIOS systems

### EFI Partition
- Dedicated partition for boot files
- Used by UEFI systems
- More flexible than MBR
- Supports larger disks

### Boot Loader
- Program that loads the OS
- Examples: GRUB, bootmgr.exe, boot.efi
- OS-specific implementation
- Bridge between firmware and OS

---

## Important Notes

1. **Modern systems boot faster** due to:
   - SSD technology
   - Advanced processors (e.g., M1 chip in Mac)
   - UEFI optimizations
   - Faster POST procedures

2. **Steps 1-4** are handled by BIOS/UEFI (hardware/firmware level)

3. **Step 5 onwards** is handled by the boot loader and OS (software level)

4. **Each OS has its own boot process** after the boot loader takes control

5. **Without CMOS battery**, the system may not boot properly or will lose settings

---

## Homework Suggestions

To deepen your understanding, research more about:
- UEFI detailed specifications
- MBR vs GPT partition schemes
- Different boot loader implementations
- Secure Boot in UEFI
- Boot process troubleshooting

---

## Questions to Review

1. What happens immediately after pressing the power button?
2. What is the difference between BIOS and UEFI?
3. What is the role of CMOS battery?
4. What does POST check for?
5. Where is the boot loader stored?
6. What is the difference between MBR and EFI?
7. Name boot loaders for Windows, Mac, and Linux
8. At which step does the OS actually start loading?

---

*Notes from OS Lecture 6 by Lakshay*
*Topic: What Happens When You Turn On Your Computer*

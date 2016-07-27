# AutoWBAdjustTool

AutoWBAdjustTool is a tool for auto white balance adjustment of some TVs. For now, it supports Letv, Haier and CAN. 

## Requirements

### Software

* OS
	* Windows (XP, Vista or 7).
* Development Tools
	* Visual Basic 6.0
	* Visual C++ 6.0
* Drivers
	* FTDI USB Serial Converter Drivers (Google it to download this driver. I am using CDM 2.02.04.exe).
	* CA-SDK for CA-310/CA-210/100Plus (You can find the SDK in CD/DVD in KONICA MINOLTA products or its offical website).
	* Drivers for Chroma VPG products (To install **VPGMaster** provided by Chroma so that you can get drivers for Chroma VPG products).
	* I2CBridge.0.1.4.exe (Install it so that you can communicate with Hx6310 by I2C).

### Hardware
* A PC with softwares introduced above. 
* A TV which needs to adjust white balance.
* CA-310 or CA-210 with a USB B Type cable.
* Chroma VPG products (such as, 22294, 22294-A, 2401, 2402) with a USB B Type cable and a signal cable (for example, a HDMI cable).
* A debug tool which connects PC and TV.
* A network cable (Some TVs may use a network cable instead of a debug tool to connect to PC).
* A barcode scanner.

![Devices](https://github.com/heray1990/AutoWBAdjustTool/raw/master/Images/Devices.png)

## Building

### ColorT.dll

`ColorT.dll` contains the main algorithm of AutoWBAdjustTool. Use the workspace file `ColorT_dll/ColorT.dsw` to build it on Windows. Visual C++ 6.0 is recommended.

After building, please copy the `ColorT.dll` file from `ColorT_dll/Release` to `main_VB` so that we can use it for building AutoWBAdjustTool.

### AutoWBAdjustTool

Use the project file `main_VB/AutoWBAdjustTool.vbp` to build AutoWBAdjustTool. Visual Basic 6.0 is recommended.

After building, `main_VB/AutoAdjustColorTemp.exe` will be generated. Then we can install it into other PC.

## Installing

Create a new folder whose name is `AutoWBAdjustTool` in a target computer. Copy the following files to `AutoWBAdjustTool` folder.

### Dynamic Link Library (\*.dll)

* `ColorT.dll`
* `lptio.dll`
* `CyUSB.dll`
* `VPGCtrl.dll`
* `VPGParser.dll`

`CyUSB.dll`, `VPGCtrl.dll` and `VPGParser.dll` are Chroma VPG's SDK for VB.NET. According to [MSDN's explanation](https://msdn.microsoft.com/en-us/library/h627s4zy(v=vs.80).aspx), we need to run a command-line tool called the [Assembly Registration Tool (Regasm.exe)](https://msdn.microsoft.com/en-us/library/tzat5yw6(v=vs.80).aspx) to register or unregister `CyUSB.dll`, `VPGCtrl.dll` and `VPGParser.dll` for use with VB 6.0.

In `AutoWBAdjustTool` folder, enter the following command to register `CyUSB.dll`, `VPGCtrl.dll` and `VPGParser.dll`.

    RegAsm.exe CyUSB.dll /codebase /tlb
    RegAsm.exe VPGCtrl.dll /codebase /tlb
    RegAsm.exe VPGParser.dll /codebase /tlb

If successful, `CyUSB.tlb`, `VPGCtrl.tlb` and `VPGParser.tlb` will be generated.

### Config files

* XML files
	* `main_VB/wizard.xml`: Contains project lists. 
	* `main_VB/project_name/config.xml`: project_name must be same as names in `wizard.xml` file. 
	* `main_VB/project_name/CONFIG.INI`

### Resource files

* `Resources/AutoWB.bmp`
* `Resources/CANTV.bmp`
* `Resources/Haier.bmp`
* `Resources/Letv.bmp`
* `Resources/Picture1.bmp`
* `Resources/tv_icon.ico`

### Database

* `Data.mdb`: One table for one project or one model.
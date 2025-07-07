# CutterMachineProject

A C# Windows Forms application developed for industrial cutting machine control. This project interprets CAD files to generate G-Code and automatically controls machines using Dynomotion motion control systems.

## 🎯 Features

### CAD File Support
- **ISO/CUT Files**: Reading and interpreting Gerber format files
- **PLT Files**: HP-GL/2 plotter file format support
- Automatic part detection and separation
- Multi-part processing support

### Motion Control
- **4-Axis Control**: X, Y, Z and A (rotary) axes
- **Dynomotion KMotion** card integration
- Precise positioning and speed control
- Servo motor driver support

### Cutting Features
- **Smart Knife Angle Calculation**: Automatic tangential knife control
- **V-Notch and I-Notch Detection**: Optimization for special cutting geometries
- **Z-Axis Automation**: Automatic cutting depth based on material thickness
- **Vacuum System**: Multi-zone vacuum control

### Safety System
- **Emergency Stop**: Hardware-based safety system
- **Soft Limits**: Software-based movement boundaries
- **Home Position**: Automatic referencing system
- **Alarm Management**: Comprehensive alarm system

## 🛠️ Technical Specifications

### Requirements
- **.NET Framework 4.7.2**
- **Windows 10/11**
- **Dynomotion KMotion/KFlop** motion control card
- **Visual Studio 2019+** (for development)

### Hardware Support
- **Motion Control**: Dynomotion KMotion_dotNet library
- **I/O Control**: Digital input/output management
- **Servo Drives**: Industrial servo motor driver support
- **Sensors**: Home sensors, limit switches, emergency stop

### Supported File Formats
```
├── ISO Files (.iso)
├── CUT Files (.cut)
└── PLT Files (.plt)
```

## 📦 Installation

### Prerequisites
1. Dynomotion KMotion Software Suite installation
2. .NET Framework 4.7.2
3. Visual Studio 2019 or later

### Installation Steps
```bash
# 1. Clone the repository
git clone https://github.com/[username]/CutterMachineProject.git

# 2. Navigate to project directory
cd CutterMachineProject

# 3. Install NuGet packages
nuget restore

# 4. Build the project
msbuild CutterMachineProject.sln
```

### Configuration
1. Configure machine parameters in `App.config` file
2. Check Dynomotion C program paths
3. Set motion parameters according to machine specifications

## 🚀 Usage

### Basic Workflow
1. **System Startup**: Establish machine connection
2. **Homing**: Move all axes to home position
3. **File Loading**: Select and load CAD file
4. **Preview**: Check cutting path and parts
5. **Start Cutting**: Begin operation and monitor

### Main Screen Controls
- **Jog Controls**: Manual axis movement
- **Feed Rate Override**: Speed control (1-200%)
- **Emergency Stop**: Emergency stop button
- **Status Display**: Real-time status indication

### File Processing
```csharp
// CAD file loading example
var interpreter = new ISOFileInterpreter();
interpreter.ReadTheAllFileContent("file.iso");

// G-Code generation happens automatically
foreach(var piece in machine.Pieces)
{
    // Cutting operation for each part
    DynomotionSystem.Instance.Interpret(piece.GeneratedGCode);
}
```

## ⚙️ Configuration

### Motion Parameters
```xml
<CutterMachineProject.Properties.MotionParams>
    <setting name="VelocityInchSecondsX" value="1000" />
    <setting name="AccelInchSeconds2X" value="50" />
    <setting name="CountsPerInchX" value="4724.41" />
</CutterMachineProject.Properties.MotionParams>
```

### Homing Parameters
```xml
<CutterMachineProject.Properties.Homing>
    <setting name="HomeDirectionX" value="-1" />
    <setting name="ApproachVelX" value="20000" />
    <setting name="HomeVelX" value="2000" />
</CutterMachineProject.Properties.Homing>
```

## 🔧 Development

### Project Structure
```
CutterMachineProject/
├── App.cs                 # Main application entry point
├── Machine/               # Machine control classes
│   ├── DynomotionSystem.cs # Motion control main class
│   ├── Machine.cs          # Machine state management
│   └── Hardware/           # Hardware abstraction
├── Import/                # File interpreters
│   ├── ISOFileInterpreter.cs
│   ├── PLTFileInterpreter.cs
│   └── CUTFileInterpreter.cs
├── Gui/                   # User interface
└── GCode/                 # G-Code processing
    └── Piece.cs           # Piece class
```

### Adding New File Format
```csharp
// Inherit from CadFileInterpreter class
public class NewFormatInterpreter : CadFileInterpreter
{
    public override void ParseTheInstructions()
    {
        // File parsing logic
    }
    
    public override void DetectThePieces()
    {
        // Part detection logic
    }
}
```

## 🚨 Safety

### Important Safety Notes
- **Emergency Stop**: Must always be accessible
- **Soft Limits**: Must be properly configured
- **Home Sensors**: Should be tested regularly
- **Servo Ready**: All drives must be in RUN mode

### Alarm System
```csharp
// Alarm example
public static readonly Alarm alarmPosSoftLimitX = 
    new Alarm(1, "Soft Limit Positive X Axis", Alarm.AlarmType.ERROR);
```

## 📊 Statistics and Monitoring

- **Real-time Position**: Instant position of all axes
- **Feed Rate Monitoring**: Speed control and override
- **Execution Progress**: Operation progress status
- **I/O Status**: Digital input/output states


## 🔄 Version History

### v1.0.0
- Initial stable release
- ISO/CUT/PLT file support
- 4-axis motion control
- Tangential knife control
- Vacuum system integration

---

**Note**: This project is designed for industrial use. Please consider safety measures when using.

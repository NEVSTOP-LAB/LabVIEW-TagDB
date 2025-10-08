# NEVSTOP TagDB Library

[English](./README(en).md) | [中文](./README.md)

NEVSTOP TagDB is an advanced data management library designed specifically for the LabVIEW environment, providing efficient reading, writing, storage, and sharing of configuration and Tag data. Through optimized data structures and caching mechanisms, it offers reliable data persistence and real-time data access solutions for LabVIEW applications.

## Directory Structure

```
├── .github/          # GitHub workflow configurations
├── Benchmark/        # Performance test related files
├── Documentation/    # Documentation and icon resources
├── src/              # Source code directory
│   ├── Example/      # Example programs
│   ├── Probes/       # Custom debugging probes
│   └── TagDB/        # Core library files
│       ├── API/      # Public interface functions
│       ├── Add-ons/  # Additional features
│       └── Typedef/  # Type definitions
├── LabVIEW-TagDB.lvproj  # Main project file
└── LabVIEW-TagDB.vipb    # VIPackage build file
```

## Core Features

### 1. Flexible Data Storage
- Supports persistent storage of configuration data and Tag data
- Automatically supports conversion and storage of all LabVIEW data types through VIM (VI Macro)
- Specially optimized for Reference type data to ensure efficient storage and retrieval

### 2. Multi-thread Safety
- Provides a comprehensive data sharing mechanism in multi-threaded environments
- Built-in thread safety protection to avoid concurrent access conflicts
- Supports data access and synchronization across VIs and tasks

### 3. High Performance Design
- Implements efficient caching mechanism for fast data access
- Optimized data structures to reduce memory usage and improve retrieval efficiency
- Supports name-based DBRef acquisition method, similar to LabVIEW Named Queue, simplifying programming patterns

### 4. Configuration Management
- Complete configuration file import/export functionality
- Supports saving and restoring system status information
- Provides configuration locking feature to prevent accidental modifications

### 5. Debugging Support
- Offers three custom Probes for convenient runtime debugging and monitoring
- Includes TagDB Probe, TagDB Table Probe, and TagDB Monitor Probe

## API Reference

### Basic Operation Functions

| Function Name | Description |
|--------------|-------------|
| TagDB-Obtain.vi | Obtains TagDB Refnum, creates or opens an existing database |
| TagDB-Release.vi | Releases TagDB Refnum, closes the database |
| TagDB-IsValid.vi | Checks if TagDB Refnum is valid |

### Data Read/Write Functions

| Function Name | Description |
|--------------|-------------|
| TagDB-Write.vim | Writes/updates the value of a single Tag |
| TagDB-Read.vim | Reads the value of a single Tag |
| TagDB-Read By RegExp.vim | Batch reads Tags using regular expressions |
| TagDB-Delete.vi | Deletes a Tag |

### Configuration Management Functions

| Function Name | Description |
|--------------|-------------|
| TagDB-Load.vi | Loads TagDB configuration from file |
| TagDB-Save.vi | Saves TagDB configuration to file |
| TagDB-Set Lock.vi | Locks/unlocks TagDB, disallows/allows adding new Tags |

### Utility Functions

| Function Name | Description |
|--------------|-------------|
| TagDB-Status.vi | Gets current status information of TagDB |
| TagDB-List.vi | Lists all Tag names in the database |
| TagDB_Find Names.vi | Finds Tag names that meet the criteria |
| TagDB-Timestamp.vi | Gets timestamp of TagDB operations |
| TagDB-UpdateUI.vi | Updates UI controls associated with Tags |
| TagDB-Change Detector.vi | Detects changes in Tag values |

## Best Practices

### Data Management
- **Data sharing in multi-threaded environments**: Use TagDB as a data sharing center between multi-threaded applications, avoiding the use of global variables
- **Configuration information storage**: Store system configuration information in TagDB for easy import/export and version control
- **Temporary data caching**: Utilize TagDB's caching functionality to achieve asynchronous updates and fast access to data points
- **Control reference management**: Store LabVIEW front panel control References for convenient dynamic UI manipulation

### Performance Optimization
- For frequently accessed data, consider using TagDB's caching mechanism
- When performing bulk data operations, properly use batch operation functions to improve efficiency
- Appropriately use the locking feature to prevent data modification during critical operations

### Debugging Techniques
- Use the three built-in Probe tools to monitor the status and data changes of TagDB during runtime
- Regularly check the database status using TagDB-Status.vi to detect issues in a timely manner
- Use TagDB-Change Detector.vi to monitor changes in specific Tags, facilitating debugging of complex interaction logic

## Example Programs

The library includes multiple example programs demonstrating usage in different scenarios:

- **TagDB Example.vi**: Basic function demonstration
- **TagDB Application Example**: Practical application demonstration with a complete model configuration system
- **TagDB For Control Reference.vi**: Example of handling Reference type data for UI controls
- **TagDB Multi-Thread Example**: Usage example in multi-threaded environments
- **TagDB Using regexp Example.vi**: Regular expression query example

## Installation Instructions

Install the VIP package using VIPM (VI Package Manager)

## System Requirements

- LabVIEW 2017 or later
- VIPM 2017 or later is recommended for installation

## License

This project is licensed under the MIT License, see the [LICENSE](LICENSE) file for details.

## Contribution Guidelines

Contributions in the form of issue reports and improvement suggestions are welcome. To contribute code, please follow these steps:
1. Fork this repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Submit a Pull Request
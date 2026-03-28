# NEVSTOP TagDB Library

[English](./README(en).md) | [中文](./README.md)

NEVSTOP TagDB is an advanced data management library for LabVIEW, providing efficient read/write, storage, and sharing of configuration and Tag data. With optimized data structures and a built-in caching layer, it delivers reliable data persistence and real-time access for LabVIEW applications.

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
- Supports read/write and automatic type conversion for all LabVIEW data types via VIM (VI Macro)
- Specially optimized for Reference type data to ensure efficient storage and retrieval

### 2. Multi-thread Safety
- Provides a comprehensive data sharing mechanism in multi-threaded environments
- Built-in thread safety protection to avoid concurrent access conflicts
- Supports data access and synchronization across VIs and tasks

### 3. High Performance Design
- Implements an efficient caching mechanism for fast data access
- Optimized data structures to reduce memory usage and improve retrieval efficiency
- Supports name-based DBRef lookup (similar to LabVIEW Named Queue), simplifying cross-VI data access patterns

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
| TagDB-Write Data Recursive.vim | Recursively writes/updates data structures to Tags |
| TagDB-Write Data Elements.vim | For Cluster data, writes each element to its corresponding Tag by element name |
| TagDB-Read.vim | Reads the value of a single Tag |
| TagDB-Read Data By Element Names.vim | For Cluster data, reads each element from its corresponding Tag by element name |
| TagDB-Read By RegExp.vim | Batch reads Tags using regular expressions |
| TagDB-Delete.vi | Deletes a Tag |
| TagDB-Delete Single.vi | Deletes a single Tag by name |
| TagDB-Delete Multiple.vi | Batch deletes multiple Tags |

### Configuration Management Functions

| Function Name | Description |
|--------------|-------------|
| TagDB-Load.vi | Loads TagDB configuration from file |
| TagDB-Save.vi | Saves TagDB configuration to file |
| TagDB-Set Lock.vi | Locks/unlocks TagDB to restrict or allow adding new Tags |

### Utility Functions

| Function Name | Description |
|--------------|-------------|
| TagDB-Status.vi | Gets current status information of TagDB |
| TagDB-List.vi | Lists all Tag names in the database |
| TagDB_Find Names.vi | Finds Tag names that meet the criteria |
| TagDB-Timestamp.vi | Gets timestamp of TagDB operations |
| TagDB-UpdateUI.vi | Updates UI controls associated with Tags |
| TagDB-Change Detector.vi | Detects changes in Tag values |
| TagDB-Truncate.vi | Clears all Tag data in the TagDB database |

## Best Practices

### Data Management
- **Multi-threaded data sharing**: Use TagDB as a shared data hub across threads, replacing global variables
- **Configuration storage**: Store system configuration in TagDB for easy import/export and version management
- **Temporary data caching**: Leverage TagDB's caching to enable asynchronous updates and fast access to data points
- **Control reference management**: Store front-panel control References for dynamic UI manipulation

### Performance Optimization
- For frequently accessed data, make use of TagDB's caching mechanism
- For bulk data operations, prefer batch operation functions to improve efficiency
- Use the locking feature during critical operations to prevent unintended data modification

### Debugging Techniques
- Use the three built-in Probe tools to monitor TagDB state and data changes at runtime
- Periodically check database status with TagDB-Status.vi to catch issues early
- Use TagDB-Change Detector.vi to watch specific Tags for value changes, aiding in debugging complex interaction logic

## Example Programs

The library includes multiple example programs demonstrating usage in different scenarios:

- **TagDB Example.vi**: Basic function demonstration
- **TagDB Application Example**: Practical application demonstration with a complete model configuration system
- **TagDB For Control Reference.vi**: Example of handling Reference type data for UI controls
- **TagDB Multi-Thread Example**: Usage example in multi-threaded environments
- **TagDB Read Data Example.vi**: Comprehensive read example covering single read, element-name read (for Cluster data), and regular expression read
- **TagDB Write Data Example.vi**: Comprehensive write example covering single write, element-name write (for Cluster data), and recursive data structure write
- **TagDB Using regexp Example.vi**: Regular expression query example
- **TagDB Refresh UI Value.vi**: UI value refresh example, showing how to update UI control values in real-time

## Installation Instructions

Install the VIP package using VIPM (VI Package Manager).

## System Requirements

- LabVIEW 2017 or later
- VIPM 2017 or later is recommended for installation

## License

This project is licensed under the Apache-2.0 license, see the [LICENSE](LICENSE) file for details.

## Contribution Guidelines

Contributions in the form of issue reports and improvement suggestions are welcome. To contribute code, please follow these steps:
1. Fork this repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Submit a Pull Request
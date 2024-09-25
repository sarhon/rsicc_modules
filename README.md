# RSICC Modules

This repository contains modulefiles for managing multiple versions of MCNP and SCALE using the Environment Modules system. These modulefiles simplify the setup and switching between different versions of these tools, which are commonly used in nuclear engineering and radiation transport simulations.

## Table of Contents

- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
  - [Loading Modules](#loading-modules)
  - [Unloading Modules](#unloading-modules)
  - [Switching Between Versions](#switching-between-versions)
  - [Accessing Documentation](#accessing-documentation)
- [Additional Notes](#additional-notes)
- [Support](#support)

## Overview

The modulefiles in this repository are designed to:

- Set up environment variables for different versions of MCNP and SCALE.
- Allow easy loading and unloading of these tools using the `module` command.
- Enable users to switch between different versions without conflicts.
- Provide a `doc` command to access documentation for each tool.

## Prerequisites

- **Environment Modules System**: You need to have the Environment Modules package installed on your system. This allows you to dynamically modify your user environment via modulefiles.
- **MCNP and SCALE Installations**: Ensure you have valid installations of MCNP and SCALE. You must have proper licenses to use these tools.
- **Bash Shell**: The instructions assume you are using the Bash shell.

### Installing Environment Modules

On Debian-based systems (e.g., Ubuntu), you can install the Environment Modules system using `apt`:

```bash
sudo apt update
sudo apt install environment-modules
```

## Installation

### 1. Clone or Download the Repository

Place the `rsicc_modules` directory in a location of your choice. For example, in your home directory:

```bash
cd ~
git clone https://github.com/sarhon/rsicc_modules.git
```

### 2. Update Your `~/.bashrc` File

Add the following lines to your `~/.bashrc` file to set up the modules system and include the `rsicc_modules` directory:

```bash
# Initialize the Environment Modules system
source /etc/profile.d/modules.sh

# Use the rsicc_modules directory for modulefiles
module use ~/rsicc_modules

# Remove stack size limits (optional, recommended for MCNP/SCALE)
ulimit -s unlimited
```

- **Note**: Replace `~/rsicc_modules` with the actual path to the `rsicc_modules` directory if it's located elsewhere.

Reload your `~/.bashrc` to apply the changes:

```bash
source ~/.bashrc
```

### 3. Create the Configuration File

Create a configuration file `~/.rsicc_roots.conf` to specify the installation directories for MCNP and SCALE.

```bash
nano ~/.rsicc_roots.conf
```

#### Template `~/.rsicc_roots.conf`

```tcl
# ~/.rsicc_roots.conf

# MCNP Root Paths
set MCNP_ROOT_620 "/path/to/your/MCNP/MCNP620"
# set MCNP_ROOT_630 "/path/to/your/MCNP/MCNP630"

# SCALE Root Paths
set SCALE_ROOT_632 "/path/to/your/SCALE/SCALE-632"
set SCALE_ROOT_631 "/path/to/your/SCALE/SCALE-631"
set SCALE_ROOT_624 "/path/to/your/SCALE/SCALE-624"
```

- **Instructions**:
  - Replace `"/path/to/your/..."` with the actual installation directories of your MCNP and SCALE versions.
  - Uncomment and set additional versions as needed.
  - This file **must be created by you**; it is not included in the repository.

### 4. Verify the Configuration

Ensure that your `~/.rsicc_roots.conf` contains the correct paths and that the modulefiles can access it.

## Configuration

### Environment Modules Initialization

Ensure that the Environment Modules system is initialized by adding the following line to your `~/.bashrc` (already included in the installation steps):

```bash
source /etc/profile.d/modules.sh
```

### Modulefile Path

Add the `rsicc_modules` directory to the module path by including in your `~/.bashrc`:

```bash
module use ~/rsicc_modules
```

Replace `~/rsicc_modules` with the correct path if different.

### Stack Size Limit

For optimal performance and to prevent stack overflows when running MCNP or SCALE, it's recommended to remove stack size limits:

```bash
ulimit -s unlimited
```

## Usage

### Loading Modules

To load a specific version of MCNP or SCALE, use the `module load` command followed by the module name and version.

#### MCNP Example

```bash
module load mcnp/6.2.0
```

#### SCALE Example

```bash
module load scale/6.3.2
```

### Unloading Modules

To unload a module:

```bash
module unload mcnp/6.2.0
module unload scale/6.3.2
```

### Switching Between Versions

To switch between different versions, unload the current version and load the desired one.

#### Example

```bash
module unload scale/6.3.2
module load scale/6.2.4
```

### Accessing Documentation

Each module defines a `doc` command to access the documentation.

```bash
doc
```

- For **MCNP**, this opens the local documentation directory.
- For **SCALE**, this opens the online manual in your default web browser.

## Additional Notes

- **Configuration File (`~/.rsicc_roots.conf`)**:
  - Must be created by the user.
  - Should contain the root paths to your MCNP and SCALE installations.
  - Uses Tcl syntax since the modulefiles source it.

- **Environment Variables**:
  - The modulefiles set environment variables and modify `PATH` based on the root paths provided.
  - Ensure that the paths in your configuration file are accurate.

- **Modulefile Structure**:
  - The modulefiles are versioned and located in subdirectories (e.g., `mcnp/6.2.0`).
  - They source the configuration file to obtain the installation paths.

- **Customizing Modulefiles**:
  - If you install new versions, add the corresponding paths to your configuration file.
  - You can use the existing modulefiles as templates for new versions.

## Support

If you encounter any issues or have questions:

- **Verify Paths**: Ensure all paths in `~/.rsicc_roots.conf` are correct.
- **Check Error Messages**: Read any error messages carefully; they often indicate the problem.
- **Consult Documentation**: Refer to the modulefiles and comments for guidance.
- **Contact**: Reach out to the repository maintainer for assistance.

---

**Disclaimer**: MCNP and SCALE are proprietary software packages distributed by RSICC. Ensure you comply with all licensing agreements and export control regulations when using these tools.

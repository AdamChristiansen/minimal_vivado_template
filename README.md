# Vivado Minimal Template

This is a template for creating a minimal Xilinx Vivado project that can easily
be stored under version control. The default Xilinx Vivado project structure is
difficult to fit under version control, so the solution was to completely
separate the source from the output products. Using this system, all of the
outputs are placed in a directory, and the whole directory can be ignored by
version control. A separate directory of source files is maintained, and those
are the only project file that need to be tracked.

## Setting Up a New Project

The easiest way to use this template is to clone this repository and edit the
`generate_project.tcl` file. At the top of the file is a list of parameters that
can be changed, and comments descibing what each does.

This repository already contains a `.gitignore` that ignores the approprate
files, and it also has the source directory set up. The structure of this
project looks like

    proj/
    src/
      | constraints/
      | hdl/
      | ip/
      | repo/
      | sim/
    tcl/
    .gitignore
    generate_project.tcl

Here the `proj/` directory is generated by Xilinx Vivado using the
`generate_project.tcl` script. This diorectory (and all of its contents) are
optional. If they exist they will be loaded, otherwwise they will be skipped.
The `tcl/` directory contains empty scripts that are hooked into the synthesis
and implementation processes. The scripts are empty by default, though they can
be used to add custom behaviour.

The `src/` directory is broken into many subdirectories. All of the
subdirectories are optional, so if any of them do not exist then the script will
skip the steps associated with them. Here is an explanation of each directory.

*   `constraints/` contains all of the contstraints files used in the project
*   `hdl/` contains all of the HDL design sources
*   `ip/` contains all of the IP files used in the design. Only the `.xci` file
    is needed, because everything can be generated from it. Note that the `.xci`
    files cannot go directly in this directory. They must go in a directory with
    the same name as the `.xci` file but without the extension. This is because
    Vivado will generate the IP in-source, so they need their own directory. As
    an example, suppose that there is IP named `adder32`, then its path must be
    `/src/ip/adder32/adder32.xci`.
*   `repo/` is a repository for custom IP.
*   `sim/` constains all of the simulation sources.

## How to Run

To use this script, open Xilinx Vivado and select `Tools > Run Tcl Script...`,
then select the `generate_project.tcl` script in the file exporer. The script
will run and produce the Vivado project by importing all of the project sources.

If the `proj/` directory already exists, then the script will not be able to
create the project because a project already exists in the `proj/` directory.

Make sure to to update your project part in `generate_project.tcl` file if it is
different from the default part.

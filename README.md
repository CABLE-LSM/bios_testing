# bios_1000pts

Runs the final step (step 6. Final centennial run) of the BIOS 1000pts
configuration initialised from restart files.

# bios_testing

This repository contains CABLE test configurations for BIOS3 development (see https://github.com/CABLE-LSM/CABLE/issues/276).

## How to run a configuration (Gadi):

1. Clone the repository into `scratch` space (READ ONLY):

```sh
git clone https://github.com/CABLE-LSM/bios_testing.git /scratch/$PROJECT/$USER/bios_testing
```

If you want to make changes and push these changes to the remote repository, then clone via SSH:

```sh
git clone git@github.com:CABLE-LSM/bios_testing.git /scratch/$PROJECT/$USER/bios_testing
```

2. Checkout a configuration branch. E.g. `act9test`:

```sh
git checkout act9test
```

Configurations in this repository exist as `git` branches. To see all available configurations, run:

```sh
git branch -a
```

3. Edit the configuration shell script (`config.sh`) and set `EXE` to the absolute path of the CABLE executable.

4. Submit the `run.sh` PBS job script.

```sh
qsub run.sh
```

## Run directory structure:

Here is the directory structure produced for the `act9test` run:

```sh
.
├── bios_act9test.o117989865
├── bios.nml
├── blaze.nml
├── cable-mpi -> /home/189/sb8430/cable/offline/cable-mpi
├── cable.nml
├── clean.sh
├── config.sh
├── input
│   ├── bios_cable_rst.nc -> /g/data/rp23/experiments/2024-04-17_BIOS3-merge/sb8430/bios_act9test/restart_1700_1899/bios_cable_rst.nc
│   ├── bios_casa_rst.nc -> /g/data/rp23/experiments/2024-04-17_BIOS3-merge/sb8430/bios_act9test/restart_1700_1899/bios_casa_rst.nc
│   ├── bios_climate_rst.nc -> /g/data/rp23/experiments/2024-04-17_BIOS3-merge/sb8430/bios_act9test/restart_1700_1899/bios_climate_rst.nc
│   ├── def_soil_params.txt -> /g/data/rp23/experiments/2024-04-17_BIOS3-merge/sb8430/params_bios/def_soil_params.txt
│   ├── def_veg_params.txt -> /g/data/rp23/experiments/2024-04-17_BIOS3-merge/sb8430/params_bios/def_veg_params.txt
│   ├── pftlookup.csv -> /g/data/rp23/experiments/2024-04-17_BIOS3-merge/sb8430/params_bios/pftlookup.csv
│   └── pop_bios_ini.nc -> /g/data/rp23/experiments/2024-04-17_BIOS3-merge/sb8430/bios_act9test/restart_1700_1899/pop_bios_ini.nc
├── logs
│   ├── log_cable.txt
│   └── log_out_cable.txt
├── LUC.nml
├── outputs
│   ├── bios_out_cable.nc
│   ├── bios_out_casa.nc
│   └── cnpfluxOut.csv
├── README.md
├── restart
│   ├── bios_cable_rst.nc
│   ├── bios_casa_rst.nc
│   ├── bios_climate_rst.nc
│   └── pop_bios_ini.nc
├── run.sh
└── setup.sh
```

`bios_act9test.o117989865`: PBS log file

`bios.nml`: BIOS namelist

`blaze.nml`: BLAZE namelist

`cable-mpi -> /home/189/sb8430/cable/offline/cable-mpi`: Symlinked CABLE MPI executable

`cable.nml`: CABLE namelist

`clean.sh`: Cleanup script (resets the run directory to original state)

`config.sh`: Configuration script

`input`: Input directory

`logs`: Directory containing CABLE log files

`LUC.nml`: LUC namelist

`outputs`: Directory containing CABLE output files

`README.md`: README file

`restart`: Directory containing CABLE restart files

`run.sh`: run script (PBS job script)

`setup.sh`: setup script (always runs prior to executing CABLE)

## How to generate a code coverage report:

1. Add `-prof-gen=srcpos -prof-dir=<path/to/profiling/output/dir>` to Intel
   compiler flags.
2. Compile and run CABLE.
3. [Gadi] Load the Intel compiler module: `module load intel-compiler`.
4. Change directory into the profiling output directory and run `profmerge -a`.
5. Generate HTML coverage report: `codecov -prj myProject -spi pgopti.spi -dpi
   pgopti.dpi`. This creates a single HTML file (CODE_COVERAGE.HTML) and a
   sub-directory (CodeCoverage) in the current directory. Open the file in a
   web browser to view the reports.

See [Code Coverage Tool][code-coverage-tool] for more information.

[code-coverage-tool]: https://www.intel.com/content/www/us/en/docs/fortran-compiler/developer-guide-reference/2023-0/code-coverage-tool.html

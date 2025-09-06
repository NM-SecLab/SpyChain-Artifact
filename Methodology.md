# Documentation / Methodology

This section explains how one could conceptually reproduce the simulation scenarios described in the paper. It assumes the reviewer is able to download and build **NASA’s NOS3 framework** (publicly available on GitHub) and does not provide the complete malicious source code. Instead, it outlines which components were extended and which configuration files were modified.

---

## 1. Building and Forking NOS3

- Navigate to the [NOS3 GitHub page](https://github.com/nasa/nos3).
- **Fork** the repository. When forking, *deselect* “Copy main branch only” to ensure all branches are included.
- Clone your fork:
  ```bash
  git clone https://github.com/YOUR_USERNAME/nos3.git
  cd nos3

Add NASA’s repo as upstream:
git remote add upstream https://github.com/nasa/nos3.git
git fetch upstream
git checkout -b dev upstream/dev

Keep fork in sync:
git fetch upstream
git checkout dev
git merge upstream/dev
git push origin dev

Initialize Submodules:
git submodule update --init --recursive

Build NOS3 inside the Vagrant VM:
vagrant up
vagrant reload
vagrant ssh
cd /vagrant/nos3
make prep
make
make launch

## 2. Adding New Components

Create a GitHub repo for your component and add it to the components:
git clone https://github.com/YOUR_USERNAME/newComponent.git
git submodule add -f -b main https://github.com/YOUR_USERNAME/newComponent.git ./components/newComponent
git submodule update --init --recursive
git submodule status
git add .gitmodules components/newComponent
git commit -m "Added newComponent component"
git push origin dev

Generate a component template
cd nos3/components/sample
./generate_template.sh newComponent

Add the new component to startup and build scripts:
cfg/nos3_defs/cpu1_cfe_es_startup.scr
cfg/nos3_defs/targets.cmake
scripts/fsw/fsw_cfs_launch.sh
scripts/gsw/launch_gsw.sh
cfg/sc-full-config.xml
cfg/sims/nos3-simulator.xml
scripts/cfg/configure.py

## 3. Configuring Message IDs and Tables

Assign unique CCSDS Message IDs components:

// newComponent
#define newComponent_CMD_MID        0x18F1
#define newComponent_REQ_HK_MID     0x18F2
#define newComponent_HK_TLM_MID     0x08F1
#define newComponent_DEVICE_TLM_MID 0x08F2

Modify tables as needed:
to_config.c – add telemetry output for newComponent.
to_lab_sub.c – subscribe TO app to new telemetry.
sch_def_msgtbl.c / sch_def_schtbl.c – set up scheduled housekeeping requests.
sc_rts00x.c – define stored command sequences if automation is needed.
ds_file_tbl.c / ds_filter_tbl.c – configure data storage if logging telemetry.

## 4. Ground System (COSMOS) Integration

In gsw/cosmos/config/:
system/system.txt – declare newComponent as target.
tools/cmd_tlm_server/cmd_tlm_server.txt – add newComponent to UDP sections.
COMPONENTS/newComponent/cmd_tlm/newComponent_CMD.txt & newComponent_TLM.txt – define ground commands/telemetry.

## 5. References

https://github.com/nasa/nos3
cFE Application Developer’s Guide (fsw/cfe/docs/cFE Application Developers Guide.md)


# *bsp-probe [Andrys Jiri, 2018.12.18, v0.1 ]*  

 Author        : Jiri Andrys  
 Maintainer    : Jiri Andrys  
 Contributors  : Jiri Andrys  
  
# 1. Contents:

* [2. Overview](#2-overview)
* [3. Getting Started](#3-getting-started) 
  * [3.1 Installation](#31-installation)
  * [3.2 Run](#32-run)
  * [3.3 Example](#33-example)
  * [3.4 Run Virtual Environment in Windows](#34-run-virtual-environment-in-windows)
* [4. Dependency List](#4-dependency-list)

# 2. Overview
The `bsp-probe` is collecting information from BSP and storing to **bsp-probe.log**.  
Till now only NXP based BSPs are supported. 
The bsp-probe.log includes:
    - list of yocto layers
    - yocto layers revisions
    - git hashes of all source files 
    - local.conf
    - kernel configuration

Sometimes publicly accessible BSP is used by others to develop software and 
assembly of BSP(manifest.xml) can not include related software.

Usually people and teams whose developing applications software differs from team which is
responsible for platform development.
In case that there is light bond in release chain, separation can speed up development process.
Once application team stabilize release, then it can be added to BSP.
Middle stages could be tightened by this tool as assembly information stored by this tool. 

The **repo info** command prints basic information about layers provided by manifest.xml.
Once we have at least one layer out of manifest.xml we can not use repo info command.

Bsp-probe has been tested on following systems:  

 * Ubuntu 14.04(64bit)
 * Ubuntu 16.04(64bit with docker) 
 * Fedora 24(64bit)  

Together with **git-striper** is **bsp-probe** used for releasing requests.


# 3. Getting Started 

## 3.1 Installation

- **No installation is necessary.** 
-  The bsp-probe is added to BSP by maintainer and is located in bsp-release layer :    
sources/meta-*-bsp-release/tools/bsp-probe **
- In order to ease of using bsp-probe link to tool is added to sources/poky/scripts directory 
which is included in PATH.
- Link in sources/poky/scripts is added by manifest.xml during repo sync phase.   


## 3.2 Run

The tool have to be executed in environment where  
bitbake command is available  
**and**    
after all layers have been added to bblayers.conf  
**and**    
configuration in local.conf for given build is in final state   
**and**  
build of image file have finished.


## 3.3 Example
After we have finished configuration and build final image we can run bsp-probe(step 5). 

`1. fslbsp$ repo init -u https://github.com/XXX.git -b XXX -m XXX.xml`  
`2. fslbsp$ repo sync`     
`3. fslbsp$ SDKMACHINE=$(uname -m) MACHINE=XXX source fsl-setup-release.sh -b build`     
`4. fslbsp/build$ bitbake imageXXX`  
`5. fslbsp/build$ bsp-probe `     


# 4. Dependency List

1. Standard tools, included in almost all kind of distros and installed by default:  
   >` bash, grep, awk, mkdir, git, find, sort, pwd, printf, sed, mktemp, dirname, readlink, bitbake, bitbake-layers`  


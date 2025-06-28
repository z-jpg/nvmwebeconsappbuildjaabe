‹  lJPh  ì½Ùr I–(6¯ _á R ’ ,$È* QX’$Š €F‚äÔ°8IÏ ÏÌ`ÆVá ™HTSoÒ›Ìô*»/wdW& “ÉìÊL6&Ó½o }Èý sÜ=¶Ì À¥85eDW3Ã÷íøÙüøñŸÙ Îæš³¶úw¿Öß ü=x°I¿ð×ü¥ïõÍµ» 6 Ü½· 
Download for Linux and Unix
It is easiest to install Git on Linux using the preferred package manager of your Linux distribution. If you prefer to build from source, you can find tarballs on kernel.org. The latest version is 2.50.0

Debian/Ubuntu
For the latest stable version for your release of Debian/Ubuntu

# apt-get install git
For Ubuntu, this PPA provides the latest stable upstream Git version

# add-apt-repository ppa:git-core/ppa
# apt update; apt install git
Fedora
# yum install git (up to Fedora 21)
# dnf install git (Fedora 22 and later)
Gentoo
# emerge --ask --verbose dev-vcs/git
Arch Linux
# pacman -S git
openSUSE
# zypper install git
Mageia
# urpmi git
Nix/NixOS
# nix-env -i git
FreeBSD
# pkg install git
Solaris 9/10/11 (OpenCSW)
# pkgutil -i git
Solaris 11 Express, OpenIndiana
# pkg install developer/versioning/git
OpenBSD
# pkg_add git
Alpine
$ apk add git
Red Hat Enterprise Linux, Oracle Linux, CentOS, Scientific Linux, et al.
RHEL and derivatives typically ship older versions of git. You can download a tarball and build from source, or use a 3rd-party repository such as the IUS Community Project to obtain a more recent version of git.

Slitaz
$ tazpkg get-install git
# Upendo Page Manager Module for DNN  

This module allows you to delegate the page management responsibilities to people that are not an Administrator.  Ordinarily, you'd have to promote the person to having full admin rights to the entire website, just to get some help managing pages and **applying SEO updates**.  This module fixes that mess!  

## How to Use 💪🏽  
All you need to do is [download the latest release](https://github.com/UpendoVentures/Upendo-Dnn-PageManager/releases/latest), and [don't forget to unblock the installation package](https://hotcakescommerce.zendesk.com/hc/en-us/articles/10932095222157-How-to-Unblock-File-Downloads).  

Next, [install this module](https://www.youtube.com/watch?v=MgLaV0J_eLk&list=PLojRGd54eWTiK-0y8o5EBYVcCY2yzhTZk&index=4&pp=gAQBiAQB) like you would at any other time, then add it to a page.  

From there, it should all be self-explanatory and follow the same workflows you normally might use when managing modules on your DNN website.  

You simply assign view permissions to anyone you wish to see that page/module.  They'll be able to manage user accounts and roles on your behalf.  

<hr />  

## `Sponsors == (typeOf superHuman) Awesome;`  

> Yes, it's not real code. It's just supposed to be fun. :P

This solution is created and maintained by [Upendo Ventures](https://upendoventures.com/What/CMS/DNN) for the [DNN CMS Community](https://dnncommunity.org). Please consider [sponsoring us](https://github.com/sponsors/UpendoVentures) for this and [the many other open-source efforts we do](https://upendoventures.com/What/CMS/DNN/Extensions).  It's a lot.  :)  

- [Sponsor Us](https://github.com/sponsors/UpendoVentures) (we're grateful at any level 🙏🏽)  

## 🛠️ Need SLA-Based Support?  
If you need more help than what we can provide here, we'd be happy to help you via [Upendo DNN Support](https://upendodnn.com).  

>  😎 This is an **officially supported** extension! 🙌🏽   [DNN Extensions with Support](https://upendodnn.com/Extensions)  

<hr />  

# Developers Only 🤓  

If you're not a developer, the rest of this README is not going to interest you. 😉  

This solution was built using the [Upendo DNN Generator](https://github.com/UpendoVentures/generator-upendodnn#readme).  

<hr />

**A Special Note to ALL Developers...**  
Please do not begin any development until you first read through and understand all of the notes in the README below.  

## Background  
The previous version was not adhering to known best practices and as a result, it was unclear of how to find and maintain it. This version has been cleaned up and restructured with best practice architecture, build, versioning, and deployment in mind.  

## Solution  
The solution currently expects to be in the following environment, but you can update that to be any version you'd like, provided all extensions will be compatible:  

- DNN:  09.04.04  
- Hotcakes Commerce:  03.02.03  
- SQL:  2014+  

You should build and develop in a development environment that's separate from the local environment where you'd be testing.  The examples below help to illustrate this...  

- Development Path:  `C:\Work\ProjectName\source-code\`  
- Staging/Testing Path:  `C:\Work\ProjectName\website\`  

The *Development Path* is where the source code (solution) should be contained.  The *Staging/Testing Path* is where the testing website instance should be restored to and ran from via IIS.  

While you can technically do everything from a single path, this model helps to reduce environmental synchronization, duplication, and testing issues. It also often reduces ramp up time between testing scenarios where installations, upgrades, back-ups, and restorations are necessary.  

Either way, is up to you.  

## Getting Started  

You should get a backup of the website and database from production, then overwrite those files using this repo.  (Optional) It may be a good idea to run a data cleansing script against the database to clear out any sensitive data and/or PII.  

## Builds  

There are two possible paths for development, building and testing related to the suggested approach for this solution.  

1. Restore the website to the *Development Path*. When you build, test the updates from that path.  
2. Restore the website to the *Staging/Testing Path*. When you build, you'll need to install the extensions into this website.  

__Please Note__: It's possible to follow both approaches. This allows the website in your *Staging/Testing Path* to remain as clean as possible and be a true test before deploying to a true staging environment and/or in production.  

### Debug Mode  

When you build the solution or any single project in **DEBUG** mode, the following occurs:  

- All source code is built in debug mode.  
- Any relevant DLL's are generated and placed into the `/website/Bin/` folder.  
- Any relevant files needed to see/use the extensions are placed into their respective locations (e.g., DesktopModules, Portals, Skins, Containers, etc.).  

### Release Mode  

When you build the solution or any single project in **RELEASE** mode, the following occurs:  

- All source code is built in debug mode.  
- All extensions are packaged into installable DNN extension packages.  
- Extensions will be found in their respective folders in the `/website/Install` folder:  
  - `Hotcakes-Integration`:  Contains Hotcakes Commerce viewsets. (_This is an non-standard folder that DNN is unaware of._)  
  - `Library`: Contains class libraries (DLL's).  
  - `Module`:  Contains custom modules and skin objects.  
  - `Skin`:  Contains theme packages.  

When there are DLL's involved, there are two packages created, Install and Symbols. The respective work will be seen at the end of the respective file name.  

- Install: Used to install or upgrade an extension.  
- Symbols: Used to install the PDB files for the DLL's in the installation package. Used for troubleshooting only. Always remember to uninstall the symbols when you're done troubleshooting.  

**Special Developer Note**  
_If you don't remember to uninstall the symbols package, it could result in upgrade and/or troubleshooting issues in the future._  

## Development Environment  

Steps 1 through 8 are considered to be more for set-up, while the remaining steps are for ongoing development.  

1. Fork/install source code (see suggested paths above).  
2. Create a database and restore a backup from production. Add a user to the database that has `db_owner` permissions.  
3. Update the `PortalAlias` table to add your new website domain name and make sure it's marked as the "Primary" domain name for the respective `PortalID`.  
4. Restore a copy of the website backup to the `/website` folder (create the `/website` folder in the root, if necessary)  
5. Update the web.config to have the updated database connection string.  
6. Update the Hosts file to have the new domain name (if necessary).  
7. Update IIS to point to the desired `/website` folder(s).  
8. View the website in your preferred web browser.  
9. Open the solution.  
10. Ensure that the solution can build in both DEBUG and RELEASE modes.  
11. Update the code and build as necessary (see build notes above).  
12. Build in Debug mode will push the code updates into the `Website\DesktopModules` folder (for modules, and other areas for other extensions, such as `\Bin` for Libraries)  
13. Build in Release mode will create the release packages in the `Install\ExtensionType` folder (e.g., Skins, Modules, Libraries, etc.)  

### Working with Angular/ClientApp

For working with Angular, it require to have ClientApp inside DesktopModules.

1. Copy `ClientApp` folder under `Upendo.Modules.DnnPageManager` folder into `Website/DesktopModules/Upendo.Modules.DnnPageManager`
2. Open `Website/DesktopModules/Upendo.Modules.DnnPageManager/ClientApp` with VS-Code
3. Open `package.json`
4. Under `scripts` section, add this line
```
"devwatch": "ng build --output-hashing none --watch"
```
5. Open Terminal and execute 
```
npm run devwatch
```
6. Now, whenever there's a change, it will rebuild a clean version of it.
7. Refresh web browser to see the result. (Hard refresh to remove cache)

### Solution Folder Architecture  

Here is an explanation of each of the top-level folders found in the solution. These folders are 
also reflected the same way when viewed in Visual Studio, when necessary.  

- Assets: Contains any dependencies or backup files that may be necessary (except website/database backups).  
- Build: Contains supporting files that enable the build processes mentioned above. These files should usually not be changed.  
- Libraries: Contains class librarys that either deploy on their own, and/or are deployed within another packaged extension.  
- Modules: Contains modules.  
- References: Contains references that may be used by one or many of the projects in the solution.  
- Skin-Objects: Contains skin objects that the theme might need to use.  
- Skins: Contains theme packages (skins and containers).  
- Viewsets: Contains Hotcakes Commerce viewset packages.  
- Website: This is discussed earlier in this document.  

There is a `packages` that may be created as a result of building the solution or a project. This is created by Nuget and is not part of this solution architecture.  

### First Time Builds & Deployments  
When an extension is new to the solution, there may be an extra bit of setup required.  

1. Build the extension in DEBUG mode so the deployment files are put into their respective places.  
2. View the website and login as a superuser.  
3. Manually install the extension in the Extensions view by using it's manifest file.  
4. If there are any database dependencies, manually run the SqlDataProvider file(s) to make the necessary schema updates to the database.  
5. Add the extension to a page or otherwise use it as it's intended.  

Alternatively, you can build the solution in RELEASE mode and install that package into the 
website. Then build the solution/project again in DEBUG mode.  

### Debugging  
In order to debug the code, you'll need to follow the steps below:  

1. Open Visual Studio using the "As Administrator" option in Windows.  
2. Build the project(s) solution in DEBUG mode.  
3. Ensure that the web.config is set to allow debugging:  `<compilation debug="true" strict="false" optimizeCompilations="true">`  
4. Run the website and view the page that contains the code you wish to debug.  
5. In Visual Studio, choose the Debug > Attach to Process feature (a.k.a., `<Ctrl>`+`<Alt>`+`<P>`).  
6. Find `w3wp.exe` in the list and click the Attach button.  
7. Set any breakpoints that you wish to hit and step through.  
8. View the page again and/or perform the steps necessary to hit the breakpoint.    

### Adding/Updating References  
Any references that can't or shouldn't be managed by Nuget are managed by the `SolutionReferences.targets` file in the `Build` folder.  This central file allows you to update the references in a single place, for all projects.  

If you're adding/editing references that come from DNN (or from the References folder), DO NOT use the Visual Studio IDE to do this. It will result in long-term management issues for the solution. Instead, you should view any of the `.csproj` files in a separate text editor to see how to properly add a reference.  It's not possible to add it correctly in the Visual Studio IDE.  

#### General Instructions  
When necessary, first add the new references to the correct references folder/path, and then update the `SolutionReferences.targets` file.  

Include the following line in the `.csproj` file, just before the references section (if necessary).  

```xml
<Import Project="..\..\Build\SolutionReferences.targets" Condition="false" />
```  

__Please Note__: It's currently required for you to manually update the version numbers in the `.csproj` file when working with any `Library` type project as well.  Please see [Issue #17](https://github.com/UpendoVentures/generator-upendodnn/issues/17) for more details and to potentially help fix this.  :)  

Next, add the appropriate reference, per the targets file.  Here are examples for DNN, and Hotcakes Commerce.  

```xml
  <ItemGroup>
    <Reference Include="DotNetNuke">
      <SpecificVersion>False</SpecificVersion>
      <HintPath>$(DnnReferencePath)\DotNetNuke.dll</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Hotcakes.Commerce">
      <SpecificVersion>False</SpecificVersion>
      <HintPath>$(HccReferencePath)\Hotcakes.Commerce.dll</HintPath>
      <Private>False</Private>
    </Reference>
  </ItemGroup>
```  

Note the use of `SpecificVersion` and `Private` above.  These are very important to ensuring consistent builds and packages.  

If you reference a DLL in the references folder directly, simply edit the `.csproj` file afterward to follow the pattern outlined above.  

# Source Control  
It may be noticed that this solution and it's architecture are both complicated and elegant at the same time. A beginning developer may feel overwhelmed at first, but this solution greatly simplifies all development. This is especially important and true due to how tightly integrated and dependant all of the projects and code is.  

## Solution  
As such, this solution would function best when used with a Git-based source control product, such as Git, GitHub, and BitBucket.  There are many workflows that could be used for this solution as it relates to the interaction with Git.  For developers that are new to Git and its potential workflows, a workflow known as "centralized workflow" may be tempting, because it is how solo developers and SVN/TFS has been used in the past. When using Git, this is generally a mistake since it ignores all of the features Git offers.  

## Workflow  
It is highly recommended that a [Gitflow Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) workflow is used and followed. This empowers all developers that may be involved to work at the same time, independently, regardless of location, focus, and feature/issue they're working on.  Initially, some developers will feel this simply over-complicates the development process, but the moment something "bad" happens during a development cycle, this process will very clearly highlight itself as having saved the day.  This approach also ensures that one or more PM's are able to see and know the state of the code base, pending updates, and more because they're at all times seeing branches in a logical pattern and reviewing pull requests to the primary/release branches.  

## Branches  
The primary branches that are present and used may change over time.  Those potential branches are defined below.  There are no strict requirements, except as defined as the project/product manager assigned to this solution.  Naming conventions such as those listed below are very important to ensure the productivity of all parties involved during development, so that everyone can easily understand the purpose of various branches and their contained code/updates.  

- **main** - A _main_ (formerly known as `Master`) branch should always be present and used, regardless of the way Git is leveraged. This branch is always expected to **only** contain tested and unbroken code at all times. At no time should code be committed to this branch without first being verified to be tested and unbroken.  Pull requests into this branch would often only come from the _development_ branch.  
- **development** - A _development_ branch is not currently being used and it is not necessarily required moving forward, depending on how development will be done in the future. It is best used when development is expected to follow a more strict schedule or versioning pattern.  If continuous integration (CI) or similar solutions are to be integrated, this branch will also become necessary. This branch is where other branches are merged to first, before being determined to be production-ready. Once the code is merged to the _development_ branch, a QA engineer would smoke and regression test the code in this branch. Once all updates are verified to be correct and not break other existing features, the code in this branch would then be merged into the _master_ branch as part of a release process/cycle.  This code would also be what is used to push into a staging/UAT environment.  Pull requests generally would always come to this branch, and not to the master branch.  
- **Issues\name-number** - This is a common branching naming convention when working on bugs.  The name/number would reference a work item/task ID or a very short name to identify the update. Examples of this naming convention would include `Issues\Issue-12345` and `Issues\email-template-routing`.
- **Features\name-number** - This is a common branching naming convention when adding new features.  The name/number would reference a work item/task ID or a very short name to identify the update. Examples of this naming convention would include `Features\Issue-12345` and `Features\salesforce-integration`.
- **Tasks\name-number** - This is a common branching naming convention when working on tasks that aren't necessarily a new feature or bug fix.  The name/number would reference a work item/task ID or a very short name to identify the update. Examples of this naming convention would include `Tasks\Issue-12345` and `Tasks\03.02.01-packaging`.  
- **Releases\version** - This naming convention and its branches are only necessary when following a release schedule that's highly focused on a product management approach that includes versioning. Ideally, in this scenario, all projects would always have the same version.  This workflow would be ideal for a solution like this, but it also depends on the level of and availability of resources assigned to the project. Having such a approach also helps to identify and troubleshoot differences over time.  An example of a branch using this approach would be `Releases\03.02.01`.  The code that is included in this branch would come only from the _master_ branch, and this branch would be created directly prior to pushing the updates into production from a staging/UAT environment.  

# Support for this Project  
This solution and the related materials are proudly created and provided by Upendo Ventures.  

- [Visit Us](https://upendoventures.com/Support)  
- [E-Mail Us](mailto:solutions@upendoventures.com)  
- [Other Ways to Contact Us](https://upendoventures.com/Contact-Us)  


([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
4b4154ea040349bfd40215ec4e4cc9f372fe95f3#
nvm install 20.10.0
<a href="https://github.com/nvm-sh/logos">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/nvm-sh/logos/HEAD/nvm-logo-white.svg" />
    <img src="https://raw.githubusercontent.com/nvm-sh/logos/HEAD/nvm-logo-color.svg" height="50" alt="nvm project logo" />
  </picture>
</a>

([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
# Node Version Manager [![Build Status](https://app.travis-ci.com/nvm-sh/nvm.svg?branch=master)][3] [![nvm version](https://img.shields.io/badge/version-v0.40.3-yellow.svg)][4] [![CII Best Practices](https://bestpractices.dev/projects/684/badge)](https://bestpractices.dev/projects/684)

<!-- To update this table of contents, ensure you have run `npm install` then `npm run doctoc` -->
<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
## Table of Contents

- [Intro](#intro)
- [About](#about)
- [Installing and Updating](#installing-and-updating)
  - [Install & Update Script](#install--update-script)
    - [Additional Notes](#additional-notes)
    - [Installing in Docker](#installing-in-docker)
      - [Installing in Docker for CICD-Jobs](#installing-in-docker-for-cicd-jobs)
    - [Troubleshooting on Linux](#troubleshooting-on-linux)
    - [Troubleshooting on macOS](#troubleshooting-on-macos)
    - [Ansible](#ansible)
  - [Verify Installation](#verify-installation)
  - [Important Notes](#important-notes)
  - [Git Install](#git-install)
  - [Manual Install](#manual-install)
  - [Manual Upgrade](#manual-upgrade)
- [Usage](#usage)
  - [Long-term Support](#long-term-support)
  - [Migrating Global Packages While Installing](#migrating-global-packages-while-installing)
  - [Default Global Packages From File While Installing](#default-global-packages-from-file-while-installing)
  - [io.js](#iojs)
  - [System Version of Node](#system-version-of-node)
  - [Listing Versions](#listing-versions)
  - [Setting Custom Colors](#setting-custom-colors)
    - [Persisting custom colors](#persisting-custom-colors)
    - [Suppressing colorized output](#suppressing-colorized-output)
  - [Restoring PATH](#restoring-path)
  - [Set default node version](#set-default-node-version)
  - [Use a mirror of node binaries](#use-a-mirror-of-node-binaries)
    - [Pass Authorization header to mirror](#pass-authorization-header-to-mirror)
  - [.nvmrc](#nvmrc)
  - [Deeper Shell Integration](#deeper-shell-integration)
    - [Calling `nvm use` automatically in a directory with a `.nvmrc` file](#calling-nvm-use-automatically-in-a-directory-with-a-nvmrc-file)
      - [bash](#bash)
      - [zsh](#zsh)
      - [fish](#fish)
- [Running Tests](#running-tests)
- [Environment variables](#environment-variables)
- [Bash Completion](#bash-completion)
  - [Usage](#usage-1)
- [Compatibility Issues](#compatibility-issues)
- [Installing nvm on Alpine Linux](#installing-nvm-on-alpine-linux)
  - [Alpine Linux 3.13+](#alpine-linux-313)
  - [Alpine Linux 3.5 - 3.12](#alpine-linux-35---312)
- [Uninstalling / Removal](#uninstalling--removal)
  - [Manual Uninstall](#manual-uninstall)
- [Docker For Development Environment](#docker-for-development-environment)
- [Problems](#problems)
- [macOS Troubleshooting](#macos-troubleshooting)
- [WSL Troubleshooting](#wsl-troubleshooting)
- [Maintainers](#maintainers)
- [Project Support](#project-support)
- [Enterprise Support](#enterprise-support)
- [License](#license)
- [Copyright notice](#copyright-notice)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Intro

`nvm` allows you to quickly install and use different versions of node via the command line.

**Example:**
```sh
$ nvm use 16
Now using node v16.9.1 (npm v7.21.1)
$ node -v
v16.9.1
$ nvm use 14
Now using node v14.18.0 (npm v6.14.15)
$ node -v
v14.18.0
$ nvm install 12
Now using node v12.22.6 (npm v6.14.5)
$ node -v
v12.22.6
```

Simple as that!


## About
nvm is a version manager for [node.js](https://nodejs.org/en/), designed to be installed per-user, and invoked per-shell. `nvm` works on any POSIX-compliant shell (sh, dash, ksh, zsh, bash), in particular on these platforms: unix, macOS, and [windows WSL](https://github.com/nvm-sh/nvm#important-notes).
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
<a id="installation-and-update"></a>
<a id="install-script"></a>
## Installing and Updating

### Install & Update Script

To **install** or **update** nvm, you should run the [install script][2]. To do that, you may either download and run the script manually, or use the following cURL or Wget command:
```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
```
```sh
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
```

Running either of the above commands downloads a script and runs it. The script clones the nvm repository to `~/.nvm`, and attempts to add the source lines from the snippet below to the correct profile file (`~/.bashrc`, `~/.bash_profile`, `~/.zshrc`, or `~/.profile`). If you find the install script is updating the wrong profile file, set the `$PROFILE` env var to the profile file’s path, and then rerun the installation script.

<a id="profile_snippet"></a>
```sh
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```

#### Additional Notes

- If the environment variable `$XDG_CONFIG_HOME` is present, it will place the `nvm` files there.</sub>

- You can add `--no-use` to the end of the above script to postpone using `nvm` until you manually [`use`](#usage) it:

```sh
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" --no-use # This loads nvm, without auto-using the default version
```

- You can customize the install source, directory, profile, and version using the `NVM_SOURCE`, `NVM_DIR`, `PROFILE`, and `NODE_VERSION` variables.
Eg: `curl ... | NVM_DIR="path/to/nvm"`. Ensure that the `NVM_DIR` does not contain a trailing slash.

- The installer can use `git`, `curl`, or `wget` to download `nvm`, whichever is available.

- You can instruct the installer to not edit your shell config (for example if you already get completions via a [zsh nvm plugin](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/nvm)) by setting `PROFILE=/dev/null` before running the `install.sh` script. Here's an example one-line command to do that: `PROFILE=/dev/null bash -c 'curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash'`

#### Installing in Docker
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
When invoking bash as a non-interactive shell, like in a Docker container, none of the regular profile files are sourced. In order to use `nvm`, `node`, and `npm` like normal, you can instead specify the special `BASH_ENV` variable, which bash sources when invoked non-interactively.

```Dockerfile
# Use bash for the shell
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Create a script file sourced by both interactive and non-interactive bash shells
ENV BASH_ENV /home/user/.bash_env
RUN touch "${BASH_ENV}"
RUN echo '. "${BASH_ENV}"' >> ~/.bashrc

# Download and install nvm
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.2/install.sh | PROFILE="${BASH_ENV}" bash
RUN echo node > .nvmrc
RUN nvm install
```

##### Installing in Docker for CICD-Jobs
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
More robust, works in CI/CD-Jobs. Can be run in interactive and non-interactive containers.
See https://github.com/nvm-sh/nvm/issues/3531.

```Dockerfile
FROM ubuntu:latest
ARG NODE_VERSION=20

# install curl
RUN apt update && apt install curl -y

# install nvm
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash

# set env
ENV NVM_DIR=/root/.nvm

# install node
RUN bash -c "source $NVM_DIR/nvm.sh && nvm install $NODE_VERSION"

# set ENTRYPOINT for reloading nvm-environment
ENTRYPOINT ["bash", "-c", "source $NVM_DIR/nvm.sh && exec \"$@\"", "--"]

# set cmd to bash
CMD ["/bin/bash"]

```

This example defaults to installation of nodejs version 20.x.y. Optionally you can easily override the version with docker build args like:
```
docker build -t nvmimage --build-arg NODE_VERSION=20 or 22 .
```

After creation of the image you can start container interactively and run commands, for example:
```
docker run --rm -it nvmimage

root@0a6b5a237c14:/# nvm -v
0.40.3

root@0a6b5a237c14:/# node -v
v19.9.0

root@0a6b5a237c14:/# npm -v
9.6.3
```

Noninteractive example:
```
user@host:/tmp/test $ docker run --rm -it nvmimage node -v
v20 or 22
user@host:/tmp/test $ docker run --rm -it nvmimage npm -v
20 oe 22
```
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
#### Troubleshooting on Linux

On Linux, after running the install script, if you get `nvm: command not found` or see no feedback from your terminal after you type `command -v nvm`, simply close your current terminal, open a new terminal, and try verifying again.
Alternatively, you can run the following commands for the different shells on the command line:

*bash*: `source ~/.bashrc`

*zsh*: `source ~/.zshrc`

*ksh*: `. ~/.profile`

These should pick up the `nvm` command.
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
#### Troubleshooting on macOS

Since OS X 10.9, `/usr/bin/git` has been preset by Xcode command line tools, which means we can't properly detect if Git is installed or not. You need to manually install the Xcode command line tools before running the install script, otherwise, it'll fail. (see [#1782](https://github.com/nvm-sh/nvm/issues/1782))

If you get `nvm: command not found` after running the install script, one of the following might be the reason:

  - Since macOS 10.15, the default shell is `zsh` and nvm will look for `.zshrc` to update, none is installed by default. Create one with `touch ~/.zshrc` and run the install script again.

  - If you use bash, the previous default shell, your system may not have `.bash_profile` or `.bashrc` files where the command is set up. Create one of them with `touch ~/.bash_profile` or `touch ~/.bashrc` and run the install script again. Then, run `. ~/.bash_profile` or `. ~/.bashrc` to pick up the `nvm` command.

  - You have previously used `bash`, but you have `zsh` installed. You need to manually add [these lines](#manual-install) to `~/.zshrc` and run `. ~/.zshrc`.
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
   
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion

  - You might need to restart your terminal instance or run `. ~/.nvm/nvm.sh`. Restarting your terminal/opening a new tab/window, or running the source command will load the command and the new configuration.

  - If the above didn't help, you might need to restart your terminal instance. Try opening a new tab/window in your terminal and retry.

If the above doesn't fix the problem, you may try the following:

  - If you use bash, it may be that your `.bash_profile` (or `~/.profile`) does not source your `~/.bashrc` properly. You could fix this by adding `source ~/<your_profile_file>` to it or following the next step below.
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
  - Try adding [the snippet from the install section](#z-jpg/nvmwebeconsappbuilddjaabe), that finds the correct nvm directory and loads nvm, to your usual profile (`~/.bash_profile`, `~/.zshrc`, `~/.profile`, or `~/.bashrc`).

  - For more information about this issue and possible workarounds, please [refer here](https://github.com/nvm-sh/nvm/issues/576)

**Note** For Macs with the Apple Silicon chip, node started offering **arm64** arch Darwin packages since v16.0.0 and experimental **arm64** support when compiling from source since v14.17.0. If you are facing issues installing node using `nvm`, you may want to update to one of those versions or later.
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
#### Ansible

You can use a task:

```yaml
- name: Install nvm
  ansible.builtin.shell: >
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
  args:
    creates: "{{ ansible_env.HOME }}/.nvm/nvm.sh"
```
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
### Verify Installation

To verify that nvm has been installed, do:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```sh
command -v nvm
```

which should output `nvm` if the installation was successful. Please note that `which nvm` will not work, since `nvm` is a sourced shell function, not an executable binary.

**Note:** On Linux, after running the install script, if you get `nvm: command not found` or see no feedback from your terminal after you type `command -v nvm`, simply close your current terminal, open a new terminal, and try verifying again.

### Important Notes

If you're running a system without prepackaged binary available, which means you're going to install node or io.js from its source code, you need to make sure your system has a C++ compiler. For OS X, Xcode will work, for Debian/Ubuntu based GNU/Linux, the `build-essential` and `libssl-dev` packages work.

**Note:** `nvm` also supports Windows in some cases. It should work through WSL (Windows Subsystem for Linux) depending on the version of WSL. It should also work with [GitBash](https://gitforwindows.org/) (MSYS) or [Cygwin](https://cygwin.com). Otherwise, for Windows, a few alternatives exist, which are neither supported nor developed by us:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
  - [nvm-windows](https://github.com/coreybutler/nvm-windows)
  - [nodist](https://github.com/marcelklehr/nodist)
  - [nvs](https://github.com/jasongin/nvs)

**Note:** `nvm` does not support [Fish] either (see [#303](https://github.com/nvm-sh/nvm/issues/303)). Alternatives exist, which are neither supported nor developed by us:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
  - [bass](https://github.com/edc/bass) allows you to use utilities written for Bash in fish shell
  - [fast-nvm-fish](https://github.com/brigand/fast-nvm-fish) only works with version numbers (not aliases) but doesn't significantly slow your shell startup
  - [plugin-nvm](https://github.com/derekstavis/plugin-nvm) plugin for [Oh My Fish](https://github.com/oh-my-fish/oh-my-fish), which makes nvm and its completions available in fish shell
  - [nvm.fish](https://github.com/jorgebucaran/nvm.fish) - The Node.js version manager you'll adore, crafted just for Fish
  - [fish-nvm](https://github.com/FabioAntunes/fish-nvm) - Wrapper around nvm for fish, delays sourcing nvm until it's actually used.

**Note:** We still have some problems with FreeBSD, because there is no official pre-built binary for FreeBSD, and building from source may need [patches](https://www.freshports.org/www/node/files/patch-deps_v8_src_base_platform_platform-posix.cc); see the issue ticket:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
  - [[#900] [Bug] node on FreeBSD may need to be patched](https://github.com/nvm-sh/nvm/issues/900)
  - [nodejs/node#3716](https://github.com/nodejs/node/issues/3716)

**Note:** On OS X, if you do not have Xcode installed and you do not wish to download the ~4.3GB file, you can install the `Command Line Tools`. You can check out this blog post on how to just that:

  - [How to Install Command Line Tools in OS X Mavericks & Yosemite (Without Xcode)](https://osxdaily.com/2014/02/12/install-command-line-tools-mac-os-x/)

**Note:** On OS X, if you have/had a "system" node installed and want to install modules globally, keep in mind that:

  - When using `nvm` you do not need `sudo` to globally install a module with `npm -g`, so instead of doing `sudo npm install -g grunt`, do instead `npm install -g grunt`
  - If you have an `~/.npmrc` file, make sure it does not contain any `prefix` settings (which is not compatible with `nvm`)
  - You can (but should not?) keep your previous "system" node install, but `nvm` will only be available to your user account (the one used to install nvm). This might cause version mismatches, as other users will be using `/usr/local/lib/node_modules/*` VS your user account using `~/.nvm/versions/node/vX.X.X/lib/node_modules/*`

Homebrew installation is not supported. If you have issues with homebrew-installed `nvm`, please `brew uninstall` it, and install it using the instructions below, before filing an issue.
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
**Note:** If you're using `zsh` you can easily install `nvm` as a zsh plugin. Install [`zsh-nvm`](https://github.com/lukechilds/zsh-nvm) and run `nvm upgrade` to upgrade ([you can set](https://github.com/lukechilds/zsh-nvm#auto-use) `NVM_AUTO_USE=true` to have it automatically detect and use `.nvmrc` files).

**Note:** Git versions before v1.7 may face a problem of cloning `nvm` source from GitHub via https protocol, and there is also different behavior of git before v1.6, and git prior to [v1.17.10](https://github.com/git/git/commit/5a7d5b683f869d3e3884a89775241afa515da9e7) can not clone tags, so the minimum required git version is v1.7.10. If you are interested in the problem we mentioned here, please refer to GitHub's [HTTPS cloning errors](https://help.github.com/articles/https-cloning-errors/) article.

#([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")## Git Install

If you have `git` installed (requires git v1.7.10+):

1. clone this repo in the root of your user profile
    - `cd ~/` from anywhere then `git clone https://github.com/nvm-sh/nvm.git .nvm`
1. `cd ~/.nvm` and check out the latest version with `git checkout v0.40.3`
1. activate `nvm` by sourcing it from your shell: `. ./nvm.sh`
https://github.com/nvm-sh/nvm.git .nvm`
Now add these lines to your `~/.bashrc`, `~/.profile`, or `~/.zshrc` file to have it automatically sourced upon login:
(you may have to add to more than one of the above files)

```sh
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
### Manual Install

For a fully manual install, execute the following lines to first clone the `nvm` repository into `$HOME/.nvm`, and then load `nvm`:

```sh
export NVM_DIR="$HOME/.nvm" && (
  git clone https://github.com/nvm-sh/nvm.git "$NVM_DIR"
  cd "$NVM_DIR"
  git checkout `git describe --abbrev=0 --tags --match "v[0-9]*" $(git rev-list --tags --max-count=1)`
) && \. "$NVM_DIR/nvm.sh"
```

Now add these lines to your `~/.bashrc`, `~/.profile`, or `~/.zshrc` file to have it automatically sourced upon login:
(you may have to add to more than one of the above files)

```sh
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
### Manual Upgrade

For manual upgrade with `git` (requires git v1.7.10+):

1. change to the `$NVM_DIR`
1. pull down the latest changes
1. check out the latest version
1. activate the new version

```sh
(
  cd "$NVM_DIR"
  git fetch --tags origin
  git checkout `git describe --abbrev=0 --tags --match "v[0-9]*" $(git rev-list --tags --max-count=1)`
) && \. "$NVM_DIR/nvm.sh"
```
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
## Usage

To download, compile, and install the latest release of node, do this:

```sh
nvm install node # "node" is an alias for the latest version
```

To install a specific version of node:

```sh
nvm install 14.7.0 # or 16.3.0, 12.22.1, etc
```

To set an alias:

```sh
nvm alias my_alias v14.4.0
```
Make sure that your alias does not contain any spaces or slashes.

The first version installed becomes the default. New shells will start with the default version of node (e.g., `nvm alias default`).

You can list available versions using `ls-remote`:

```sh
nvm ls-remote
```

And then in any new shell just use the installed version:

```sh
nvm use node
```

Or you can just run it:

```sh
nvm run node --version
```

Or, you can run any arbitrary command in a subshell with the desired version of node:

```sh
nvm exec 20 or 22 node --version
```

You can also get the path to the executable to where it was installed:

```sh
nvm which 20 or 22
```

In place of a version pointer like 20 or 22, you can use the following special default aliases with `nvm install`, `nvm use`, `nvm run`, `nvm exec`, `nvm which`, etc:

  - `node`: this installs the latest version of [`node`](https://nodejs.org/en/)
  - `iojs`: this installs the latest version of [`io.js`](https://iojs.org/en/)
  - `stable`: this alias is deprecated, and only truly applies to `node` `v0.12` and earlier. Currently, this is an alias for `node`.
  - `unstable`: this alias points to `node` `v0.11` - the last "unstable" node release, since post-1.0, all node versions are stable. (in SemVer, versions communicate breakage, not stability).
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
### Long-term Support

Node has a [schedule](https://github.com/nodejs/Release#release-schedule) for long-term support (LTS) You can reference LTS versions in aliases and `.nvmrc` files with the notation `lts/*` for the latest LTS, and `lts/argon` for LTS releases from the "argon" line, for example. In addition, the following commands support LTS arguments:

  - `nvm install --lts` / `nvm install --lts=argon` / `nvm install 'lts/*'` / `nvm install lts/argon`
  - `nvm uninstall --lts` / `nvm uninstall --lts=argon` / `nvm uninstall 'lts/*'` / `nvm uninstall lts/argon`
  - `nvm use --lts` / `nvm use --lts=argon` / `nvm use 'lts/*'` / `nvm use lts/argon`
  - `nvm exec --lts` / `nvm exec --lts=argon` / `nvm exec 'lts/*'` / `nvm exec lts/argon`
  - `nvm run --lts` / `nvm run --lts=argon` / `nvm run 'lts/*'` / `nvm run lts/argon`
  - `nvm ls-remote --lts` / `nvm ls-remote --lts=argon` `nvm ls-remote 'lts/*'` / `nvm ls-remote lts/argon`
  - `nvm version-remote --lts` / `nvm version-remote --lts=argon` / `nvm version-remote 'lts/*'` / `nvm version-remote lts/argon`

Any time your local copy of `nvm` connects to https://nodejs.org, it will re-create the appropriate local aliases for all available LTS lines. These aliases (stored under `$NVM_DIR/alias/lts`), are managed by `nvm`, and you should not modify, remove, or create these files - expect your changes to be undone, and expect meddling with these files to cause bugs that will likely not be supported.

To get the latest LTS version of node and migrate your existing installed packages, use
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```sh
nvm install --reinstall-packages-from=current 'lts/*'
```
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
### Migrating Global Packages While Installing

If you want to install a new version of Node.js and migrate npm packages from a previous version:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```sh
nvm install --reinstall-packages-from=node node
```

This will first use "nvm version node" to identify the current version you're migrating packages from. Then it resolves the new version to install from the remote server and installs it. Lastly, it runs "nvm reinstall-packages" to reinstall the npm packages from your prior version of Node to the new one.

You can also install and migrate npm packages from specific versions of Node like this:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```sh
nvm install --reinstall-packages-from=18 - 20 or 22
nvm install --reinstall-packages-from=iojs v18 - 20 or 22
```

Note that reinstalling packages _explicitly does not update the npm version_ — this is to ensure that npm isn't accidentally upgraded to a broken version for the new node version.

To update npm at the same time add the `--latest-npm` flag, like this:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```sh
nvm install --reinstall-packages-from=default --latest-npm 'lts/*'
```

or, you can at any time run the following command to get the latest supported npm version on the current node version 20 or 22:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```sh
nvm install-latest-npm
```

If you've already gotten an error to the effect of "npm does not support Node.js", you'll need to (1) revert to a previous node version (`nvm ls` & `nvm use <your latest _working_ version from the ls>`), (2) delete the newly created node version (`nvm uninstall <your _broken_ version of node from the ls>`), then (3) rerun your `nvm install` with the `--latest-npm` flag.
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")

### Default Global Packages From File While Installing

If you have a list of default packages you want installed every time you install a new version, we support that too -- just add the package names, one per line, to the file `$NVM_DIR/default-packages`. You can add anything npm would accept as a package argument on the command line.
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```sh
# $NVM_DIR/default-packages
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
rimraf
object-inspect@1.0.2
stevemao/left-pad
```
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
### io.js

If you want to install [io.js](https://github.com/iojs/io.js/):
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```sh
nvm install iojs
```

If you want to install a new version of io.js and migrate npm packages from a previous version:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```sh
nvm install --reinstall-packages-from=iojs iojs
```

The same guidelines mentioned for migrating npm packages in node are applicable to io.js.
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
### System Version of Node

If you want to use the system-installed version of node, you can use the special default alias "system":
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```sh
nvm use system
nvm run system --version
```
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
### Listing Versions

If you want to see what versions are installed:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```sh
nvm ls
```

If you want to see what versions are available to install:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```sh
nvm ls-remote
```
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
### Setting Custom Colors

You can set five colors that will be used to display version and alias information. These colors replace the default colors.
  Initial colors are: g b y r e

  Color codes:

    r/R = red / bold red

    g/G = green / bold green

    b/B = blue / bold blue

    c/C = cyan / bold cyan

    m/M = magenta / bold magenta

    y/Y = yellow / bold yellow

    k/K = black / bold black

    e/W = light grey / white
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```sh
nvm set-colors rgBcm
```

#### Persisting custom colors

If you want the custom colors to persist after terminating the shell, export the `NVM_COLORS` variable in your shell profile. For example, if you want to use cyan, magenta, green, bold red and bold yellow, add the following line:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```sh
export NVM_COLORS='cmgRY'
```

#### Suppressing colorized output

`nvm help (or -h or --help)`, `nvm ls`, `nvm ls-remote` and `nvm alias` usually produce colorized output. You can disable colors with the `--no-colors` option (or by setting the environment variable `TERM=dumb`):
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```sh
nvm ls --no-colors
nvm help --no-colors
TERM=dumb nvm ls
```

### Restoring PATH
To restore your PATH, you can deactivate it:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```sh
nvm deactivate
```

### Set default node version
To set a default Node version to be used in any new shell, use the alias 'default':
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```sh
nvm alias default node # this refers to the latest installed version of node
nvm alias default 18 # this refers to the latest installed v18.x version of node
nvm alias default 18.12  # this refers to the latest installed v18.12.x version of node
```

### Use a mirror of node binaries
To use a mirror of the node binaries, set `$NVM_NODEJS_ORG_MIRROR`:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```sh
export NVM_NODEJS_ORG_MIRROR=https://nodejs.org/dist
nvm install node

NVM_NODEJS_ORG_MIRROR=https://nodejs.org/dist nvm install 20 or 22
```

To use a mirror of the io.js binaries, set `$NVM_IOJS_ORG_MIRROR`:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```sh
export NVM_IOJS_ORG_MIRROR=https://iojs.org/dist
nvm install iojs-v1.0.3

NVM_IOJS_ORG_MIRROR=https://iojs.org/dist nvm install iojs-v20 or 22
```

`nvm use` will not, by default, create a "current" symlink. Set `$NVM_SYMLINK_CURRENT` to "true" to enable this behavior, which is sometimes useful for IDEs. Note that using `nvm` in multiple shell tabs with this environment variable enabled can cause race conditions.
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
#### Pass Authorization header to mirror
To pass an Authorization header through to the mirror url, set `$NVM_AUTH_HEADER`
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```sh
NVM_AUTH_HEADER="Bearer secret-token" nvm install node
```
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
### .nvmrc

You can create a `.nvmrc` file containing a node version number (or any other string that `nvm` understands; see `nvm --help` for details) in the project root directory (or any parent directory).
Afterwards, `nvm use`, `nvm install`, `nvm exec`, `nvm run`, and `nvm which` will use the version specified in the `.nvmrc` file if no version is supplied on the command line.

For example, to make nvm default to the latest 5.9 release, the latest LTS version, or the latest node version for the current directory:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```sh
$ echo "5.9" > .nvmrc

$ echo "lts/*" > .nvmrc # to default to the latest LTS version

$ echo "node" > .nvmrc # to default to the latest version
```

[NB these examples assume a POSIX-compliant shell version of `echo`. If you use a Windows `cmd` development environment, eg the `.nvmrc` file is used to configure a remote Linux deployment, then keep in mind the `"`s will be copied leading to an invalid file. Remove them.]

Then when you run nvm use:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```sh
$ nvm use
Found '/path/to/project/.nvmrc' with version <5.9>
Now using node v5.9.1 (npm v3.7.3)
```

Running nvm install will also switch over to the correct version, but if the correct node version isn't already installed, it will install it for you.
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```sh
$ nvm install
Found '/path/to/project/.nvmrc' with version <18>
Downloading and installing node v20 or 22...
Downloading https://nodejs.org/dist/v20 or 22/node-v20 or 22-linux-x64.tar.xz...
#################################################################################### 100.0%
Computing checksum with sha256sum
Checksums matched!
Now using node v118 (npm v20 or 22)
```

`nvm use` et. al. will traverse directory structure upwards from the current directory looking for the `.nvmrc` file. In other words, running `nvm use` et. al. in any subdirectory of a directory with an `.nvmrc` will result in that `.nvmrc` being utilized.

The contents of a `.nvmrc` file **must** contain precisely one `<version>` (as described by `nvm --help`) followed by a newline. `.nvmrc` files may also have comments. The comment delimiter is `#`, and it and any text after it, as well as blank lines, and leading and trailing white space, will be ignored when parsing.

Key/value pairs using `=` are also allowed and ignored, but are reserved for future use, and may cause validation errors in the future.

Run [`npx nvmrc`](https://npmjs.com/nvmrc) to validate an `.nvmrc` file. If that tool’s results do not agree with nvm, one or the other has a bug - please file an issue.

### Deeper Shell Integration

You can use [`nvshim`](https://github.com/iamogbz/nvshim) to shim the `node`, `npm`, and `npx` bins to automatically use the `nvm` config in the current directory. `nvshim` is **not** supported by the `nvm` maintainers. Please [report issues to the `nvshim` team](https://github.com/iamogbz/nvshim/issues/new).

If you prefer a lighter-weight solution, the recipes below have been contributed by `nvm` users. They are **not** supported by the `nvm` maintainers. We are, however, accepting pull requests for more examples.

#### Calling `nvm use` automatically in a directory with a `.nvmrc` file

In your profile (`~/.bash_profile`, `~/.zshrc`, `~/.profile`, or `~/.bashrc`), add the following to `nvm use` whenever you enter a new directory:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
##### bash

Put the following at the end of your `$HOME/.bashrc`:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```bash
cdnvm() {
    command cd "$@" || return $?
    nvm_path="$(nvm_find_up .nvmrc | command tr -d '\n')"

    # If there are no .nvmrc file, use the default nvm version
    if [[ ! $nvm_path = *[^[:space:]]* ]]; then

        declare default_version
        default_version="$(nvm version default)"

        # If there is no default version, set it to `node`
        # This will use the latest version on your machine
        if [ $default_version = 'N/A' ]; then
            nvm alias default node
            default_version=$(nvm version default)
        fi

        # If the current version is not the default version, set it to use the default version
        if [ "$(nvm current)" != "${default_version}" ]; then
            nvm use default
        fi
    elif [[ -s "${nvm_path}/.nvmrc" && -r "${nvm_path}/.nvmrc" ]]; then
        declare nvm_version
        nvm_version=$(<"${nvm_path}"/.nvmrc)

        declare locally_resolved_nvm_version
        # `nvm ls` will check all locally-available versions
        # If there are multiple matching versions, take the latest one
        # Remove the `->` and `*` characters and spaces
        # `locally_resolved_nvm_version` will be `N/A` if no local versions are found
        locally_resolved_nvm_version=$(nvm ls --no-colors "${nvm_version}" | command tail -1 | command tr -d '\->*' | command tr -d '[:space:]')

        # If it is not already installed, install it
        # `nvm install` will implicitly use the newly-installed version
        if [ "${locally_resolved_nvm_version}" = 'N/A' ]; then
            nvm install "${nvm_version}";
        elif [ "$(nvm current)" != "${locally_resolved_nvm_version}" ]; then
            nvm use "${nvm_version}";
        fi
    fi
}

alias cd='cdnvm'
cdnvm "$PWD" || exit
```

This alias would search 'up' from your current directory in order to detect a `.nvmrc` file. If it finds it, it will switch to that version; if not, it will use the default version.
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
##### zsh

This shell function will install (if needed) and `nvm use` the specified Node version when an `.nvmrc` is found, and `nvm use default` otherwise.

Put this into your `$HOME/.zshrc` to call `nvm use` automatically whenever you enter a directory that contains an
`.nvmrc` file with a string telling nvm which node to `use`:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```zsh
# place this after nvm initialization!
autoload -U add-zsh-hook

load-nvmrc() {
  local nvmrc_path
  nvmrc_path="$(nvm_find_nvmrc)"

  if [ -n "$nvmrc_path" ]; then
    local nvmrc_node_version
    nvmrc_node_version=$(nvm version "$(cat "${nvmrc_path}")")

    if [ "$nvmrc_node_version" = "N/A" ]; then
      nvm install
    elif [ "$nvmrc_node_version" != "$(nvm version)" ]; then
      nvm use
    fi
  elif [ -n "$(PWD=$OLDPWD nvm_find_nvmrc)" ] && [ "$(nvm version)" != "$(nvm version default)" ]; then
    echo "Reverting to nvm default version"
    nvm use default
  fi
}

add-zsh-hook chpwd load-nvmrc
load-nvmrc
```

After saving the file, run `source ~/.zshrc` to reload the configuration with the latest changes made.
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
##### fish

This requires that you have [bass](https://github.com/edc/bass) installed.
```fish
# ~/.config/fish/functions/nvm.fish
function nvm
  bass source ~/.nvm/nvm.sh --no-use ';' nvm $argv
end

# ~/.config/fish/functions/nvm_find_nvmrc.fish
function nvm_find_nvmrc
  bass source ~/.nvm/nvm.sh --no-use ';' nvm_find_nvmrc
end

# ~/.config/fish/functions/load_nvm.fish
function load_nvm --on-variable="PWD"
  set -l default_node_version (nvm version default)
  set -l node_version (nvm version)
  set -l nvmrc_path (nvm_find_nvmrc)
  if test -n "$nvmrc_path"
    set -l nvmrc_node_version (nvm version (cat $nvmrc_path))
    if test "$nvmrc_node_version" = "N/A"
      nvm install (cat $nvmrc_path)
    else if test "$nvmrc_node_version" != "$node_version"
      nvm use $nvmrc_node_version
    end
  else if test "$node_version" != "$default_node_version"
    echo "Reverting to default Node version"
    nvm use default
  end
end

# ~/.config/fish/config.fish
# You must call it on initialization or listening to directory switching won't work
load_nvm > /dev/stderr
```
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
## Running Tests

Tests are written in [Urchin]. Install Urchin (and other dependencies) like so:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
    npm install

There are slow tests and fast tests. The slow tests do things like install node
and check that the right versions are used. The fast tests fake this to test
things like aliases and uninstalling. From the root of the nvm git repository,
run the fast tests like this:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
    npm run test/fast

Run the slow tests like this:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
    npm run test/slow

Run all of the tests like this:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
    npm test
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
Nota bene: Avoid running nvm while the tests are running.
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
## Environment variables

nvm exposes the following environment variables:

- `NVM_DIR` - nvm's installation directory.
- `NVM_BIN` - where node, npm, and global packages for the active version of node are installed.
- `NVM_INC` - node's include file directory (useful for building C/C++ addons for node).
- `NVM_CD_FLAGS` - used to maintain compatibility with zsh.
- `NVM_RC_VERSION` - version from .nvmrc file if being used.

Additionally, nvm modifies `PATH`, and, if present, `MANPATH` and `NODE_PATH` when changing versions.

([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
## Bash Completion

To activate, you need to source `bash_completion`:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```sh
[[ -r $NVM_DIR/bash_completion ]] && \. $NVM_DIR/bash_completion
```
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
Put the above sourcing line just below the sourcing line for nvm in your profile (`.bashrc`, `.bash_profile`).
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
### Usage
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
nvm:

> `$ nvm` <kbd>Tab</kbd>
```sh
alias               deactivate          install             list-remote         reinstall-packages  uninstall           version
cache               exec                install-latest-npm  ls                  run                 unload              version-remote
current             help                list                ls-remote           unalias             use                 which
```

nvm alias:

> `$ nvm alias` <kbd>Tab</kbd>
```sh
default      iojs         lts/*        lts/argon    lts/boron    lts/carbon   lts/dubnium  lts/erbium   node         stable       unstable
```


> `$ nvm alias my_alias` <kbd>Tab</kbd>
```sh
v10.22.0       v12.18.3      v14.8.0
v18
```

nvm use:
> `$ nvm use` <kbd>Tab</kbd>

```
my_alias        default        v10.22.0       v12.18.3      v14.8.0 v18
```

nvm uninstall:
> `$ nvm uninstall` <kbd>Tab</kbd>

```
my_alias        default        v10.22.0       v12.18.3      v14.8.0 v18
```
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
## Compatibility Issues

`nvm` will encounter some issues if you have some non-default settings set. (see [#606](https://github.com/nvm-sh/nvm/issues/606))
The following are known to cause issues:

Inside `~/.npmrc`:

```sh
prefix='some/path'
```

Environment Variables:

```sh
$NPM_CONFIG_PREFIX
$PREFIX
```

Shell settings:

```sh
set -e
```
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
## Installing nvm on Alpine Linux

In order to provide the best performance (and other optimizations), nvm will download and install pre-compiled binaries for Node (and npm) when you run `nvm install X`. The Node project compiles, tests and hosts/provides these pre-compiled binaries which are built for mainstream/traditional Linux distributions (such as Debian, Ubuntu, CentOS, RedHat et al).

Alpine Linux, unlike mainstream/traditional Linux distributions, is based on [BusyBox](https://www.busybox.net/), a very compact (~5MB) Linux distribution. BusyBox (and thus Alpine Linux) uses a different C/C++ stack to most mainstream/traditional Linux distributions - [musl](https://www.musl-libc.org/). This makes binary programs built for such mainstream/traditional incompatible with Alpine Linux, thus we cannot simply `nvm install X` on Alpine Linux and expect the downloaded binary to run correctly - you'll likely see "...does not exist" errors if you try that.

There is a `-s` flag for `nvm install` which requests nvm download Node source and compile it locally.

If installing nvm on Alpine Linux *is* still what you want or need to do, you should be able to achieve this by running the following from you Alpine Linux shell, depending on which version you are using:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
### Alpine Linux 3.13+
```sh
apk add -U curl bash ca-certificates openssl ncurses coreutils python3 make gcc g++ libgcc linux-headers grep util-linux binutils findutils
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
```
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
### Alpine Linux 3.5 - 3.12
```sh
apk add -U curl bash ca-certificates openssl ncurses coreutils python2 make gcc g++ libgcc linux-headers grep util-linux binutils findutils
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
```

_Note: Alpine 3.5 can only install NodeJS versions up to v6.9.5, Alpine 3.6 can only install versions up to v6.10.3, Alpine 3.7 installs versions up to v8.9.3, Alpine 3.8 installs versions up to v8.14.0, Alpine 3.9 installs versions up to v10.19.0, Alpine 3.10 installs versions up to v10.24.1, Alpine 3.11 installs versions up to v12.22.6, Alpine 3.12 installs versions up to v12.22.12, Alpine 3.13 & 3.14 install versions up to v14.20.0, Alpine 3.15 & 3.16 install versions up to v16.16.0 (**These are all versions on the main branch**). Alpine 3.5 - 3.12 required the package `python2` to build NodeJS, as they are older versions to build. Alpine 3.13+ requires `python3` to successfully build newer NodeJS versions, but you can use `python2` with Alpine 3.13+ if you need to build versions of node supported in Alpine 3.5 - 3.15, you just need to specify what version of NodeJS you need to install in the package install script._

The Node project has some desire but no concrete plans (due to the overheads of building, testing and support) to offer Alpine-compatible binaries.

As a potential alternative, @mhart (a Node contributor) has some [Docker images for Alpine Linux with Node and optionally, npm, pre-installed](https://github.com/mhart/alpine-node).

<a id="removal"></a>
## Uninstalling / Removal

### Manual Uninstall

To remove `nvm` manually, execute the following:

First, use `nvm unload` to remove the nvm command from your terminal session and delete the installation directory:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```sh
$ nvm_dir="${NVM_DIR:-~/.nvm}"
$ nvm unload
$ rm -rf "$nvm_dir"
```

Edit `~/.bashrc` (or other shell resource config) and remove the lines below:

```sh
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
[[ -r $NVM_DIR/bash_completion ]] && \. $NVM_DIR/bash_completion
```

## Docker For Development Environment

To make the development and testing work easier, we have a Dockerfile for development usage, which is based on Ubuntu 18.04 base image, prepared with essential and useful tools for `nvm` development, to build the docker image of the environment, run the docker command at the root of `nvm` repository:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```sh
$ docker build -t nvm-dev .
```

This will package your current nvm repository with our pre-defined development environment into a docker image named `nvm-dev`, once it's built with success, validate your image via `docker images`:

```sh
$ docker images

REPOSITORY         TAG                 IMAGE ID            CREATED             SIZE
nvm-dev            latest              9ca4c57a97d8        7 days ago          650 MB
```

If you got no error message, now you can easily involve in:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```sh
$ docker run -h nvm-dev -it nvm-dev

nvm@nvm-dev:~/.nvm$
```

Please note that it'll take about 8 minutes to build the image and the image size would be about 650MB, so it's not suitable for production usage.

For more information and documentation about docker, please refer to its official website:

  - https://www.docker.com/
  - https://docs.docker.com/

## Problems

  - If you try to install a node version and the installation fails, be sure to run `nvm cache clear` to delete cached node downloads, or you might get an error like the following:

    curl: (33) HTTP server doesn't seem to support byte ranges. Cannot resume.

  - Where's my `sudo node`? Check out [#43](https://github.com/nvm-sh/nvm/issues/43)

  - After the v0.8.6 release of node, nvm tries to install from binary packages. But in some systems, the official binary packages don't work due to incompatibility of shared libs. In such cases, use `-s` option to force install from source:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```sh
nvm install -s 0.8.6
```

  - If setting the `default` alias does not establish the node version in new shells (i.e. `nvm current` yields `system`), ensure that the system's node `PATH` is set before the `nvm.sh` source line in your shell profile (see [#658](https://github.com/nvm-sh/nvm/issues/658))

## macOS Troubleshooting

**nvm node version not found in vim shell**

If you set node version to a version other than your system node version `nvm use 6.2.1` and open vim and run `:!node -v` you should see `v6.2.1` if you see your system version `v0.12.7`. You need to run:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```shell
sudo chmod ugo-x /usr/libexec/path_helper
```

More on this issue in [dotphiles/dotzsh](https://github.com/dotphiles/dotzsh#mac-os-x).
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
**nvm is not compatible with the npm config "prefix" option**

Some solutions for this issue can be found [here](https://github.com/nvm-sh/nvm/issues/1245)

There is one more edge case causing this issue, and that's a **mismatch between the `$HOME` path and the user's home directory's actual name**.

You have to make sure that the user directory name in `$HOME` and the user directory name you'd see from running `ls /Users/` **are capitalized the same way** ([See this issue](https://github.com/nvm-sh/nvm/issues/2261)).
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
To change the user directory and/or account name follow the instructions [here](https://support.apple.com/en-us/HT201548)

[1]: https://github.com/nvm-sh/nvm.git
[2]: https://github.com/nvm-sh/nvm/blob/v0.40.3/install.sh
[3]: https://app.travis-ci.com/nvm-sh/nvm
[4]: https://github.com/nvm-sh/nvm/releases/tag/v0.40.3
[Urchin]: https://git.sdf.org/tlevine/urchin
[Fish]: https://fishshell.com

**Homebrew makes zsh directories unsecure**
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```shell
zsh compinit: insecure directories, run compaudit for list.
Ignore insecure directories and continue [y] or abort compinit [n]? y
```

Homebrew causes insecure directories like `/usr/local/share/zsh/site-functions` and `/usr/local/share/zsh`. This is **not** an `nvm` problem - it is a homebrew problem. Refer [here](https://github.com/zsh-users/zsh-completions/issues/680) for some solutions related to the issue.

**Macs with Apple Silicon chips**

Experimental support for the Apple Silicon chip architecture was added in node.js v15.3 and full support was added in v16.0.
Because of this, if you try to install older versions of node as usual, you will probably experience either compilation errors when installing node or out-of-memory errors while running your code.

So, if you want to run a version prior to v16.0 on an Apple Silicon Mac, it may be best to compile node targeting the `x86_64` Intel architecture so that Rosetta 2 can translate the `x86_64` processor instructions to ARM-based Apple Silicon instructions.
Here's what you will need to do:

- Install Rosetta, if you haven't already done so
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
  ```sh
  $ softwareupdate --install-rosetta
  ```

  You might wonder, "how will my Apple Silicon Mac know to use Rosetta for a version of node compiled for an Intel chip?".
  If an executable contains only Intel instructions, macOS will automatically use Rosetta to translate the instructions.

- Open a shell that's running using Rosetta
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
  ```sh
  $ arch -x86_64 zsh
  ```

  Note: This same thing can also be accomplished by finding the Terminal or iTerm App in Finder, right clicking, selecting "Get Info", and then checking the box labeled "Open using Rosetta".

  Note: This terminal session is now running in `zsh`.
  If `zsh` is not the shell you typically use, `nvm` may not be `source`'d automatically like it probably is for your usual shell through your dotfiles.
  If that's the case, make sure to source `nvm`.
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
  ```sh
  $ source "${NVM_DIR}/nvm.sh"
  ```

- Install whatever older version of node you are interested in. Let's use 20 or 22 as an example.
  This will fetch the node source code and compile it, which will take several minutes.
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
  ```sh
  $ nvm install v20 or 22 --shared-zlib
  ```

  Note: You're probably curious why `--shared-zlib` is included.
  There's a bug in recent versions of Apple's system `clang` compiler.
  If one of these broken versions is installed on your system, the above step will likely still succeed even if you didn't include the `--shared-zlib` flag.
  However, later, when you attempt to `npm install` something using your old version of node.js, you will see `incorrect data check` errors.
  If you want to avoid the possible hassle of dealing with this, include that flag.
  For more details, see [this issue](https://github.com/nodejs/node/issues/39313) and [this comment](https://github.com/nodejs/node/issues/39313#issuecomment-90.40.376)

- Exit back to your native shell.
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
  ```sh
  $ exit
  $ arch
  arm64
  ```

  Note: If you selected the box labeled "Open using Rosetta" rather than running the CLI command in the second step, you will see `i386` here.
  Unless you have another reason to have that box selected, you can deselect it now.

- Check to make sure the architecture is correct. `x64` is the abbreviation for `x86_64`, which is what you want to see.
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
  ```sh
  $ node -p process.arch
  x64
  ```

Now you should be able to use node as usual.

## WSL Troubleshooting

If you've encountered this error on WSL-2:

  ```sh
  curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                  Dload  Upload  Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:--  0:00:09 --:--:--     0curl: (6) Could not resolve host: raw.githubusercontent.com
  ```

It may be due to your antivirus, VPN, or other reasons.

Where you can `ping 8.8.8.8` while you can't `ping google.com`


This could simply be solved by running this in your root directory:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
  ```sh
  sudo rm /etc/resolv.conf
  sudo bash -c 'echo "nameserver 8.8.8.8" > /etc/resolv.conf'
  sudo bash -c 'echo "[network]" > /etc/wsl.conf'
  sudo bash -c 'echo "generateResolvConf = false" >> /etc/wsl.conf'
  sudo chattr +i /etc/resolv.conf
  ```

This deletes your `resolv.conf` file that is automatically generated when you run WSL, creates a new file and puts `nameserver 8.8.8.8`, then creates a `wsl.conf` file and adds `[network]` and `generateResolveConf = false` to prevent auto-generation of that file.

You can check the contents of the file by running:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
  ```sh
  cat /etc/resolv.conf
  ```

## Maintainers

Currently, the sole maintainer is [@ljharb](https://github.com/ljharb) - more maintainers are quite welcome, and we hope to add folks to the team over time. [Governance](./GOVERNANCE.md) will be re-evaluated as the project evolves.

## Project Support

Only the latest version (v0.40.3 at this time) is supported.

## Enterprise Support

If you are unable to update to the latest version of `nvm`, our [partners](https://openjsf.org/ecosystem-sustainability-program) provide commercial security fixes for all unsupported versions:

  - [HeroDevs Never-Ending Support](https://www.herodevs.com/support?utm_source=OpenJS&utm_medium=Link&utm_campaign=nvm_openjs)

## License

See [LICENSE.md](./LICENSE.md).

## Copyright notice

Copyright [OpenJS Foundation](https://openjsf.org) and `nvm` contributors. All rights reserved. The [OpenJS Foundation](https://openjsf.org) has registered trademarks and uses trademarks.  For a list of trademarks of the [OpenJS Foundation](https://openjsf.org), please see our [Trademark Policy](https://trademark-policy.openjsf.org/) and [Trademark List](https://trademark-list.openjsf.org/).  Trademarks and logos not indicated on the [list of OpenJS Foundation trademarks](https://trademark-list.openjsf.org) are trademarks™ or registered® trademarks of their respective holders. Use of them does not imply any affiliation with or endorsement by them.
[The OpenJS Foundation](https://openjsf.org/) | [Terms of Use](https://terms-of-use.openjsf.org/) | [Privacy Policy](https://privacy-policy.openjsf.org/) | [Bylaws](https://bylaws.openjsf.org/) | [Code of Conduct](https://code-of-conduct.openjsf.org) | [Trademark Policy](https://trademark-policy.openjsf.org/) | [Trademark List](https://trademark-list.openjsf.org/) | [Cookie Policy](https://www.linuxfoundation.org/cookies/)
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
#!/usr/bin/env bash

{ # this ensures the entire script is downloaded #

nvm_has() {
  type "$1" > /dev/null 2>&1
}

nvm_echo() {
  command printf %s\\n "$*" 2>/dev/null
}

if [ -z "${BASH_VERSION}" ] || [ -n "${ZSH_VERSION}" ]; then
  # shellcheck disable=SC2016
  nvm_echo >&2 'Error: the install instructions explicitly say to pipe the install script to `bash`; please follow them'
  exit 1
fi

nvm_grep() {
  GREP_OPTIONS='' command grep "$@"
}

nvm_default_install_dir() {
  [ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm"
}

nvm_install_dir() {
  if [ -n "$NVM_DIR" ]; then
    printf %s "${NVM_DIR}"
  else
    nvm_default_install_dir
  fi
}

nvm_latest_version() {
  nvm_echo "v0.40.3"
}

nvm_profile_is_bash_or_zsh() {
  local TEST_PROFILE
  TEST_PROFILE="${1-}"
  case "${TEST_PROFILE-}" in
    *"/.bashrc" | *"/.bash_profile" | *"/.zshrc" | *"/.zprofile")
      return
    ;;
    *)
      return 1
    ;;
  esac
}

#
# Outputs the location to NVM depending on:
# * The availability of $NVM_SOURCE
# * The presence of $NVM_INSTALL_GITHUB_REPO
# * The method used ("script" or "git" in the script, defaults to "git")
# NVM_SOURCE always takes precedence unless the method is "script-nvm-exec"
#
nvm_source() {
  local NVM_GITHUB_REPO
  NVM_GITHUB_REPO="${NVM_INSTALL_GITHUB_REPO:-nvm-sh/nvm}"
  if [ "${NVM_GITHUB_REPO}" != 'nvm-sh/nvm' ]; then
    { nvm_echo >&2 "$(cat)" ; } << EOF
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE REPO IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!

The default repository for this install is \`nvm-sh/nvm\`,
but the environment variables \`\$NVM_INSTALL_GITHUB_REPO\` is
currently set to \`${NVM_GITHUB_REPO}\`.

If this is not intentional, interrupt this installation and
verify your environment variables.
EOF
  fi
  local NVM_VERSION
  NVM_VERSION="${NVM_INSTALL_VERSION:-$(nvm_latest_version)}"
  local NVM_METHOD
  NVM_METHOD="$1"
  local NVM_SOURCE_URL
  NVM_SOURCE_URL="$NVM_SOURCE"
  if [ "_$NVM_METHOD" = "_script-nvm-exec" ]; then
    NVM_SOURCE_URL="https://raw.githubusercontent.com/${NVM_GITHUB_REPO}/${NVM_VERSION}/nvm-exec"
  elif [ "_$NVM_METHOD" = "_script-nvm-bash-completion" ]; then
    NVM_SOURCE_URL="https://raw.githubusercontent.com/${NVM_GITHUB_REPO}/${NVM_VERSION}/bash_completion"
  elif [ -z "$NVM_SOURCE_URL" ]; then
    if [ "_$NVM_METHOD" = "_script" ]; then
      NVM_SOURCE_URL="https://raw.githubusercontent.com/${NVM_GITHUB_REPO}/${NVM_VERSION}/nvm.sh"
    elif [ "_$NVM_METHOD" = "_git" ] || [ -z "$NVM_METHOD" ]; then
      NVM_SOURCE_URL="https://github.com/${NVM_GITHUB_REPO}.git"
    else
      nvm_echo >&2 "Unexpected value \"$NVM_METHOD\" for \$NVM_METHOD"
      return 1
    fi
  fi
  nvm_echo "$NVM_SOURCE_URL"
}

#
# Node.js version to install
#
nvm_node_version() {
  nvm_echo "$NODE_VERSION"
}

nvm_download() {
  if nvm_has "curl"; then
    curl --fail --compressed -q "$@"
  elif nvm_has "wget"; then
    # Emulate curl with wget
    ARGS=$(nvm_echo "$@" | command sed -e 's/--progress-bar /--progress=bar /' \
                            -e 's/--compressed //' \
                            -e 's/--fail //' \
                            -e 's/-L //' \
                            -e 's/-I /--server-response /' \
                            -e 's/-s /-q /' \
                            -e 's/-sS /-nv /' \
                            -e 's/-o /-O /' \
                            -e 's/-C - /-c /')
    # shellcheck disable=SC2086
    eval wget $ARGS
  fi
}

install_nvm_from_git() {
  local INSTALL_DIR
  INSTALL_DIR="$(nvm_install_dir)"
  local NVM_VERSION
  NVM_VERSION="${NVM_INSTALL_VERSION:-$(nvm_latest_version)}"
  if [ -n "${NVM_INSTALL_VERSION:-}" ]; then
    # Check if version is an existing ref
    if command git ls-remote "$(nvm_source "git")" "$NVM_VERSION" | nvm_grep -q "$NVM_VERSION" ; then
      :
    # Check if version is an existing changeset
    elif ! nvm_download -o /dev/null "$(nvm_source "script-nvm-exec")"; then
      nvm_echo >&2 "Failed to find '$NVM_VERSION' version."
      exit 1
    fi
  fi

  local fetch_error
  if [ -d "$INSTALL_DIR/.git" ]; then
    # Updating repo
    nvm_echo "=> nvm is already installed in $INSTALL_DIR, trying to update using git"
    command printf '\r=> '
    fetch_error="Failed to update nvm with $NVM_VERSION, run 'git fetch' in $INSTALL_DIR yourself."
  else
    fetch_error="Failed to fetch origin with $NVM_VERSION. Please report this!"
    nvm_echo "=> Downloading nvm from git to '$INSTALL_DIR'"
    command printf '\r=> '
    mkdir -p "${INSTALL_DIR}"
    if [ "$(ls -A "${INSTALL_DIR}")" ]; then
      # Initializing repo
      command git init "${INSTALL_DIR}" || {
        nvm_echo >&2 'Failed to initialize nvm repo. Please report this!'
        exit 2
      }
      command git --git-dir="${INSTALL_DIR}/.git" remote add origin "$(nvm_source)" 2> /dev/null \
        || command git --git-dir="${INSTALL_DIR}/.git" remote set-url origin "$(nvm_source)" || {
        nvm_echo >&2 'Failed to add remote "origin" (or set the URL). Please report this!'
        exit 2
      }
    else
      # Cloning repo
      command git clone "$(nvm_source)" --depth=1 "${INSTALL_DIR}" || {
        nvm_echo >&2 'Failed to clone nvm repo. Please report this!'
        exit 2
      }
    fi
  fi
  # Try to fetch tag
  if command git --git-dir="$INSTALL_DIR"/.git --work-tree="$INSTALL_DIR" fetch origin tag "$NVM_VERSION" --depth=1 2>/dev/null; then
    :
  # Fetch given version
  elif ! command git --git-dir="$INSTALL_DIR"/.git --work-tree="$INSTALL_DIR" fetch origin "$NVM_VERSION" --depth=1; then
    nvm_echo >&2 "$fetch_error"
    exit 1
  fi
  command git -c advice.detachedHead=false --git-dir="$INSTALL_DIR"/.git --work-tree="$INSTALL_DIR" checkout -f --quiet FETCH_HEAD || {
    nvm_echo >&2 "Failed to checkout the given version $NVM_VERSION. Please report this!"
    exit 2
  }
  if [ -n "$(command git --git-dir="$INSTALL_DIR"/.git --work-tree="$INSTALL_DIR" show-ref refs/heads/master)" ]; then
    if command git --no-pager --git-dir="$INSTALL_DIR"/.git --work-tree="$INSTALL_DIR" branch --quiet 2>/dev/null; then
      command git --no-pager --git-dir="$INSTALL_DIR"/.git --work-tree="$INSTALL_DIR" branch --quiet -D master >/dev/null 2>&1
    else
      nvm_echo >&2 "Your version of git is out of date. Please update it!"
      command git --no-pager --git-dir="$INSTALL_DIR"/.git --work-tree="$INSTALL_DIR" branch -D master >/dev/null 2>&1
    fi
  fi

  nvm_echo "=> Compressing and cleaning up git repository"
  if ! command git --git-dir="$INSTALL_DIR"/.git --work-tree="$INSTALL_DIR" reflog expire --expire=now --all; then
    nvm_echo >&2 "Your version of git is out of date. Please update it!"
  fi
  if ! command git --git-dir="$INSTALL_DIR"/.git --work-tree="$INSTALL_DIR" gc --auto --aggressive --prune=now ; then
    nvm_echo >&2 "Your version of git is out of date. Please update it!"
  fi
  return
}

#([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
# Automatically install Node.js
#
nvm_install_node() {
  local NODE_VERSION_LOCAL
  NODE_VERSION_LOCAL="$(nvm_node_version)"

  if [ -z "$NODE_VERSION_LOCAL" ]; then
    return 0
  fi

  nvm_echo "=> Installing Node.js version $NODE_VERSION_LOCAL"
  nvm install "$NODE_VERSION_LOCAL"
  local CURRENT_NVM_NODE

  CURRENT_NVM_NODE="$(nvm_version current)"
  if [ "$(nvm_version "$NODE_VERSION_LOCAL")" == "$CURRENT_NVM_NODE" ]; then
    nvm_echo "=> Node.js version $NODE_VERSION_LOCAL has been successfully installed"
  else
    nvm_echo >&2 "Failed to install Node.js $NODE_VERSION_LOCAL"
  fi
}

install_nvm_as_script() {
  local INSTALL_DIR
  INSTALL_DIR="$(nvm_install_dir)"
  local NVM_SOURCE_LOCAL
  NVM_SOURCE_LOCAL="$(nvm_source script)"
  local NVM_EXEC_SOURCE
  NVM_EXEC_SOURCE="$(nvm_source script-nvm-exec)"
  local NVM_BASH_COMPLETION_SOURCE
  NVM_BASH_COMPLETION_SOURCE="$(nvm_source script-nvm-bash-completion)"
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
  # Downloading to $INSTALL_DIR
  mkdir -p "$INSTALL_DIR"
  if [ -f "$INSTALL_DIR/nvm.sh" ]; then
    nvm_echo "=> nvm is already installed in $INSTALL_DIR, trying to update the script"
  else
    nvm_echo "=> Downloading nvm as script to '$INSTALL_DIR'"
  fi
  nvm_download -s "$NVM_SOURCE_LOCAL" -o "$INSTALL_DIR/nvm.sh" || {
    nvm_echo >&2 "Failed to download '$NVM_SOURCE_LOCAL'"
    return 1
  } &
  nvm_download -s "$NVM_EXEC_SOURCE" -o "$INSTALL_DIR/nvm-exec" || {
    nvm_echo >&2 "Failed to download '$NVM_EXEC_SOURCE'"
    return 2
  } &
  nvm_download -s "$NVM_BASH_COMPLETION_SOURCE" -o "$INSTALL_DIR/bash_completion" || {
    nvm_echo >&2 "Failed to download '$NVM_BASH_COMPLETION_SOURCE'"
    return 2
  } &
  for job in $(jobs -p | command sort)
  do
    wait "$job" || return $?
  done
  chmod a+x "$INSTALL_DIR/nvm-exec" || {
    nvm_echo >&2 "Failed to mark '$INSTALL_DIR/nvm-exec' as executable"
    return 3
  }
}

nvm_try_profile() {
  if [ -z "${1-}" ] || [ ! -f "${1}" ]; then
    return 1
  fi
  nvm_echo "${1}"
}

#
# Detect profile file if not specified as environment variable
# (eg: PROFILE=~/.myprofile)
# The echo'ed path is guaranteed to be an existing file
# Otherwise, an empty string is returned
#
nvm_detect_profile() {
  if [ "${PROFILE-}" = '/dev/null' ]; then
    # the user has specifically requested NOT to have nvm touch their profile
    return
  fi

  if [ -n "${PROFILE}" ] && [ -f "${PROFILE}" ]; then
    nvm_echo "${PROFILE}"
    return
  fi

  local DETECTED_PROFILE
  DETECTED_PROFILE=''

  if [ "${SHELL#*bash}" != "$SHELL" ]; then
    if [ -f "$HOME/.bashrc" ]; then
      DETECTED_PROFILE="$HOME/.bashrc"
    elif [ -f "$HOME/.bash_profile" ]; then
      DETECTED_PROFILE="$HOME/.bash_profile"
    fi
  elif [ "${SHELL#*zsh}" != "$SHELL" ]; then
    if [ -f "${ZDOTDIR:-${HOME}}/.zshrc" ]; then
      DETECTED_PROFILE="${ZDOTDIR:-${HOME}}/.zshrc"
    elif [ -f "${ZDOTDIR:-${HOME}}/.zprofile" ]; then
      DETECTED_PROFILE="${ZDOTDIR:-${HOME}}/.zprofile"
    fi
  fi

  if [ -z "$DETECTED_PROFILE" ]; then
    for EACH_PROFILE in ".profile" ".bashrc" ".bash_profile" ".zprofile" ".zshrc"
    do
      if DETECTED_PROFILE="$(nvm_try_profile "${ZDOTDIR:-${HOME}}/${EACH_PROFILE}")"; then
        break
      fi
    done
  fi

  if [ -n "$DETECTED_PROFILE" ]; then
    nvm_echo "$DETECTED_PROFILE"
  fi
}

#
# Check whether the user has any globally-installed npm modules in their system
# Node, and warn them if so.
#
nvm_check_global_modules() {
  local NPM_COMMAND
  NPM_COMMAND="$(command -v npm 2>/dev/null)" || return 0
  [ -n "${NVM_DIR}" ] && [ -z "${NPM_COMMAND%%"$NVM_DIR"/*}" ] && return 0

  local NPM_VERSION
  NPM_VERSION="$(npm --version)"
  NPM_VERSION="${NPM_VERSION:--1}"
  [ "${NPM_VERSION%%[!-0-9]*}" -gt 0 ] || return 0

  local NPM_GLOBAL_MODULES
  NPM_GLOBAL_MODULES="$(
    npm list -g --depth=0 |
    command sed -e '/ npm@/d' -e '/ (empty)$/d'
  )"

  local MODULE_COUNT
  MODULE_COUNT="$(
    command printf %s\\n "$NPM_GLOBAL_MODULES" |
    command sed -ne '1!p' |                     # Remove the first line
    wc -l | command tr -d ' '                   # Count entries
  )"

  if [ "${MODULE_COUNT}" != '0' ]; then
    # shellcheck disable=SC2016
    nvm_echo '=> You currently have modules installed globally with `npm`. These will no'
    # shellcheck disable=SC2016
    nvm_echo '=> longer be linked to the active version of Node when you install a new node'
    # shellcheck disable=SC2016
    nvm_echo '=> with `nvm`; and they may (depending on how you construct your `$PATH`)'
    # shellcheck disable=SC2016
    nvm_echo '=> override the binaries of modules installed with `nvm`:'
    nvm_echo

    command printf %s\\n "$NPM_GLOBAL_MODULES"
    nvm_echo '=> If you wish to uninstall them at a later point (or re-install them under your'
    # shellcheck disable=SC2016
    nvm_echo '=> `nvm` node installs), you can remove them from the system Node as follows:'
    nvm_echo
    nvm_echo '     $ nvm use system'
    nvm_echo '     $ npm uninstall -g a_module'
    nvm_echo
  fi
}

nvm_do_install() {
  if [ -n "${NVM_DIR-}" ] && ! [ -d "${NVM_DIR}" ]; then
    if [ -e "${NVM_DIR}" ]; then
      nvm_echo >&2 "File \"${NVM_DIR}\" has the same name as installation directory."
      exit 1
    fi

    if [ "${NVM_DIR}" = "$(nvm_default_install_dir)" ]; then
      mkdir "${NVM_DIR}"
    else
      nvm_echo >&2 "You have \$NVM_DIR set to \"${NVM_DIR}\", but that directory does not exist. Check your profile files and environment."
      exit 1
    fi
  fi
  # Disable the optional which check, https://www.shellcheck.net/wiki/SC2230
  # shellcheck disable=SC2230
  if nvm_has xcode-select && [ "$(xcode-select -p >/dev/null 2>/dev/null ; echo $?)" = '2' ] && [ "$(which git)" = '/usr/bin/git' ] && [ "$(which curl)" = '/usr/bin/curl' ]; then
    nvm_echo >&2 'You may be on a Mac, and need to install the Xcode Command Line Developer Tools.'
    # shellcheck disable=SC2016
    nvm_echo >&2 'If so, run `xcode-select --install` and try again. If not, please report this!'
    exit 1
  fi
  if [ -z "${METHOD}" ]; then
    # Autodetect install method
    if nvm_has git; then
      install_nvm_from_git
    elif nvm_has curl || nvm_has wget; then
      install_nvm_as_script
    else
      nvm_echo >&2 'You need git, curl, or wget to install nvm'
      exit 1
    fi
  elif [ "${METHOD}" = 'git' ]; then
    if ! nvm_has git; then
      nvm_echo >&2 "You need git to install nvm"
      exit 1
    fi
    install_nvm_from_git
  elif [ "${METHOD}" = 'script' ]; then
    if ! nvm_has curl && ! nvm_has wget; then
      nvm_echo >&2 "You need curl or wget to install nvm"
      exit 1
    fi
    install_nvm_as_script
  else
    nvm_echo >&2 "The environment variable \$METHOD is set to \"${METHOD}\", which is not recognized as a valid installation method."
    exit 1
  fi

  nvm_echo

  local NVM_PROFILE
  NVM_PROFILE="$(nvm_detect_profile)"
  local PROFILE_INSTALL_DIR
  PROFILE_INSTALL_DIR="$(nvm_install_dir | command sed "s:^$HOME:\$HOME:")"

  SOURCE_STR="\\nexport NVM_DIR=\"${PROFILE_INSTALL_DIR}\"\\n[ -s \"\$NVM_DIR/nvm.sh\" ] && \\. \"\$NVM_DIR/nvm.sh\"  # This loads nvm\\n"

  # shellcheck disable=SC2016
  COMPLETION_STR='[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion\n'
  BASH_OR_ZSH=false

  if [ -z "${NVM_PROFILE-}" ] ; then
    local TRIED_PROFILE
    if [ -n "${PROFILE}" ]; then
      TRIED_PROFILE="${NVM_PROFILE} (as defined in \$PROFILE), "
    fi
    nvm_echo "=> Profile not found. Tried ${TRIED_PROFILE-}~/.bashrc, ~/.bash_profile, ~/.zprofile, ~/.zshrc, and ~/.profile."
    nvm_echo "=> Create one of them and run this script again"
    nvm_echo "   OR"
    nvm_echo "=> Append the following lines to the correct file yourself:"
    command printf "${SOURCE_STR}"
    nvm_echo
  else
    if nvm_profile_is_bash_or_zsh "${NVM_PROFILE-}"; then
      BASH_OR_ZSH=true
    fi
    if ! command grep -qc '/nvm.sh' "$NVM_PROFILE"; then
      nvm_echo "=> Appending nvm source string to $NVM_PROFILE"
      command printf "${SOURCE_STR}" >> "$NVM_PROFILE"
    else
      nvm_echo "=> nvm source string already in ${NVM_PROFILE}"
    fi
    # shellcheck disable=SC2016
    if ${BASH_OR_ZSH} && ! command grep -qc '$NVM_DIR/bash_completion' "$NVM_PROFILE"; then
      nvm_echo "=> Appending bash_completion source string to $NVM_PROFILE"
      command printf "$COMPLETION_STR" >> "$NVM_PROFILE"
    else
      nvm_echo "=> bash_completion source string already in ${NVM_PROFILE}"
    fi
  fi
  if ${BASH_OR_ZSH} && [ -z "${NVM_PROFILE-}" ] ; then
    nvm_echo "=> Please also append the following lines to the if you are using bash/zsh shell:"
    command printf "${COMPLETION_STR}"
  fi

  # Source nvm
  # shellcheck source=/dev/null
  \. "$(nvm_install_dir)/nvm.sh"

  nvm_check_global_modules

  nvm_install_node

  nvm_reset

  nvm_echo "=> Close and reopen your terminal to start using nvm or run the following to use it now:"
  command printf "${SOURCE_STR}"
  if ${BASH_OR_ZSH} ; then
    command printf "${COMPLETION_STR}"
  fi
}

#
# Unsets the various functions defined
# during the execution of the install script
#
nvm_reset() {
  unset -f nvm_has nvm_install_dir nvm_latest_version nvm_profile_is_bash_or_zsh \
    nvm_source nvm_node_version nvm_download install_nvm_from_git nvm_install_node \
    install_nvm_as_script nvm_try_profile nvm_detect_profile nvm_check_global_modules \
    nvm_do_install nvm_reset nvm_default_install_dir nvm_grep
}

[ "_$NVM_ENV" = "_testing" ] || nvm_do_install

} # this ensures the entire script is downloaded #

([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")# Contributing to Angular
nvm install 20.10.0
<docs-decorative-header title="What is Angular?" imgSrc="adev/src/assets/images/what_is_angular.svg"> <!-- markdownlint-disable-line -->
</docs-decorative-header>

<big style="margin-top: 2em">
Angular is a web framework that empowers developers to build fast, reliable applications.
</big>

Maintained by a dedicated team at Google, Angular provides a broad suite of tools, APIs, and
libraries to simplify and streamline your development workflow. Angular gives you
a solid platform on which to build fast, reliable applications that scale with both the size of
your team and the size of your codebase.

**Want to see some code?** Jump over to our [Essentials](essentials) for a quick overview of
what it's like to use Angular, or get started in the [Tutorial](tutorials/learn-angular) if you
prefer following step-by-step instructions.

## Features that power your development
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
<docs-card-container>
  <docs-card title="Keep your codebase organized with an opinionated component model and flexible dependency injection
system" href="guide/components" link="Get started with Components">
  Angular components make it easy to split your code into well-encapsulated parts.

  The versatile dependency injection helps you keep your code modular, loosely-coupled, and
  testable.
  </docs-card>
  <docs-card title="Get fast state updates with fine-grained reactivity based on Signals" href="guide/signals" link="Explore Angular Signals">
  Our fine-grained reactivity model, combined with compile-time optimizations, simplifies development and helps build faster apps by default.

  Granularly track how and where state is used throughout an application, giving the framework the power to render fast updates via highly optimized instructions.
  </docs-card>
  <docs-card title="Meet your performance targets with SSR, SSG, hydration, and next-generation deferred loading" href="guide/ssr" link="Read about SSR">
    Angular supports both server-side rendering (SSR) and static site generation (SSG) along
    with full DOM hydration. `@defer` blocks in templates make it simple to declaratively divide
    your templates into lazy-loadable parts.
  </docs-card>
  <docs-card title="Guarantee everything works together with Angular's first-party modules for forms, routing, and
more">
  [Angular's router](guide/routing) provides a feature-rich navigation toolkit, including support
  for route guards, data resolution, lazy-loading, and much more.

  [Angular's forms module](guide/forms) provides a standardized system for form participation and validation.
  </docs-card>
</docs-card-container>
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
## Develop applications faster than ever
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
<docs-card-container>
  <docs-card title="Effortlessly build, serve, test, deploy with Angular CLI" href="tools/cli" link="Angular CLI">
  Angular CLI gets your project running in under a minute with the commands you need to
  grow into a deployed production application.
  </docs-card>
  <docs-card title="Visually debug, analyze, and optimize your code with the Angular DevTools browser extension" href="tools/devtools" link="Angular DevTools">
  Angular DevTools sits alongside your browser's developer tools. It helps debug and analyze your
  app, including a component tree inspector, dependency injection tree view,
  and custom performance profiling flame chart.
  </docs-card>
  <docs-card title="Never miss a version with ng update" href="cli/update" link="ng update">
  Angular CLI's `ng update` runs automated code transformations that automatically handle routine
  breaking changes, dramatically simplifying major version updates. Keeping up with the latest
  version keeps your app as fast and secure as possible.
  </docs-card>
  <docs-card title="Stay productive with IDE integration in your favorite editor" href="tools/language-service" link="Language service">
  Angular's IDE language services powers code completion, navigation, refactoring, and real-time
  diagnostics in your favorite editor.
  </docs-card>
</docs-card-container>
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
## Ship with confidence
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
<docs-card-container>
  <docs-card title="Verified commit-by-commit against Google's colossal monorepo" href="https://cacm.acm.org/magazines/2016/7/204032-why-google-stores-billions-of-lines-of-code-in-a-single-repository/fulltext" link="Learn about Google's monorepo">
  Every Angular commit is checked against _hundreds of thousands_ of tests in Google's internal code
  repository, representing countless real-world scenarios.
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
  Angular is committed to stability for some of Google’s largest products, including Google Cloud.
  This commitment ensures changes are well-tested, backwards compatible, and include migration tools
  whenever possible.
  </docs-card>
  <docs-card title="Clear support policies and predictable release schedule" href="reference/releases" link="Versioning & releasing">
  Angular's predictable, time-based release schedule gives your organization confidence in the
  stability and backwards compatibility of the framework. Long Term Support (LTS) windows make sure
  you get critical security fixes when you need them. First-party update tools, guides and automated
  migration schematics help keep your apps up-to-date with the latest advancements to the framework
  and the web platform.
  </docs-card>
</docs-card-container>
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
## Works at any scale
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
<docs-card-container>
  <docs-card title="Reach users everywhere with internationalization support" href="guide/i18n" link="Internationalization">
  Angular's internationalization features handle message translations and formatting, including
  support for unicode standard ICU syntax.
  </docs-card>
  <docs-card title="Protect your users with security by default" href="best-practices/security" link="Security">
  In collaboration with Google's world-class security engineers, Angular aims to make development
  safe by default. Built-in security features, including HTML sanitization and
  trusted type support, help protect your users from common vulnerabilities like
  cross-site scripting and cross-site request forgery.
  </docs-card>
  <docs-card title="Keep large teams productive with Vite and esbuild" href="tools/cli/build-system-migration" link="ESBuild and Vite">
  Angular CLI includes a fast, modern build pipeline using Vite and ESBuild. Developers report
  building projects with hundreds of thousands of lines of code in less than a minute.
  </docs-card>
  <docs-card title="Proven in some of Google's largest web apps">
  Large Google products build on top of Angular's architecture and help develop new features that
  further improve Angular's scalability, from [Google Fonts](https://fonts.google.com/) to [Google Cloud](https://console.cloud.google.com).
  </docs-card>
</docs-card-container>
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
## Open-source first
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
<docs-card-container>
  <docs-card title="Made in the open on GitHub" href="https://github.com/angular/angular" link="Star our GitHub">
  Curious what we’re working on? Every PR and commit is available on our GitHub. Run into an issue or bug? We triage GitHub issues regularly to ensure we’re responsive and engaged with our community, and solving the real world problems you’re facing.
  </docs-card>
  <docs-card title="Built with transparency" href="roadmap" link="Read our public roadmap">
  Our team publishes a public roadmap of our current and future work and values your feedback. We publish Request for Comments (RFCs) to collect feedback on larger feature changes and ensure the community voice is heard while shaping the future direction of Angular.
  </docs-card>
</docs-card-container>
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
## A thriving community

<docs-card-container>
  <docs-card title="Courses, blogs and resources" href="https://devlibrary.withgoogle.com/products/angular?sort=added" link="Check out DevLibrary">
  Our community is composed of talented developers, writers, instructors, podcasters, and more. The Google for Developers library is just a sample of the high quality resources available for new and experienced developers to continue developing.
  </docs-card>
  <docs-card title="Open Source" href="https://github.com/angular/angular/blob/main/CONTRIBUTING.md" link="Contribute to Angular">
  We are thankful for the open source contributors who make Angular a better framework for everyone. From fixing a typo in the docs, to adding major features, we encourage anyone interested to get started on our GitHub.
  </docs-card>
  <docs-card title="Community partnerships" href="https://developers.google.com/community/experts/directory?specialization=angular" link="Meet the Angular GDEs">
  Our team partners with individuals, educators, and enterprises to ensure we consistently are supporting developers. Angular Google Developer Experts (GDEs) represent community leaders around the world educating, organizing, and developing with Angular. Enterprise partnerships help ensure that Angular scales well for technology industry leaders.
  </docs-card>
  <docs-card title="Partnering with other Google technologies">
  Angular partners closely with other Google technologies and teams to improve the web.

  Our ongoing partnership with Chrome’s Aurora actively explores improvements to user experience across the web, developing built-in performance optimizations like NgOptimizedImage and improvements to Angular’s Core Web Vitals.

  We are also working with [Firebase](https://firebase.google.com/), [Tensorflow](https://www.tensorflow.org/), [Flutter](https://flutter.dev/), [Material Design](https://m3.material.io/), and [Google Cloud](https://cloud.google.com/) to ensure we provide meaningful integrations across the developer workflow.
  </docs-card>
</docs-card-container>

<docs-callout title="Join the momentum!">
  <docs-pill-row>
    <docs-pill href="roadmap" title="Read Angular's roadmap"/>
    <docs-pill href="playground" title="Try out our playground"/>
    <docs-pill href="tutorials" title="Learn with tutorials"/>
    <docs-pill href="https://youtube.com/playlist?list=PL1w1q3fL4pmj9k1FrJ3Pe91EPub2_h4jF" title="Watch our YouTube course"/>
    <docs-pill href="api" title="Reference our APIs"/>
  </docs-pill-row>
</docs-callout>


We would love for you to contribute to Angular and help make it even better than it is today!
As a contributor, here are the guidelines we would like you to follow:

 - [Code of Conduct](#coc)
 - [Question or Problem?](#question)
 - [Issues and Bugs](#issue)
 - [Feature Requests](#feature)
 - [Submission Guidelines](#submit)
 - [Coding Rules](#rules)
 - [Commit Message Guidelines](#commit)
 - [Signing the CLA](#cla)

([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
## <a name="coc"></a> Code of Conduct

Help us keep Angular open and inclusive.
Please read and follow our [Code of Conduct][coc].


## <a name="question"></a> Got a Question or Problem?

Do not open issues for general support questions as we want to keep GitHub issues for bug reports and feature requests.
Instead, we recommend using [Stack Overflow](https://stackoverflow.com/questions/tagged/angular) to ask support-related questions. When creating a new question on Stack Overflow, make sure to add the `angular` tag.

Stack Overflow is a much better place to ask questions since:

- there are thousands of people willing to help on Stack Overflow
- questions and answers stay available for public viewing so your question/answer might help someone else
- Stack Overflow's voting system assures that the best answers are prominently visible.

To save your and our time, we will systematically close all issues that are requests for general support and redirect people to Stack Overflow.

If you would like to chat about the question in real-time, you can reach out via [the Angular community Discord server][discord].


## <a name="issue"></a> Found a Bug?

If you find a bug in the source code, you can help us by [submitting an issue](#submit-issue) to our [GitHub Repository][github].
Even better, you can [submit a Pull Request](#submit-pr) with a fix.


## <a name="feature"></a> Missing a Feature?
You can *request* a new feature by [submitting an issue](#submit-issue) to our GitHub Repository.
If you would like to *implement* a new feature, please consider the size of the change in order to determine the right steps to proceed:

* For a **Major Feature**, first open an issue and outline your proposal so that it can be discussed.
  This process allows us to better coordinate our efforts, prevent duplication of work, and help you to craft the change so that it is successfully accepted into the project.

  **Note**: Adding a new topic to the documentation, or significantly re-writing a topic, counts as a major feature.

* **Small Features** can be crafted and directly [submitted as a Pull Request](#submit-pr).


## <a name="submit"></a> Submission Guidelines


### <a name="submit-issue"></a> Submitting an Issue

Before you submit an issue, please search the issue tracker. An issue for your problem might already exist and the discussion might inform you of workarounds readily available.

We want to fix all the issues as soon as possible, but before fixing a bug, we need to reproduce and confirm it.
In order to reproduce bugs, we require that you provide a minimal reproduction.
Having a minimal reproducible scenario gives us a wealth of important information without going back and forth to you with additional questions.

A minimal reproduction allows us to quickly confirm a bug (or point out a coding problem) as well as confirm that we are fixing the right problem.

We require a minimal reproduction to save maintainers' time and ultimately be able to fix more bugs.
Often, developers find coding problems themselves while preparing a minimal reproduction.
We understand that sometimes it might be hard to extract essential bits of code from a larger codebase, but we really need to isolate the problem before we can fix it.

Unfortunately, we are not able to investigate / fix bugs without a minimal reproduction, so if we don't hear back from you, we are going to close an issue that doesn't have enough info to be reproduced.

You can file new issues by selecting from our [new issue templates](https://github.com/angular/angular/issues/new/choose) and filling out the issue template.


### <a name="submit-pr"></a> Submitting a Pull Request (PR)

Before you submit your Pull Request (PR) consider the following guidelines:

1. Search [GitHub](https://github.com/angular/angular/pulls) for an open or closed PR that relates to your submission.
   You don't want to duplicate existing efforts.

2. Be sure that an issue describes the problem you're fixing, or documents the design for the feature you'd like to add.
   Discussing the design upfront helps to ensure that we're ready to accept your work.

3. Please sign our [Contributor License Agreement (CLA)](#cla) before sending PRs.
   We cannot accept code without a signed CLA.
   Make sure you author all contributed Git commits with email address associated with your CLA signature.

4. [Fork](https://docs.github.com/en/github/getting-started-with-github/fork-a-repo) the [angular/angular](https://github.com/angular/angular/fork) repo.

5. In your forked repository, make your changes in a new git branch:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
     ```shell
     git checkout -b my-fix-branch main
     ```

6. Create your patch, **including appropriate test cases**.

7. Follow our [Coding Rules](#rules).

8. Run the full Angular test suite, as described in the [developer documentation][dev-doc], and ensure that all tests pass.

9. Commit your changes using a descriptive commit message that follows our [commit message conventions][commit-message-guidelines].
   Adherence to these conventions is necessary because release notes are automatically generated from these messages.
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
     ```shell
     git commit --all
     ```
    Note: the optional commit `--all` command line option will automatically "add" and "rm" edited files.

10. Push your branch to GitHub:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
    ```shell
    git push origin my-fix-branch
    ```

11. In GitHub, send a pull request to `angular:main`.

#([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")## Reviewing a Pull Request

The Angular team reserves the right not to accept pull requests from community members who haven't been good citizens of the community. Such behavior includes not following the [Angular code of conduct](https://github.com/angular/code-of-conduct) and applies within or outside of Angular managed channels.

#### Addressing review feedback

If we ask for changes via code reviews then:

1. Make the required updates to the code.

2. Re-run the Angular test suites to ensure tests are still passing.

3. Create a fixup commit and push to your GitHub repository (this will update your Pull Request):
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
    ```shell
    git commit --all --fixup HEAD
    git push
    ```

    For more info on working with fixup commits see [here](./contributing-docs/using-fixup-commits.md).

That's it! Thank you for your contribution!


##### Updating the commit message

A reviewer might often suggest changes to a commit message (for example, to add more context for a change or adhere to our [commit message guidelines][commit-message-guidelines]).
In order to update the commit message of the last commit on your branch:

1. Check out your branch:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
    ```shell
    git checkout my-fix-branch
    ```
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
2. Amend the last commit and modify the commit message:

    ```shell
    git commit --amend
    ```

3. Push to your GitHub repository:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
    ```shell
    git push --force-with-lease
    ```

> NOTE:<br />
> If you need to update the commit message of an earlier commit, you can use `git rebase` in interactive mode.
> See the [git docs](https://git-scm.com/docs/git-rebase#_interactive_mode) for more details.

([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
#### After your pull request is merged

After your pull request is merged, you can safely delete your branch and pull the changes from the main (upstream) repository:

* Delete the remote branch on GitHub either through the GitHub web UI or your local shell as follows:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
    ```shell
    git push origin --delete my-fix-branch
    ```

* Check out the main branch:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
    ```shell
    git checkout main -f
    ```

* Delete the local branch:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
    ```shell
    git branch -D my-fix-branch
    ```

* Update your local `main` with the latest upstream version:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
    ```shell
    git pull --ff upstream main
    ```


## <a name="rules"></a> Coding Rules
To ensure consistency throughout the source code, keep these rules in mind as you are working:

* All features or bug fixes **must be tested** by one or more specs (unit-tests).
* All public API methods **must be documented**.
* We follow [Google's TypeScript Style Guide][ts-style-guide], but wrap all code at **100 characters**.

   An automated formatter is available, see [DEVELOPER.md](contributing-docs/building-and-testing-angular.md#formatting-your-source-code).


## <a name="commit"></a> Commit Message Guidelines

We have very precise rules over how our Git commit messages must be formatted:
```
<type>(<scope>): <short summary>
```

See [Commit Message Guidelines][commit-message-guidelines] for details.

## <a name="cla"></a> Signing the CLA

Please sign our Contributor License Agreement (CLA) before sending pull requests. For any code
changes to be accepted, the CLA must be signed. It's a quick process, we promise!

* For individuals, we have a [simple click-through form][individual-cla].
* For corporations, we'll need you to
  [print, sign and one of scan+email, fax or mail the form][corporate-cla].

If you have more than one GitHub accounts, or multiple email addresses associated with a single GitHub account, you must sign the CLA using the primary email address of the GitHub account used to author Git commits and send pull requests.

The following documents can help you sort out issues with GitHub accounts and multiple email addresses:

  * https://help.github.com/articles/setting-your-commit-email-address-in-git/
  * https://stackoverflow.com/questions/37245303/what-does-usera-committed-with-userb-13-days-ago-on-github-mean
  * https://help.github.com/articles/about-commit-email-addresses/
  * https://help.github.com/articles/blocking-command-line-pushes-that-expose-your-personal-email-address/




[coc]: https://github.com/angular/code-of-conduct/blob/main/CODE_OF_CONDUCT.md
[corporate-cla]: https://cla.developers.google.com/about/google-corporate
[dev-doc]: ./contributing-docs/building-and-testing-angular.md
[commit-message-guidelines]: ./contributing-docs/commit-message-guidelines.md
[github]: https://github.com/angular/angular
[discord]: https://discord.gg/angular
[individual-cla]: https://cla.developers.google.com/about/google-individual
[ts-style-guide]: https://google.github.io/styleguide/tsguide.html
// server.mjs
import { createServer } from 'node:http';

const server = createServer((req, res) => {
  res.writeHead(200, { 'Content-Type': 'text/plain' });
  res.end('Hello World!\n');
});

// starts a simple http server locally on port 3000
server.listen(3000, '127.0.0.1', () => {
  console.log('Listening on 127.0.0.1:3000');
});

// run with `node server.mjs`

# Docker has specific installation instructions for each operating system.
# Please refer to the official documentation at https://docker.com/get-started/
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
# Pull the Node.js Docker image:
docker pull node:22-alpine
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
# Create a Node.js container and start a Shell session:
docker run -it --rm --entrypoint sh node:22-alpine
# Use bash for the shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
# Create a script file sourced by both interactive and non-interactive bash shells
ENV BASH_ENV /home/user/.bash_env
RUN touch "${BASH_ENV}"
RUN echo '. "${BASH_ENV}"' >> ~/.bashrc
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
# Download and install nvm
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.2/install.sh | PROFILE="${BASH_ENV}" bash
RUN echo node > .nvmrc
RUN nvm install
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
# Verify the Node.js version:
node -v # Should print "v22.16.0".

# Verify npm version:
npm -v # Should print "10.9.2".

//npm.pkg.github.com/:_authToken=TOKEN
$ npm login --scope=@NAMESPACE --auth-type=legacy --registry=https://npm.pkg.github.com

> Username: USERNAME
> Password: TOKEN
@NAMESPACE:registry=https://npm.pkg.github.com

$ git add .
# Adds the file to your local repository and stages it for commit. To unstage a file, use 'git reset HEAD YOUR-FILE'.

$ git commit -m "Add existing file"
# Commits the tracked changes and prepares them to be pushed to a remote repository. To remove this commit and modify the file, use 'git reset --soft HEAD~1' and commit and add the file again.

$ git push origin YOUR_BRANCH
# Pushes the changes in your local repository up to the remote repository you specified as the origin

@my-org/test.

https://github.com/my-org/test.git.
npm publish

"publishConfig": {
  "registry": "https://npm.pkg.github.com"
},
https://github.com/my-org/test.git.
npm publish

#
name: Create and publish a Docker image
FROM ubuntu:latest
ARG NODE_VERSION=20

# install curl
RUN apt update && apt install curl -y

# install nvm
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash

# set env
ENV NVM_DIR=/root/.nvm

# install node
RUN bash -c "source $NVM_DIR/nvm.sh && nvm install $NODE_VERSION"

# set ENTRYPOINT for reloading nvm-environment
ENTRYPOINT ["bash", "-c", "source $NVM_DIR/nvm.sh && exec \"$@\"", "--"]

# set cmd to bash
CMD ["/bin/bash"]


# Configures this workflow to run every time a change is pushed to the branch called `release`.
on:
  push:
    branches: ['release']

# Defines two custom environment variables for the workflow. These are used for the Container registry domain, and a name for the Docker image that this workflow builds.
env:
  REGISTRY: ghcr.io
  IMAGE_NAME: ${{ github.repository }}

# There is a single job in this workflow. It's configured to run on the latest available version of Ubuntu.
jobs:
  build-and-push-image:
    runs-on: ubuntu-latest
    # Sets the permissions granted to the `GITHUB_TOKEN` for the actions in this job.
    permissions:
      contents: read
      packages: write
      attestations: write
      id-token: write
      #
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4
      # Uses the `docker/login-action` action to log in to the Container registry registry using the account and password that will publish the packages. Once published, the packages are scoped to the account defined here.
      - name: Log in to the Container registry
        uses: docker/login-action@65b78e6e13532edd9afa3aa52ac7964289d1a9c1
        with:
          registry: ${{ env.REGISTRY }}
          username: ${{ github.actor }}
          password: ${{ secrets.GITHUB_TOKEN }}
      # This step uses [docker/metadata-action](https://github.com/docker/metadata-action#about) to extract tags and labels that will be applied to the specified image. The `id` "meta" allows the output of this step to be referenced in a subsequent step. The `images` value provides the base name for the tags and labels.
      - name: Extract metadata (tags, labels) for Docker
        id: meta
        uses: docker/metadata-action@9ec57ed1fcdbf14dcef7dfbe97b2010124a938b7
        with:
          images: ${{ env.REGISTRY }}/${{ env.IMAGE_NAME }}
      # This step uses the `docker/build-push-action` action to build the image, based on your repository's `Dockerfile`. If the build succeeds, it pushes the image to GitHub Packages.
      # It uses the `context` parameter to define the build's context as the set of files located in the specified path. For more information, see [Usage](https://github.com/docker/build-push-action#usage) in the README of the `docker/build-push-action` repository.
      # It uses the `tags` and `labels` parameters to tag and label the image with the output from the "meta" step.
      - name: Build and push Docker image
        id: push
        uses: docker/build-push-action@f2a1d5e99d037542a71f64918e516c093c6f3fc4
        with:
          context: .
          push: true
          tags: ${{ steps.meta.outputs.tags }}
          labels: ${{ steps.meta.outputs.labels }}
      
      # This step generates an artifact attestation for the image, which is an unforgeable statement about where and how it was built. It increases supply chain security for people who consume the image. For more information, see [Using artifact attestations to establish provenance for builds](/actions/security-guides/using-artifact-attestations-to-establish-provenance-for-builds).
      - name: Generate artifact attestation
        uses: actions/attest-build-provenance@v2
        with:
          subject-name: ${{ env.REGISTRY }}/${{ env.IMAGE_NAME}}
          subject-digest: ${{ steps.push.outputs.digest }}
          push-to-registry: true
      

"repository":"https://github.com/OWNER/REPOSITORY",

{
  "name": "@my-org/server",
  "version": "1.0.0",
  "description": "Server app that uses the ORGANIZATION_NAME/PACKAGE_NAME package",
  "main": "index.js",
  "author": "",
  "license": "MIT",
  "dependencies": {
    "ORGANIZATION_NAME/PACKAGE_NAME": "1.0.0"
  }
}
npm install

@NAMESPACE:registry=https://npm.pkg.github.com
@NAMESPACE:registry=https://npm.pkg.github.com

#
name: Demo Push

# This workflow runs when any of the following occur:
# - A push is made to a branch called `main` or `seed`
# - A tag starting with "v" is created
# - A pull request is created or updated
on:
  push:
    branches:
      - main
      - seed
    tags:
      - v*
  pull_request:
  # This creates an environment variable called `IMAGE_NAME ` with the value `ghtoken_product_demo`.
env:
  IMAGE_NAME: ghtoken_product_demo
#
jobs:
  # This pushes the image to GitHub Packages.
  push:
    runs-on: ubuntu-latest
    permissions:
      packages: write
      contents: read
      #
    steps:
      - uses: actions/checkout@v4

      - name: Build image
        run: docker build . --file Dockerfile --tag $IMAGE_NAME --label "runnumber=${GITHUB_RUN_ID}"

      - name: Log in to registry
        run: echo "${{ secrets.GITHUB_TOKEN }}" | docker login ghcr.io -u ${{ github.actor }} --password-stdin
        #
      - name: Push image
        run: |
          IMAGE_ID=ghcr.io/${{ github.repository_owner }}/$IMAGE_NAME

          # This changes all uppercase characters to lowercase.
          IMAGE_ID=$(echo $IMAGE_ID | tr '[A-Z]' '[a-z]')
          # This strips the git ref prefix from the version.
          VERSION=$(echo "${{ github.ref }}" | sed -e 's,.*/\(.*\),\1,')
          # This strips the "v" prefix from the tag name.
          [[ "${{ github.ref }}" == "refs/tags/"* ]] && VERSION=$(echo $VERSION | sed -e 's/^v//')
          # This uses the Docker `latest` tag convention.
          [ "$VERSION" == "main" ] && VERSION=latest
          echo IMAGE_ID=$IMAGE_ID
          echo VERSION=$VERSION
          docker tag $IMAGE_NAME $IMAGE_ID:$VERSION
          docker push $IMAGE_ID:$VERSIONs

         ([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
          Skip to content
Navigation Menu
nvm-sh
nvm

Type / to search
Code
Issues
314
Pull requests
41
Actions
Security
Insights
Owner avatar
nvm
Public
nvm-sh/nvm
Go to file
t
Name		
ljharb
ljharb
v0.40.3
977563e
 · 
2 months ago
.github
[actions] release test needs git tags
4 months ago
test
[Fix] reinstall-packages: do not reinstall corepack
3 months ago
.dockerignore
[New] nvm use/nvm install: add --save option
3 years ago
.editorconfig
[New] allow .nvmrc files to support comments
last year
.gitattributes
[meta] fix gitattributes to properly recognize images as binary
2 years ago
.gitignore
[Tests] fix broken tests exposed by 863bd63
10 months ago
.gitmodules
[New] allow .nvmrc files to support comments
last year
.mailmap
Add a Git .mailmap with my new name
8 years ago
.npmrc
Only apps should have lockfiles
8 years ago
.travis.yml
[Tests] migrate installation_iojs test suite to GitHub Actions
7 months ago
CODE_OF_CONDUCT.md
[meta] use HEAD instead of master where possible
3 years ago
CONTRIBUTING.md
[meta] add DCO
7 months ago
Dockerfile
[readme] add docker tips
3 years ago
GOVERNANCE.md
[meta] add project charter and governance
4 years ago
LICENSE.md
[meta] add copyright line to license file
6 years ago
Makefile
[Tests] move sourcing suite to GHA
10 months ago
PROJECT_CHARTER.md
[meta] add project charter and governance
4 years ago
README.md
v0.40.3
2 months ago
ROADMAP.md
[meta] update repo links to point to org
6 years ago
bash_completion
[Fix] bash_completion: be robust when cd is overridden
4 years ago
install.sh
v0.40.3
2 months ago
nvm-exec
[Fix] nvm exec: no longer error with '-q: invalid option' for zsh u…
2 years ago
nvm.sh
v0.40.3
2 months ago
package.json
v0.40.3
2 months ago
rename_test.sh
[meta] Rename some files to be more cross platform
5 years ago
update_test_mocks.sh
[Refactor] add nvm_wrap_with_color_code; allow no color code
3 years ago
Repository files navigation
README
Code of conduct
MIT license
Security
nvm project logo
Node Version Manager Build Status nvm version CII Best Practices
Table of Contents
Intro
About
Installing and Updating
Install & Update Script
Additional Notes
Installing in Docker
Installing in Docker for CICD-Jobs
Troubleshooting on Linux
Troubleshooting on macOS
Ansible
Verify Installation
Important Notes
Git Install
Manual Install
Manual Upgrade
Usage
Long-term Support
Migrating Global Packages While Installing
Default Global Packages From File While Installing
io.js
System Version of Node
Listing Versions
Setting Custom Colors
Persisting custom colors
Suppressing colorized output
Restoring PATH
Set default node version
Use a mirror of node binaries
Pass Authorization header to mirror
.nvmrc
Deeper Shell Integration
Calling nvm use automatically in a directory with a .nvmrc file
bash
zsh
fish
Running Tests
Environment variables
Bash Completion
Usage
Compatibility Issues
Installing nvm on Alpine Linux
Alpine Linux 3.13+
Alpine Linux 3.5 - 3.12
Uninstalling / Removal
Manual Uninstall
Docker For Development Environment
Problems
macOS Troubleshooting
WSL Troubleshooting
Maintainers
Project Support
Enterprise Support
License
Copyright notice
Intro
nvm allows you to quickly install and use different versions of node via the command line.

Example:

$ nvm use 16
Now using node v16.9.1 (npm v7.21.1)
$ node -v
v16.9.1
$ nvm use 14
Now using node v14.18.0 (npm v6.14.15)
$ node -v
v14.18.0
$ nvm install 12
Now using node v12.22.6 (npm v6.14.5)
$ node -v
v12.22.6
Simple as that!

About
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
nvm is a version manager for node.js, designed to be installed per-user, and invoked per-shell. nvm works on any POSIX-compliant shell (sh, dash, ksh, zsh, bash), in particular on these platforms: unix, macOS, and windows WSL.

([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
Installing and Updating
Install & Update Script
To install or update nvm, you should run the install script. To do that, you may either download and run the script manually, or use the following cURL or Wget command:

curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
Running either of the above commands downloads a script and runs it. The script clones the nvm repository to ~/.nvm, and attempts to add the source lines from the snippet below to the correct profile file (~/.bashrc, ~/.bash_profile, ~/.zshrc, or ~/.profile). If you find the install script is updating the wrong profile file, set the $PROFILE env var to the profile file’s path, and then rerun the installation script.


export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
Additional Notes
If the environment variable $XDG_CONFIG_HOME is present, it will place the nvm files there.

You can add --no-use to the end of the above script to postpone using nvm until you manually use it:

export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" --no-use # This loads nvm, without auto-using the default version
You can customize the install source, directory, profile, and version using the NVM_SOURCE, NVM_DIR, PROFILE, and NODE_VERSION variables. Eg: curl ... | NVM_DIR="path/to/nvm". Ensure that the NVM_DIR does not contain a trailing slash.

The installer can use git, curl, or wget to download nvm, whichever is available.

You can instruct the installer to not edit your shell config (for example if you already get completions via a zsh nvm plugin) by setting PROFILE=/dev/null before running the install.sh script. Here's an example one-line command to do that: PROFILE=/dev/null bash -c 'curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash'
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
Installing in Docker
When invoking bash as a non-interactive shell, like in a Docker container, none of the regular profile files are sourced. In order to use nvm, node, and npm like normal, you can instead specify the special BASH_ENV variable, which bash sources when invoked non-interactively.
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
# Use bash for the shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
# Create a script file sourced by both interactive and non-interactive bash shells
ENV BASH_ENV /home/user/.bash_env
RUN touch "${BASH_ENV}"
RUN echo '. "${BASH_ENV}"' >> ~/.bashrc
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
# Download and install nvm
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.2/install.sh | PROFILE="${BASH_ENV}" bash
RUN echo node > .nvmrc
RUN nvm install
Installing in Docker for CICD-Jobs
More robust, works in CI/CD-Jobs. Can be run in interactive and non-interactive containers. See #3531.
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
FROM ubuntu:latest
ARG NODE_VERSION=20

# install curl
RUN apt update && apt install curl -y
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
# install nvm
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
# set env
ENV NVM_DIR=/root/.nvm
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
# install node
RUN bash -c "source $NVM_DIR/nvm.sh && nvm install $NODE_VERSION"
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
# set ENTRYPOINT for reloading nvm-environment
ENTRYPOINT ["bash", "-c", "source $NVM_DIR/nvm.sh && exec \"$@\"", "--"]
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
# set cmd to bash
CMD ["/bin/bash"]
This example defaults to installation of nodejs version 20.x.y. Optionally you can easily override the version with docker build args like:

docker build -t nvmimage --build-arg NODE_VERSION=19 .
After creation of the image you can start container interactively and run commands, for example:

docker run --rm -it nvmimage

root@0a6b5a237c14:/# nvm -v
0.40.3

root@0a6b5a237c14:/# node -v
v19.9.0

root@0a6b5a237c14:/# npm -v
9.6.3
Noninteractive example:

user@host:/tmp/test $ docker run --rm -it nvmimage node -v
v19.9.0
user@host:/tmp/test $ docker run --rm -it nvmimage npm -v
9.6.3
Troubleshooting on Linux
On Linux, after running the install script, if you get nvm: command not found or see no feedback from your terminal after you type command -v nvm, simply close your current terminal, open a new terminal, and try verifying again. Alternatively, you can run the following commands for the different shells on the command line:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
bash: source ~/.bashrc

zsh: source ~/.zshrc

ksh: . ~/.profile

These should pick up the nvm command.
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
Troubleshooting on macOS
Since OS X 10.9, /usr/bin/git has been preset by Xcode command line tools, which means we can't properly detect if Git is installed or not. You need to manually install the Xcode command line tools before running the install script, otherwise, it'll fail. (see #1782)

If you get nvm: command not found after running the install script, one of the following might be the reason:

Since macOS 10.15, the default shell is zsh and nvm will look for .zshrc to update, none is installed by default. Create one with touch ~/.zshrc and run the install script again.

If you use bash, the previous default shell, your system may not have .bash_profile or .bashrc files where the command is set up. Create one of them with touch ~/.bash_profile or touch ~/.bashrc and run the install script again. Then, run . ~/.bash_profile or . ~/.bashrc to pick up the nvm command.

You have previously used bash, but you have zsh installed. You need to manually add these lines to ~/.zshrc and run . ~/.zshrc.

You might need to restart your terminal instance or run . ~/.nvm/nvm.sh. Restarting your terminal/opening a new tab/window, or running the source command will load the command and the new configuration.

If the above didn't help, you might need to restart your terminal instance. Try opening a new tab/window in your terminal and retry.

If the above doesn't fix the problem, you may try the following:

If you use bash, it may be that your .bash_profile (or ~/.profile) does not source your ~/.bashrc properly. You could fix this by adding source ~/<your_profile_file> to it or following the next step below.

Try adding the snippet from the install section, that finds the correct nvm directory and loads nvm, to your usual profile (~/.bash_profile, ~/.zshrc, ~/.profile, or ~/.bashrc).

For more information about this issue and possible workarounds, please refer here

Note For Macs with the Apple Silicon chip, node started offering arm64 arch Darwin packages since v16.0.0 and experimental arm64 support when compiling from source since v14.17.0. If you are facing issues installing node using nvm, you may want to update to one of those versions or later.
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
Ansible
You can use a task:

- name: Install nvm
  ansible.builtin.shell: >
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
  args:
    creates: "{{ ansible_env.HOME }}/.nvm/nvm.sh"
Verify Installation
To verify that nvm has been installed, do:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
command -v nvm
which should output nvm if the installation was successful. Please note that which nvm will not work, since nvm is a sourced shell function, not an executable binary.

Note: On Linux, after running the install script, if you get nvm: command not found or see no feedback from your terminal after you type command -v nvm, simply close your current terminal, open a new terminal, and try verifying again.

Important Notes
If you're running a system without prepackaged binary available, which means you're going to install node or io.js from its source code, you need to make sure your system has a C++ compiler. For OS X, Xcode will work, for Debian/Ubuntu based GNU/Linux, the build-essential and libssl-dev packages work.

Note: nvm also supports Windows in some cases. It should work through WSL (Windows Subsystem for Linux) depending on the version of WSL. It should also work with GitBash (MSYS) or Cygwin. Otherwise, for Windows, a few alternatives exist, which are neither supported nor developed by us:

nvm-windows
nodist
nvs
Note: nvm does not support Fish either (see #303). Alternatives exist, which are neither supported nor developed by us:

bass allows you to use utilities written for Bash in fish shell
fast-nvm-fish only works with version numbers (not aliases) but doesn't significantly slow your shell startup
plugin-nvm plugin for Oh My Fish, which makes nvm and its completions available in fish shell
nvm.fish - The Node.js version manager you'll adore, crafted just for Fish
fish-nvm - Wrapper around nvm for fish, delays sourcing nvm until it's actually used.
Note: We still have some problems with FreeBSD, because there is no official pre-built binary for FreeBSD, and building from source may need patches; see the issue ticket:

[#900] [Bug] node on FreeBSD may need to be patched
nodejs/node#3716
Note: On OS X, if you do not have Xcode installed and you do not wish to download the ~4.3GB file, you can install the Command Line Tools. You can check out this blog post on how to just that:

How to Install Command Line Tools in OS X Mavericks & Yosemite (Without Xcode)
Note: On OS X, if you have/had a "system" node installed and want to install modules globally, keep in mind that:

When using nvm you do not need sudo to globally install a module with npm -g, so instead of doing sudo npm install -g grunt, do instead npm install -g grunt
If you have an ~/.npmrc file, make sure it does not contain any prefix settings (which is not compatible with nvm)
You can (but should not?) keep your previous "system" node install, but nvm will only be available to your user account (the one used to install nvm). This might cause version mismatches, as other users will be using /usr/local/lib/node_modules/* VS your user account using ~/.nvm/versions/node/vX.X.X/lib/node_modules/*
Homebrew installation is not supported. If you have issues with homebrew-installed nvm, please brew uninstall it, and install it using the instructions below, before filing an issue.

Note: If you're using zsh you can easily install nvm as a zsh plugin. Install zsh-nvm and run nvm upgrade to upgrade (you can set NVM_AUTO_USE=true to have it automatically detect and use .nvmrc files).

Note: Git versions before v1.7 may face a problem of cloning nvm source from GitHub via https protocol, and there is also different behavior of git before v1.6, and git prior to v1.17.10 can not clone tags, so the minimum required git version is v1.7.10. If you are interested in the problem we mentioned here, please refer to GitHub's HTTPS cloning errors article.
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
Git Install
If you have git installed (requires git v1.7.10+):

clone this repo in the root of your user profile
cd ~/ from anywhere then git clone https://github.com/nvm-sh/nvm.git .nvm
cd ~/.nvm and check out the latest version with git checkout v0.40.3
activate nvm by sourcing it from your shell: . ./nvm.sh
Now add these lines to your ~/.bashrc, ~/.profile, or ~/.zshrc file to have it automatically sourced upon login: (you may have to add to more than one of the above files)

export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
Manual Install
For a fully manual install, execute the following lines to first clone the nvm repository into $HOME/.nvm, and then load nvm:

export NVM_DIR="$HOME/.nvm" && (
  git clone https://github.com/nvm-sh/nvm.git "$NVM_DIR"
  cd "$NVM_DIR"
  git checkout `git describe --abbrev=0 --tags --match "v[0-9]*" $(git rev-list --tags --max-count=1)`
) && \. "$NVM_DIR/nvm.sh"
Now add these lines to your ~/.bashrc, ~/.profile, or ~/.zshrc file to have it automatically sourced upon login: (you may have to add to more than one of the above files)
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
Manual Upgrade
For manual upgrade with git (requires git v1.7.10+):

change to the $NVM_DIR
pull down the latest changes
check out the latest version
activate the new version
(
  cd "$NVM_DIR"
  git fetch --tags origin
  git checkout `git describe --abbrev=0 --tags --match "v[0-9]*" $(git rev-list --tags --max-count=1)`
) && \. "$NVM_DIR/nvm.sh"
Usage
To download, compile, and install the latest release of node, do this:

nvm install node # "node" is an alias for the latest version
To install a specific version of node:

nvm install 14.7.0 # or 16.3.0, 12.22.1, etc
To set an alias:

nvm alias my_alias v14.4.0
Make sure that your alias does not contain any spaces or slashes.

The first version installed becomes the default. New shells will start with the default version of node (e.g., nvm alias default).

You can list available versions using ls-remote:

nvm ls-remote
And then in any new shell just use the installed version:

nvm use node
Or you can just run it:

nvm run node --version
Or, you can run any arbitrary command in a subshell with the desired version of node:

nvm exec 4.2 node --version
You can also get the path to the executable to where it was installed:

nvm which 12.22
In place of a version pointer like "14.7" or "16.3" or "12.22.1", you can use the following special default aliases with nvm install, nvm use, nvm run, nvm exec, nvm which, etc:

node: this installs the latest version of node
iojs: this installs the latest version of io.js
stable: this alias is deprecated, and only truly applies to node v0.12 and earlier. Currently, this is an alias for node.
unstable: this alias points to node v0.11 - the last "unstable" node release, since post-1.0, all node versions are stable. (in SemVer, versions communicate breakage, not stability).
Long-term Support
Node has a schedule for long-term support (LTS) You can reference LTS versions in aliases and .nvmrc files with the notation lts/* for the latest LTS, and lts/argon for LTS releases from the "argon" line, for example. In addition, the following commands support LTS arguments:

nvm install --lts / nvm install --lts=argon / nvm install 'lts/*' / nvm install lts/argon
nvm uninstall --lts / nvm uninstall --lts=argon / nvm uninstall 'lts/*' / nvm uninstall lts/argon
nvm use --lts / nvm use --lts=argon / nvm use 'lts/*' / nvm use lts/argon
nvm exec --lts / nvm exec --lts=argon / nvm exec 'lts/*' / nvm exec lts/argon
nvm run --lts / nvm run --lts=argon / nvm run 'lts/*' / nvm run lts/argon
nvm ls-remote --lts / nvm ls-remote --lts=argon nvm ls-remote 'lts/*' / nvm ls-remote lts/argon
nvm version-remote --lts / nvm version-remote --lts=argon / nvm version-remote 'lts/*' / nvm version-remote lts/argon
Any time your local copy of nvm connects to https://nodejs.org, it will re-create the appropriate local aliases for all available LTS lines. These aliases (stored under $NVM_DIR/alias/lts), are managed by nvm, and you should not modify, remove, or create these files - expect your changes to be undone, and expect meddling with these files to cause bugs that will likely not be supported.

To get the latest LTS version of node and migrate your existing installed packages, use

nvm install --reinstall-packages-from=current 'lts/*'
Migrating Global Packages While Installing
If you want to install a new version of Node.js and migrate npm packages from a previous version:

nvm install --reinstall-packages-from=node node
This will first use "nvm version node" to identify the current version you're migrating packages from. Then it resolves the new version to install from the remote server and installs it. Lastly, it runs "nvm reinstall-packages" to reinstall the npm packages from your prior version of Node to the new one.

You can also install and migrate npm packages from specific versions of Node like this:

nvm install --reinstall-packages-from=5 6
nvm install --reinstall-packages-from=iojs v4.2
Note that reinstalling packages explicitly does not update the npm version — this is to ensure that npm isn't accidentally upgraded to a broken version for the new node version.

To update npm at the same time add the --latest-npm flag, like this:

nvm install --reinstall-packages-from=default --latest-npm 'lts/*'
or, you can at any time run the following command to get the latest supported npm version on the current node version:

nvm install-latest-npm
If you've already gotten an error to the effect of "npm does not support Node.js", you'll need to (1) revert to a previous node version (nvm ls & nvm use <your latest _working_ version from the ls>), (2) delete the newly created node version (nvm uninstall <your _broken_ version of node from the ls>), then (3) rerun your nvm install with the --latest-npm flag.

Default Global Packages From File While Installing
If you have a list of default packages you want installed every time you install a new version, we support that too -- just add the package names, one per line, to the file $NVM_DIR/default-packages. You can add anything npm would accept as a package argument on the command line.
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
# $NVM_DIR/default-packages

rimraf
object-inspect@1.0.2
stevemao/left-pad
io.js
If you want to install io.js:

nvm install iojs
If you want to install a new version of io.js and migrate npm packages from a previous version:

nvm install --reinstall-packages-from=iojs iojs
The same guidelines mentioned for migrating npm packages in node are applicable to io.js.

System Version of Node
If you want to use the system-installed version of node, you can use the special default alias "system":

nvm use system
nvm run system --version
Listing Versions
If you want to see what versions are installed:

nvm ls
If you want to see what versions are available to install:

nvm ls-remote
Setting Custom Colors
You can set five colors that will be used to display version and alias information. These colors replace the default colors. Initial colors are: g b y r e

Color codes:

r/R = red / bold red

g/G = green / bold green

b/B = blue / bold blue

c/C = cyan / bold cyan

m/M = magenta / bold magenta

y/Y = yellow / bold yellow

k/K = black / bold black

e/W = light grey / white
nvm set-colors rgBcm
Persisting custom colors
If you want the custom colors to persist after terminating the shell, export the NVM_COLORS variable in your shell profile. For example, if you want to use cyan, magenta, green, bold red and bold yellow, add the following line:

export NVM_COLORS='cmgRY'
Suppressing colorized output
nvm help (or -h or --help), nvm ls, nvm ls-remote and nvm alias usually produce colorized output. You can disable colors with the --no-colors option (or by setting the environment variable TERM=dumb):

nvm ls --no-colors
nvm help --no-colors
TERM=dumb nvm ls
Restoring PATH
To restore your PATH, you can deactivate it:

nvm deactivate
Set default node version
To set a default Node version to be used in any new shell, use the alias 'default':

nvm alias default node # this refers to the latest installed version of node
nvm alias default 18 # this refers to the latest installed v18.x version of node
nvm alias default 18.12  # this refers to the latest installed v18.12.x version of node
Use a mirror of node binaries
To use a mirror of the node binaries, set $NVM_NODEJS_ORG_MIRROR:

export NVM_NODEJS_ORG_MIRROR=https://nodejs.org/dist
nvm install node

NVM_NODEJS_ORG_MIRROR=https://nodejs.org/dist nvm install 4.2
To use a mirror of the io.js binaries, set $NVM_IOJS_ORG_MIRROR:

export NVM_IOJS_ORG_MIRROR=https://iojs.org/dist
nvm install iojs-v1.0.3

NVM_IOJS_ORG_MIRROR=https://iojs.org/dist nvm install iojs-v1.0.3
nvm use will not, by default, create a "current" symlink. Set $NVM_SYMLINK_CURRENT to "true" to enable this behavior, which is sometimes useful for IDEs. Note that using nvm in multiple shell tabs with this environment variable enabled can cause race conditions.

Pass Authorization header to mirror
To pass an Authorization header through to the mirror url, set $NVM_AUTH_HEADER

NVM_AUTH_HEADER="Bearer secret-token" nvm install node
.nvmrc
You can create a .nvmrc file containing a node version number (or any other string that nvm understands; see nvm --help for details) in the project root directory (or any parent directory). Afterwards, nvm use, nvm install, nvm exec, nvm run, and nvm which will use the version specified in the .nvmrc file if no version is supplied on the command line.

For example, to make nvm default to the latest 5.9 release, the latest LTS version, or the latest node version for the current directory:

$ echo "5.9" > .nvmrc

$ echo "lts/*" > .nvmrc # to default to the latest LTS version

$ echo "node" > .nvmrc # to default to the latest version
[NB these examples assume a POSIX-compliant shell version of echo. If you use a Windows cmd development environment, eg the .nvmrc file is used to configure a remote Linux deployment, then keep in mind the "s will be copied leading to an invalid file. Remove them.]
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
Then when you run nvm use:

$ nvm use
Found '/path/to/project/.nvmrc' with version <5.9>
Now using node v5.9.1 (npm v3.7.3)
Running nvm install will also switch over to the correct version, but if the correct node version isn't already installed, it will install it for you.

$ nvm install
Found '/path/to/project/.nvmrc' with version <5.9>
Downloading and installing node v5.9.1...
Downloading https://nodejs.org/dist/v5.9.1/node-v5.9.1-linux-x64.tar.xz...
#################################################################################### 100.0%
Computing checksum with sha256sum
Checksums matched!
Now using node v5.9.1 (npm v3.7.3)
nvm use et. al. will traverse directory structure upwards from the current directory looking for the .nvmrc file. In other words, running nvm use et. al. in any subdirectory of a directory with an .nvmrc will result in that .nvmrc being utilized.

The contents of a .nvmrc file must contain precisely one <version> (as described by nvm --help) followed by a newline. .nvmrc files may also have comments. The comment delimiter is #, and it and any text after it, as well as blank lines, and leading and trailing white space, will be ignored when parsing.

Key/value pairs using = are also allowed and ignored, but are reserved for future use, and may cause validation errors in the future.

Run npx nvmrc to validate an .nvmrc file. If that tool’s results do not agree with nvm, one or the other has a bug - please file an issue.

Deeper Shell Integration
You can use nvshim to shim the node, npm, and npx bins to automatically use the nvm config in the current directory. nvshim is not supported by the nvm maintainers. Please report issues to the nvshim team.

If you prefer a lighter-weight solution, the recipes below have been contributed by nvm users. They are not supported by the nvm maintainers. We are, however, accepting pull requests for more examples.

Calling nvm use automatically in a directory with a .nvmrc file
In your profile (~/.bash_profile, ~/.zshrc, ~/.profile, or ~/.bashrc), add the following to nvm use whenever you enter a new directory:

bash
Put the following at the end of your $HOME/.bashrc:

cdnvm() {
    command cd "$@" || return $?
    nvm_path="$(nvm_find_up .nvmrc | command tr -d '\n')"

    # If there are no .nvmrc file, use the default nvm version
    if [[ ! $nvm_path = *[^[:space:]]* ]]; then

        declare default_version
        default_version="$(nvm version default)"

        # If there is no default version, set it to `node`
        # This will use the latest version on your machine
        if [ $default_version = 'N/A' ]; then
            nvm alias default node
            default_version=$(nvm version default)
        fi

        # If the current version is not the default version, set it to use the default version
        if [ "$(nvm current)" != "${default_version}" ]; then
            nvm use default
        fi
    elif [[ -s "${nvm_path}/.nvmrc" && -r "${nvm_path}/.nvmrc" ]]; then
        declare nvm_version
        nvm_version=$(<"${nvm_path}"/.nvmrc)

        declare locally_resolved_nvm_version
        # `nvm ls` will check all locally-available versions
        # If there are multiple matching versions, take the latest one
        # Remove the `->` and `*` characters and spaces
        # `locally_resolved_nvm_version` will be `N/A` if no local versions are found
        locally_resolved_nvm_version=$(nvm ls --no-colors "${nvm_version}" | command tail -1 | command tr -d '\->*' | command tr -d '[:space:]')

        # If it is not already installed, install it
        # `nvm install` will implicitly use the newly-installed version
        if [ "${locally_resolved_nvm_version}" = 'N/A' ]; then
            nvm install "${nvm_version}";
        elif [ "$(nvm current)" != "${locally_resolved_nvm_version}" ]; then
            nvm use "${nvm_version}";
        fi
    fi
}

alias cd='cdnvm'
cdnvm "$PWD" || exit
This alias would search 'up' from your current directory in order to detect a .nvmrc file. If it finds it, it will switch to that version; if not, it will use the default version.

zsh
This shell function will install (if needed) and nvm use the specified Node version when an .nvmrc is found, and nvm use default otherwise.

Put this into your $HOME/.zshrc to call nvm use automatically whenever you enter a directory that contains an .nvmrc file with a string telling nvm which node to use:

# place this after nvm initialization!
autoload -U add-zsh-hook

load-nvmrc() {
  local nvmrc_path
  nvmrc_path="$(nvm_find_nvmrc)"

  if [ -n "$nvmrc_path" ]; then
    local nvmrc_node_version
    nvmrc_node_version=$(nvm version "$(cat "${nvmrc_path}")")

    if [ "$nvmrc_node_version" = "N/A" ]; then
      nvm install
    elif [ "$nvmrc_node_version" != "$(nvm version)" ]; then
      nvm use
    fi
  elif [ -n "$(PWD=$OLDPWD nvm_find_nvmrc)" ] && [ "$(nvm version)" != "$(nvm version default)" ]; then
    echo "Reverting to nvm default version"
    nvm use default
  fi
}

add-zsh-hook chpwd load-nvmrc
load-nvmrc
After saving the file, run source ~/.zshrc to reload the configuration with the latest changes made.

fish
This requires that you have bass installed.

# ~/.config/fish/functions/nvm.fish
function nvm
  bass source ~/.nvm/nvm.sh --no-use ';' nvm $argv
end

# ~/.config/fish/functions/nvm_find_nvmrc.fish
function nvm_find_nvmrc
  bass source ~/.nvm/nvm.sh --no-use ';' nvm_find_nvmrc
end

# ~/.config/fish/functions/load_nvm.fish
function load_nvm --on-variable="PWD"
  set -l default_node_version (nvm version default)
  set -l node_version (nvm version)
  set -l nvmrc_path (nvm_find_nvmrc)
  if test -n "$nvmrc_path"
    set -l nvmrc_node_version (nvm version (cat $nvmrc_path))
    if test "$nvmrc_node_version" = "N/A"
      nvm install (cat $nvmrc_path)
    else if test "$nvmrc_node_version" != "$node_version"
      nvm use $nvmrc_node_version
    end
  else if test "$node_version" != "$default_node_version"
    echo "Reverting to default Node version"
    nvm use default
  end
end

# ~/.config/fish/config.fish
# You must call it on initialization or listening to directory switching won't work
load_nvm > /dev/stderr
Running Tests
Tests are written in Urchin. Install Urchin (and other dependencies) like so:

npm install
There are slow tests and fast tests. The slow tests do things like install node and check that the right versions are used. The fast tests fake this to test things like aliases and uninstalling. From the root of the nvm git repository, run the fast tests like this:

npm run test/fast
Run the slow tests like this:

npm run test/slow
Run all of the tests like this:

npm test
Nota bene: Avoid running nvm while the tests are running.

Environment variables
nvm exposes the following environment variables:

NVM_DIR - nvm's installation directory.
NVM_BIN - where node, npm, and global packages for the active version of node are installed.
NVM_INC - node's include file directory (useful for building C/C++ addons for node).
NVM_CD_FLAGS - used to maintain compatibility with zsh.
NVM_RC_VERSION - version from .nvmrc file if being used.
Additionally, nvm modifies PATH, and, if present, MANPATH and NODE_PATH when changing versions.

Bash Completion
To activate, you need to source bash_completion:

[[ -r $NVM_DIR/bash_completion ]] && \. $NVM_DIR/bash_completion
Put the above sourcing line just below the sourcing line for nvm in your profile (.bashrc, .bash_profile).

Usage
nvm:

$ nvm Tab

alias               deactivate          install             list-remote         reinstall-packages  uninstall           version
cache               exec                install-latest-npm  ls                  run                 unload              version-remote
current             help                list                ls-remote           unalias             use                 which
nvm alias:

$ nvm alias Tab

default      iojs         lts/*        lts/argon    lts/boron    lts/carbon   lts/dubnium  lts/erbium   node         stable       unstable
$ nvm alias my_alias Tab

v10.22.0       v12.18.3      v14.8.0
nvm use:

$ nvm use Tab

my_alias        default        v10.22.0       v12.18.3      v14.8.0
nvm uninstall:

$ nvm uninstall Tab

my_alias        default        v10.22.0       v12.18.3      v14.8.0
Compatibility Issues
nvm will encounter some issues if you have some non-default settings set. (see #606) The following are known to cause issues:

Inside ~/.npmrc:

prefix='some/path'
Environment Variables:

$NPM_CONFIG_PREFIX
$PREFIX
Shell settings:

set -e
Installing nvm on Alpine Linux
In order to provide the best performance (and other optimizations), nvm will download and install pre-compiled binaries for Node (and npm) when you run nvm install X. The Node project compiles, tests and hosts/provides these pre-compiled binaries which are built for mainstream/traditional Linux distributions (such as Debian, Ubuntu, CentOS, RedHat et al).

Alpine Linux, unlike mainstream/traditional Linux distributions, is based on BusyBox, a very compact (~5MB) Linux distribution. BusyBox (and thus Alpine Linux) uses a different C/C++ stack to most mainstream/traditional Linux distributions - musl. This makes binary programs built for such mainstream/traditional incompatible with Alpine Linux, thus we cannot simply nvm install X on Alpine Linux and expect the downloaded binary to run correctly - you'll likely see "...does not exist" errors if you try that.

There is a -s flag for nvm install which requests nvm download Node source and compile it locally.

If installing nvm on Alpine Linux is still what you want or need to do, you should be able to achieve this by running the following from you Alpine Linux shell, depending on which version you are using:

Alpine Linux 3.13+
apk add -U curl bash ca-certificates openssl ncurses coreutils python3 make gcc g++ libgcc linux-headers grep util-linux binutils findutils
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
Alpine Linux 3.5 - 3.12
apk add -U curl bash ca-certificates openssl ncurses coreutils python2 make gcc g++ libgcc linux-headers grep util-linux binutils findutils
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
Note: Alpine 3.5 can only install NodeJS versions up to v6.9.5, Alpine 3.6 can only install versions up to v6.10.3, Alpine 3.7 installs versions up to v8.9.3, Alpine 3.8 installs versions up to v8.14.0, Alpine 3.9 installs versions up to v10.19.0, Alpine 3.10 installs versions up to v10.24.1, Alpine 3.11 installs versions up to v12.22.6, Alpine 3.12 installs versions up to v12.22.12, Alpine 3.13 & 3.14 install versions up to v14.20.0, Alpine 3.15 & 3.16 install versions up to v16.16.0 (These are all versions on the main branch). Alpine 3.5 - 3.12 required the package python2 to build NodeJS, as they are older versions to build. Alpine 3.13+ requires python3 to successfully build newer NodeJS versions, but you can use python2 with Alpine 3.13+ if you need to build versions of node supported in Alpine 3.5 - 3.15, you just need to specify what version of NodeJS you need to install in the package install script.

The Node project has some desire but no concrete plans (due to the overheads of building, testing and support) to offer Alpine-compatible binaries.

As a potential alternative, @mhart (a Node contributor) has some Docker images for Alpine Linux with Node and optionally, npm, pre-installed.

([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
Uninstalling / Removal
Manual Uninstall
To remove nvm manually, execute the following:

First, use nvm unload to remove the nvm command from your terminal session and delete the installation directory:

$ nvm_dir="${NVM_DIR:-~/.nvm}"
$ nvm unload
$ rm -rf "$nvm_dir"
Edit ~/.bashrc (or other shell resource config) and remove the lines below:

export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
[[ -r $NVM_DIR/bash_completion ]] && \. $NVM_DIR/bash_completion
Docker For Development Environment
To make the development and testing work easier, we have a Dockerfile for development usage, which is based on Ubuntu 18.04 base image, prepared with essential and useful tools for nvm development, to build the docker image of the environment, run the docker command at the root of nvm repository:

$ docker build -t nvm-dev .
This will package your current nvm repository with our pre-defined development environment into a docker image named nvm-dev, once it's built with success, validate your image via docker images:

$ docker images

REPOSITORY         TAG                 IMAGE ID            CREATED             SIZE
nvm-dev            latest              9ca4c57a97d8        7 days ago          650 MB
If you got no error message, now you can easily involve in:

$ docker run -h nvm-dev -it nvm-dev

nvm@nvm-dev:~/.nvm$
Please note that it'll take about 8 minutes to build the image and the image size would be about 650MB, so it's not suitable for production usage.

For more information and documentation about docker, please refer to its official website:

https://www.docker.com/
https://docs.docker.com/
Problems
If you try to install a node version and the installation fails, be sure to run nvm cache clear to delete cached node downloads, or you might get an error like the following:

curl: (33) HTTP server doesn't seem to support byte ranges. Cannot resume.

Where's my sudo node? Check out #43

After the v0.8.6 release of node, nvm tries to install from binary packages. But in some systems, the official binary packages don't work due to incompatibility of shared libs. In such cases, use -s option to force install from source:

nvm install -s 0.8.6
If setting the default alias does not establish the node version in new shells (i.e. nvm current yields system), ensure that the system's node PATH is set before the nvm.sh source line in your shell profile (see #658)
macOS Troubleshooting
nvm node version not found in vim shell

If you set node version to a version other than your system node version nvm use 6.2.1 and open vim and run :!node -v you should see v6.2.1 if you see your system version v0.12.7. You need to run:

sudo chmod ugo-x /usr/libexec/path_helper
More on this issue in dotphiles/dotzsh.

nvm is not compatible with the npm config "prefix" option

Some solutions for this issue can be found here

There is one more edge case causing this issue, and that's a mismatch between the $HOME path and the user's home directory's actual name.

You have to make sure that the user directory name in $HOME and the user directory name you'd see from running ls /Users/ are capitalized the same way (See this issue).

To change the user directory and/or account name follow the instructions here

Homebrew makes zsh directories unsecure

zsh compinit: insecure directories, run compaudit for list.
Ignore insecure directories and continue [y] or abort compinit [n]? y
Homebrew causes insecure directories like /usr/local/share/zsh/site-functions and /usr/local/share/zsh. This is not an nvm problem - it is a homebrew problem. Refer here for some solutions related to the issue.

Macs with Apple Silicon chips

Experimental support for the Apple Silicon chip architecture was added in node.js v15.3 and full support was added in v16.0. Because of this, if you try to install older versions of node as usual, you will probably experience either compilation errors when installing node or out-of-memory errors while running your code.

So, if you want to run a version prior to v16.0 on an Apple Silicon Mac, it may be best to compile node targeting the x86_64 Intel architecture so that Rosetta 2 can translate the x86_64 processor instructions to ARM-based Apple Silicon instructions. Here's what you will need to do:

Install Rosetta, if you haven't already done so

$ softwareupdate --install-rosetta
You might wonder, "how will my Apple Silicon Mac know to use Rosetta for a version of node compiled for an Intel chip?". If an executable contains only Intel instructions, macOS will automatically use Rosetta to translate the instructions.

Open a shell that's running using Rosetta

$ arch -x86_64 zsh
Note: This same thing can also be accomplished by finding the Terminal or iTerm App in Finder, right clicking, selecting "Get Info", and then checking the box labeled "Open using Rosetta".

Note: This terminal session is now running in zsh. If zsh is not the shell you typically use, nvm may not be source'd automatically like it probably is for your usual shell through your dotfiles. If that's the case, make sure to source nvm.

$ source "${NVM_DIR}/nvm.sh"
Install whatever older version of node you are interested in. Let's use 12.22.1 as an example. This will fetch the node source code and compile it, which will take several minutes.

$ nvm install v12.22.1 --shared-zlib
Note: You're probably curious why --shared-zlib is included. There's a bug in recent versions of Apple's system clang compiler. If one of these broken versions is installed on your system, the above step will likely still succeed even if you didn't include the --shared-zlib flag. However, later, when you attempt to npm install something using your old version of node.js, you will see incorrect data check errors. If you want to avoid the possible hassle of dealing with this, include that flag. For more details, see this issue and this comment

Exit back to your native shell.

$ exit
$ arch
arm64
Note: If you selected the box labeled "Open using Rosetta" rather than running the CLI command in the second step, you will see i386 here. Unless you have another reason to have that box selected, you can deselect it now.

Check to make sure the architecture is correct. x64 is the abbreviation for x86_64, which is what you want to see.

$ node -p process.arch
x64
Now you should be able to use node as usual.

WSL Troubleshooting
If you've encountered this error on WSL-2:

curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
% Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                Dload  Upload  Total   Spent    Left  Speed
0     0    0     0    0     0      0      0 --:--:--  0:00:09 --:--:--     0curl: (6) Could not resolve host: raw.githubusercontent.com
It may be due to your antivirus, VPN, or other reasons.

Where you can ping 8.8.8.8 while you can't ping google.com

This could simply be solved by running this in your root directory:

sudo rm /etc/resolv.conf
sudo bash -c 'echo "nameserver 8.8.8.8" > /etc/resolv.conf'
sudo bash -c 'echo "[network]" > /etc/wsl.conf'
sudo bash -c 'echo "generateResolvConf = false" >> /etc/wsl.conf'
sudo chattr +i /etc/resolv.conf
This deletes your resolv.conf file that is automatically generated when you run WSL, creates a new file and puts nameserver 8.8.8.8, then creates a wsl.conf file and adds [network] and generateResolveConf = false to prevent auto-generation of that file.

You can check the contents of the file by running:

cat /etc/resolv.conf
Maintainers
Currently, the sole maintainer is @ljharb - more maintainers are quite welcome, and we hope to add folks to the team over time. Governance will be re-evaluated as the project evolves.

Project Support
Only the latest version (v0.40.3 at this time) is supported.

Enterprise Support
If you are unable to update to the latest version of nvm, our partners provide commercial security fixes for all unsupported versions:

HeroDevs Never-Ending Support
License
See LICENSE.md.

Copyright notice
Copyright OpenJS Foundation and nvm contributors. All rights reserved. The OpenJS Foundation has registered trademarks and uses trademarks. For a list of trademarks of the OpenJS Foundation, please see our Trademark Policy and Trademark List. Trademarks and logos not indicated on the list of OpenJS Foundation trademarks are trademarks™ or registered® trademarks of their respective holders. Use of them does not imply any affiliation with or endorsement by them. The OpenJS Foundation | Terms of Use | Privacy Policy | Bylaws | Code of Conduct | Trademark Policy | Trademark List | Cookie Policy

About
Node Version Manager - POSIX-compliant bash script to manage multiple active node.js versions

Topics
nodejs shell bash zsh node install nvm posix lts version-manager node-js posix-compliant nvmrc
Resources
 Readme
License
 MIT license
Code of conduct
 Code of conduct
Security policy
 Security policy
 Activity
 Custom properties
Stars
 85.4k stars
Watchers
 1k watching
Forks
 8.9k forks
Report repository
Releases 70
v0.40.3
Latest
on Apr 24
+ 69 releases
Sponsor this project
@ljharb
ljharb Jordan Harband
tidelift
tidelift.com/funding/github/npm/nvm
Learn more about GitHub Sponsors
Contributors
371
@ljharb
@PeterDaveHello
@creationix
@koenpunt
@lukechilds
@frasertweedale
@agnoster
@danielb2
@nlf
@nmarghetti
@ELLIOTTCABLE
@kt3k
@sladyn98
@tlevine
+ 357 contributors
Languages
Shell
98.0%
 
Makefile
1.2%
 
Other
0.8%
Footer
© 2025 GitHub, Inc.
Footer navigation
Terms
Privacy
Security
Status
Docs
Contact
Manage cookies
Do not share my personal information












([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
#!/usr/bin/env bash

set -e

echo 'Updating test mocks...'

MOCKS_DIR="$PWD/test/fast/Unit tests/mocks"

echo "creating $MOCKS_DIR"
mkdir -p "$MOCKS_DIR"

\. "$NVM_DIR/nvm.sh" --no-use
nvm deactivate 2> /dev/null
nvm_is_version_installed() {
  return 1
}

([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
nvm_make_alias() {
  # prevent local alias creation
  return 0
}

([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
nvm_ls_remote > "$MOCKS_DIR/nvm_ls_remote.txt"
nvm_ls_remote_iojs > "$MOCKS_DIR/nvm_ls_remote_iojs.txt"
NVM_LTS=* nvm_ls_remote > "$MOCKS_DIR/nvm_ls_remote LTS.txt"
NVM_LTS=argon nvm_ls_remote > "$MOCKS_DIR/nvm_ls_remote LTS argon.txt"
nvm_download -L -s "https://nodejs.org/download/nightly/index.tab" -o - > "$MOCKS_DIR/nodejs.org-download-nightly-index.tab"
nvm_download -L -s "$(nvm_get_mirror iojs std)/index.tab" -o - > "$MOCKS_DIR/iojs.org-dist-index.tab"
NVM_COLORS=0ygre nvm ls-remote > "$MOCKS_DIR/nvm ls-remote.txt"
NVM_COLORS=0ygre nvm ls-remote --lts > "$MOCKS_DIR/nvm ls-remote lts.txt"
NVM_COLORS=0ygre nvm ls-remote node > "$MOCKS_DIR/nvm ls-remote node.txt"
NVM_COLORS=0ygre nvm ls-remote iojs > "$MOCKS_DIR/nvm ls-remote iojs.txt"
nvm_print_implicit_alias remote stable > "$MOCKS_DIR/nvm_print_implicit_alias remote stable.txt"
nvm_ls_remote stable > "$MOCKS_DIR/nvm_ls_remote stable.txt"
nvm alias "lts/*" > "$MOCKS_DIR/lts-star.txt"

([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
set +e
NVM_NODEJS_ORG_MIRROR=https://nodejs.org/download/nightly/ nvm_ls_remote > "$MOCKS_DIR/nvm_ls_remote nightly.txt"
nvm_download -L -s "$(nvm_get_mirror node std)/index.tab" -o - > "$MOCKS_DIR/nodejs.org-dist-index.tab"
NVM_NODEJS_ORG_MIRROR=https://nodejs.org/download/nightly/ nvm_print_implicit_alias remote stable > "$MOCKS_DIR/nvm_print_implicit_alias remote stable nightly.txt"
NVM_NODEJS_ORG_MIRROR=https://nodejs.org/download/nightly/ nvm_ls_remote stable > "$MOCKS_DIR/nvm_ls_remote stable nightly.txt"
NVM_NODEJS_ORG_MIRROR=https://nodejs.org/download/nightly/ NVM_LTS=* nvm_ls_remote > "$MOCKS_DIR/nvm_ls_remote LTS nightly.txt"
NVM_NODEJS_ORG_MIRROR=https://nodejs.org/download/nightly/ NVM_LTS=argon nvm_ls_remote > "$MOCKS_DIR/nvm_ls_remote LTS nightly argon.txt"
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
set -e

ALIAS_PATH="$MOCKS_DIR/nvm_make_alias LTS alias calls.txt"
: > "$ALIAS_PATH"
LTS_NAMES_PATH="$MOCKS_DIR/LTS_names.txt"
: > "$LTS_NAMES_PATH"
nvm_make_alias() {
  # prevent local alias creation, and store arguments
  echo "${1}|${2}" >> "$ALIAS_PATH"
  if [ "${1}" != 'lts/*' ]; then
    echo "${1#lts/}" >> "$LTS_NAMES_PATH"
  fi
}
nvm ls-remote --lts > /dev/null

echo "done! Don't forget to git commit them."

([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
4b4154ea040349bfd40215ec4e4cc9f372fe95f3# nvmwebeconsappbuildjaabe
nvm webeconsappbuildjaabe
# NVM Web – Minimal Starter

# Contributing to the Firebase JS SDK

We'd love for you to contribute to our source code and to help make the Firebase JS SDK even better
than it is today! Here are the guidelines we'd like you to follow:

 - [Code of Conduct](#coc)
 - [Question or Problem?](#question)
 - [Issues and Bugs](#issue)
 - [Submission Guidelines](#submit)
 - [Updating Documentation](#docs)

## <a name="coc"></a> Code of Conduct

As contributors and maintainers of the Firebase JS SDK project, we pledge to respect everyone who
contributes by posting issues, updating documentation, submitting pull requests, providing feedback
in comments, and any other activities.

Communication through any of Firebase's channels (GitHub, StackOverflow, X, etc.)
must be constructive and never resort to personal attacks, trolling, public or private harassment,
insults, or other unprofessional conduct.

We promise to extend courtesy and respect to everyone involved in this project regardless of gender,
gender identity, sexual orientation, disability, age, race, ethnicity, religion, or level of
experience. We expect anyone contributing to the project to do the same.

If any member of the community violates this code of conduct, the maintainers of the Firebase JS SDK
project may take action, removing issues, comments, and PRs or blocking accounts as deemed
appropriate.

If you are subject to or witness unacceptable behavior, or have any other concerns, please drop us a
line at firebase-code-of-conduct@google.com.

## <a name="question"></a> Got a Question?

If you have questions about how to use the Firebase JS SDK, please direct these to
[StackOverflow][stackoverflow] and use the `firebase` and `javascript` tags. You can also use the
[Firebase Google Group][firebase-google-group] or [Slack][slack] to contact members of the Firebase
team for help.

## <a name="issue"></a> Found an Issue?

If you find a bug in the source code, a mistake in the documentation, or some other issue, you can
help us by submitting an issue to our [GitHub Repository][github]. Even better you can submit a Pull
Request with a test demonstrating the bug and a fix!

See [below](#submit) for some guidelines.

## <a name="other-issue"></a> Production Issues

If you have a production issue, please [contact Firebase support][support] who will work with you to
resolve the issue.

## <a name="submit"></a> Submission Guidelines

### Submitting an Issue

Before you submit your issue, try searching [past issues][archive], [StackOverflow][stackoverflow],
and the [Firebase Google Group][firebase-google-group] for issues similar to your own. You can help
us to maximize the effort we spend fixing issues, and adding new features, by not reporting
duplicate issues.

If you encounter an issue that appears to be a bug that has not been reported before, please
[open a new issue in the repo](https://github.com/firebase/firebase-js-sdk/issues/new/choose). When
filling out the new issue report form, be sure to include as much information as possible, such as
reproduction steps, the error message you received, and any screenshots or other relevant data. The
more context you can provide the better we will be able to understand the issue, route it to the
appropriate team, and provide you with the help you need.

Also as a great rule of thumb:

**If you get help, help others. Good karma rulez!**

## Before you Contribute

### Sign our Contributor License Agreement

Contributions to this project must be accompanied by a
[Contributor License Agreement](https://cla.developers.google.com/about) (CLA).
You (or your employer) retain the copyright to your contribution; this simply
gives us permission to use and redistribute your contributions as part of the
project.

If you or your current employer have already signed the Google CLA (even if it
was for a different project), you probably don't need to do it again.

Visit <https://cla.developers.google.com/> to see your current agreements or to
sign a new one.

### Review our community guidelines

This project follows
[Google's Open Source Community Guidelines](https://opensource.google/conduct/).

### Submitting a Pull Request

All submissions, including submissions by project members, require review. We use GitHub pull
requests for this purpose. Consult
[GitHub Help](https://help.github.com/articles/about-pull-requests/) for more information on using
pull requests.

If you plan to work on a larger contribution, you should get in touch with us first through the
issue tracker with your idea so that we can help out and possibly guide you. Coordinating up front
makes it much easier to avoid frustration later on. Some pull requests (large contributions, API
additions/changes, etc) may be subject to additional internal review, we appreciate your patience as
we fully validate your contribution.

#### Pull Request Guidelines

* Search [GitHub](https://github.com/firebase/firebase-js-sdk/pulls) for an open or closed Pull
Request that relates to your submission. You don't want to duplicate effort.
* Create an issue to discuss a change before submitting a PR. We'd hate to have to turn down your
contributions because of something that could have been communicated early on.
* [Create a fork of the GitHub repo][fork-repo] to ensure that you can push your changes for us to
review.
* Make your changes in a new git branch:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
  ```shell
  git checkout -b my-fix-branch main
  ```
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
* Create your change, **including appropriate test cases**. Changes with tests are more likely to be
merged.
* Avoid checking in files that shouldn't be tracked (e.g `node_modules`, `gulp-cache`, `.tmp`,
`.idea`). If your development setup automatically creates some of these files, please add them to
the `.gitignore` at the root of the package (click [here][gitignore] to read more on how to add
entries to the `.gitignore`).
* Commit your changes
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
     ```shell
     git commit -a
     ```
  _Note: the optional commit `-a` command line option will automatically "add" and "rm" edited
  files._

* Test your changes locally to ensure everything is in good working order:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
    ```shell
   npm test
    ```
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
* Push your branch to your fork on GitHub:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
    ```shell
    git push origin my-fix-branch
    ```

* In GitHub, create a pull request against the `firebase-js-sdk:main` branch.
* Add changeset. See [Adding changeset to PR](#adding-changeset-to-pr).
* All pull requests must be reviewed by a member of the Firebase JS SDK team, who will merge it
when/if they feel it is good to go.

That's it! Thank you for your contribution!

#### Adding changeset to PR
The repository uses changesets to associate PR contributions with major and minor version releases
and patch releases. If your change is a feature or a behavioral change (either of which should
correspond to a version bump) then you will need to generate a changeset in your PR to track the
change.

Start the changeset creation process by running the following command in the base directory of the
repository:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```shell
yarn changeset
```

You will be asked to create a description (here's an [example](https://github.com/firebase/firebase-js-sdk/pull/3284#issuecomment-649718617)). You
should include the version bump for your package as well as the description for the change. Valid
version bump types are major, minor or patch, where:

 * a major version is an incompatible API change
 * a minor version is a backwards compatible API change
 * a patch version is a backwards compatible bug fix or any change that does not affect the API. A
   refactor, for example.

Please always include the firebase package with the same version bump type as your package. This is
to ensure that the version of the firebase package will be bumped correctly, 

 For example,
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```
---
"@firebase/storage": minor
"firebase": minor
---

This is a test.
```

You do not need to create a Changeset for the following changes:

 * the addition or alteration of a test
 * documentation updates
 * updates to the repository’s CI
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
#### Multiple changeset files

If your PR touches multiple SDKs or addresses multiple issues that require
different version bump or different description, you can create multiple
changeset files in the PR.

## <a name="docs"></a> Updating Documentation

Reference docs for the Firebase [JS SDK](https://firebase.google.com/docs/reference/js/) and
[Node (client) SDK](https://firebase.google.com/docs/reference/node/) are generated by
[Typedoc](https://typedoc.org/).

Typedoc generates this documentation from the main
[firebase index.d.ts type definition file](packages/firebase/compat/index.d.ts).  Any updates to
documentation should be made in that file.

If any pages are added or removed by your change (by adding or removing a class or interface), the
[js/toc.yaml](scripts/docgen/content-sources/js/toc.yaml) and/or
[node/toc.yaml](scripts/docgen/content-sources/node/toc.yaml) need to be modified to reflect this.

# Formatting Code
A Formatting Check CI failure in your PR indicates that the code does not follow the repo's
formatting guidelines. In your local build environment, please run the code formatting tool locally
by executing the command `yarn format`. Once the code is formatted, commit the changes and push your
branch. The push should cause the CI to re-check your PR's changes.
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
# Generating Documentation HTML Files

If the Doc Change Check fails in your PR, it indicates that the documentation has not been generated
correctly for the changes. In your local build environment, please run the following commands in the
root directory to generate the documentation locally:

```
yarn
yarn docgen:all
```

This will generate reference docs and the toc in `docs-devsite/`. Commit and push the generated
documentation changes to GitHub following the [PR submission guidelines](#submit). Your push
to the remote repository should force any failing documentation checks to execute again.

**NOTE:** These files are formatted to be inserted into Google's documentation site, which adds some
styling and navigation, so the raw files will be missing navigation elements and may not look
polished. However, it should be enough to preview the content.

[archive]: https://github.com/firebase/firebase-js-sdk/issues?utf8=%E2%9C%93&q=is%3Aissue
[file-an-issue]: https://github.com/firebase/firebase-js-sdk/issues/new
[firebase-google-group]: https://groups.google.com/forum/#!forum/firebase-talk
[fork-repo]: https://github.com/firebase/firebase-js-sdk/fork
[github]: https://github.com/firebase/firebase-js-sdk
[gitignore]: https://git-scm.com/docs/gitignore
[google-cla]: https://cla.developers.google.com/about/google-individual
[js-style-guide]: http://google.github.io/styleguide/javascriptguide.xml
[jsbin]: http://jsbin.com/rinilu/edit?js,console
[slack]: https://firebase-community.appspot.com/
[stackoverflow]: http://stackoverflow.com/questions/tagged/firebase
[support]: https://firebase.google.com/support/

## Features

- **Backend (Node.js/Express):** REST API for nvm commands (list Node.js versions)
- **Frontend (React):** Displays Node.js versions from backend
- **Dockerized:** Run both with `docker-compose up`

## Quick Start
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
# nvm-web Google Cloud Quickstart

This guide shows how to deploy your nvm-web project (Node.js backend + React frontend, both in Docker) to Google Cloud using **Cloud Run**.

---

## Prerequisites

- [Google Cloud account](https://console.cloud.google.com/)
- [Google Cloud SDK (gcloud) installed](https://cloud.google.com/sdk/docs/install)
- [Docker installed](https://docs.docker.com/get-docker/)
- Your project code ready in two folders: `backend/` and `frontend/`

---

## 1. Set Up Google Cloud
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```bash
gcloud auth login
gcloud config set project YOUR_PROJECT_ID
gcloud config set run/region YOUR_REGION
```

---

## 2. Enable Required APIs
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```bash
gcloud services enable run.googleapis.com artifactregistry.googleapis.com
```

---

## 3. Build & Push Docker Images

1. **Create Artifact Registry:**
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
   ```bash
   gcloud artifacts repositories create nvm-web-repo --repository-format=docker --location=YOUR_REGION
   ```

2. **Build and Push Backend:**
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
   ```bash
   docker build -t YOUR_REGION-docker.pkg.dev/YOUR_PROJECT_ID/nvm-web-repo/nvm-web-backend:latest ./backend
   docker push YOUR_REGION-docker.pkg.dev/YOUR_PROJECT_ID/nvm-web-repo/nvm-web-backend:latest
   ```

3. **Build and Push Frontend:**
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
   ```bash
   docker build -t YOUR_REGION-docker.pkg.dev/YOUR_PROJECT_ID/nvm-web-repo/nvm-web-frontend:latest ./frontend
   docker push YOUR_REGION-docker.pkg.dev/YOUR_PROJECT_ID/nvm-web-repo/nvm-web-frontend:latest
   ```

---

## 4. Deploy to Cloud Run

1. **Deploy Backend:**
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
   ```bash
   gcloud run deploy nvm-web-backend \
     --image YOUR_REGION-docker.pkg.dev/YOUR_PROJECT_ID/nvm-web-repo/nvm-web-backend:latest \
     --platform managed \
     --allow-unauthenticated \
     --port 4000
   ```

2. **Deploy Frontend:**
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
   ```bash
   gcloud run deploy nvm-web-frontend \
     --image YOUR_REGION-docker.pkg.dev/YOUR_PROJECT_ID/nvm-web-repo/nvm-web-frontend:latest \
     --platform managed \
     --allow-unauthenticated \
     --port 80
   ```

---

## 5. Access Your Services
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
- After deployment, Cloud Run will give you unique URLs for frontend and backend.
- Set your frontend to use the backend’s URL for API calls (edit `.env` or config before building frontend).

---
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
## 6. (Optional) Use a Custom Domain

- [Map a custom domain to your Cloud Run services](https://cloud.google.com/run/docs/mapping-custom-domains).
- Set up HTTPS automatically with Google-managed certificates.

---

## 7. Clean Up

To avoid charges:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
```bash
gcloud run services delete nvm-web-backend
gcloud run services delete nvm-web-frontend
gcloud artifacts repositories delete nvm-web-repo --location=YOUR_REGION
```

---

## Resources

- [Cloud Run Quickstart](https://cloud.google.com/run/docs/quickstarts)
- [Artifact Registry Quickstart](https://cloud.google.com/artifact-registry/docs/docker/quickstart)
- [Cloud Run Custom Domains](https://cloud.google.com/run/docs/mapping-custom-domains)

---

**You’re ready!** 🚀

1. **Install Docker & Docker Compose**
2. `docker-compose up --build`
3. Visit:
   - Backend: [http://localhost:4000/api/nvm/versions](http://localhost:4000/api/nvm/versions)
   - Frontend: [http://localhost:3000](http://localhost:3000)

_Note: For nvm commands to work, nvm must be installed on the backend container or host. For development, you may want to run backend locally with nvm installed._

## Next Steps

- Add more nvm features (install, uninstall, switch)
- Add authentication
- Improve error handling and UI
- Skip to main content
Firebase
More
Search
/


English
Blog
Studio
Go to console
Sign in
Documentation
Overview
Fundamentals

AI

Build

Run

Reference
Samples
Filter

Here's everything we announced at I/O, from new Firebase Studio features to more ways to integrate AI. Read blog.
Firebase
Documentation
Reference
Was this helpful?

Send feedbackFirebase CLI reference 

bookmark_border


The Firebase CLI (GitHub) provides a variety of tools for managing, viewing, and deploying to Firebase projects.

Before using the Firebase CLI, set up a Firebase project.

Set up or update the CLI
Install the Firebase CLI
You can install the Firebase CLI using a method that matches your operating system, experience level, and/or use case. Regardless of how you install the CLI, you have access to the same functionality and the firebase command.

Windows macOS Linux

Windows
You can install the Firebase CLI for Windows using one of the following options:

Option	Description	Recommended for...
standalone binary	Download the standalone binary for the CLI. Then, you can access the executable to open a shell where you can run the firebase command.	New developers

Developers not using or unfamiliar with Node.js
npm	Use npm (the Node Package Manager) to install the CLI and enable the globally available firebase command.	Developers using Node.js
standalone binary
npm
To download and run the binary for the Firebase CLI, follow these steps:

Download the Firebase CLI binary for Windows.

Access the binary to open a shell where you can run the firebase command.

Continue to log in and test the CLI.

macOS or Linux
You can install the Firebase CLI for macOS or Linux using one of the following options:

Option	Description	Recommended for...
automatic install script	Run a single command that automatically detects your operating system, downloads the latest CLI release, then enables the globally available firebase command.	New developers

Developers not using or unfamiliar with Node.js

Automated deploys in a CI/CD environment
standalone binary	Download the standalone binary for the CLI. Then, you can configure and run the binary to suit your workflow.	Fully customizable workflows using the CLI
npm	Use npm (the Node Package Manager) to install the CLI and enable the globally available firebase command.	Developers using Node.js
auto install script
standalone binary
npm
To install the Firebase CLI using the automatic install script, follow these steps:

Run the following cURL command:

curl -sL https://firebase.tools | bash
This script automatically detects your operating system, downloads the latest Firebase CLI release, then enables the globally available firebase command.

Continue to log in and test the CLI.

For more examples and details about the automatic install script, refer to the script's source code at firebase.tools.

Log in and test the Firebase CLI
After installing the CLI, you must authenticate. Then you can confirm authentication by listing your Firebase projects.

Log into Firebase using your Google account by running the following command:

firebase login
This command connects your local machine to Firebase and grants you access to your Firebase projects.

Note: The firebase login command opens a web page that connects to localhost on your machine. If you're using a remote machine and don't have access to localhost, run the command with the flag --no-localhost.
Note: You can also use the Firebase CLI with CI systems.
Test that the CLI is properly installed and accessing your account by listing your Firebase projects. Run the following command:


firebase projects:list
The displayed list should be the same as the Firebase projects listed in the Firebase console.

Update to the latest CLI version
Generally, you want to use the most up-to-date Firebase CLI version.

In many cases, new features and bug fixes are available only with the latest version of the Firebase CLI. It's a good practice to frequently update the CLI to its latest version.
How you update the CLI version depends on your operating system and how you installed the CLI.

Windows
macOS
Linux
standalone binary: Download the new version, then replace it on your system
npm: Run npm install -g firebase-tools
Use the CLI with CI systems
We recommend that you authenticate using Application Default Credentials when using the CLI with CI systems.

(Recommended) Use Application Default Credentials
The Firebase CLI will detect and use Application Default Credentials if they're set. The simplest way to authenticate the CLI in CI and other headless environments is to set up Application Default Credentials.

(Legacy) Use FIREBASE_TOKEN
Alternatively, you can authenticate using FIREBASE_TOKEN. This is less secure than Application Default Credentials and is no longer recommended.

On a machine with a browser, install the Firebase CLI.

Start the signin process by running the following command:


firebase login:ci
Visit the URL provided, then log in using a Google account.

Print a new refresh token. The current CLI session will not be affected.

Store the output token in a secure but accessible way in your CI system.

Use this token when running firebase commands. You can use either of the following two options:

Option 1: Store the token as the environment variable FIREBASE_TOKEN. Your system will automatically use the token.

Option 2: Run all firebase commands with the --token TOKEN flag in your CI system.
This is the order of precedence for token loading: flag, environment variable, desired Firebase project.

Note: On any machine with the Firebase CLI installed, you can immediately revoke access for the specified token by running the following command: firebase logout --token TOKEN
Initialize a Firebase project
Many common tasks performed using the CLI, such as deploying to a Firebase project, require a project directory. You establish a project directory using the firebase init command. A project directory is usually the same directory as your source control root, and after running firebase init, the directory contains a firebase.json configuration file.

To initialize a new Firebase project, run the following command from within your app's directory:


firebase init
Note: The firebase init command does not create a new directory. If you're starting a new app, you must first make a directory, then run firebase init from within that directory.
The firebase init command steps you through setting up your project directory and some Firebase products. During project initialization, the Firebase CLI asks you to complete the following tasks:

Select a default Firebase project.

This step associates the current project directory with a Firebase project so that project-specific commands (like firebase deploy) run against the appropriate Firebase project.

It's also possible to associate multiple Firebase projects (such as a staging project and a production project) with the same project directory.

Select desired Firebase products to set up in your Firebase project.

This step prompts you to set configurations for specific files for the selected products. For more details on these configurations, refer to the specific product's documentation (for example, Hosting). Note that you can always run firebase init later to set up more Firebase products.

At the end of initialization, Firebase automatically creates the following two files at the root of your local app directory:

A firebase.json configuration file that lists your project configuration.

A .firebaserc file that stores your project aliases.

The firebase.json file
The firebase init command creates a firebase.json configuration file in the root of your project directory.

The firebase.json file is required to deploy assets with the Firebase CLI because it specifies which files and settings from your project directory are deployed to your Firebase project. Since some settings can be defined in either your project directory or the Firebase console, make sure that you resolve any potential deployment conflicts.

You can configure most Firebase Hosting options directly in the firebase.json file. However, for other Firebase services that can be deployed with the Firebase CLI, the firebase init command creates specific files where you can define settings for those services, such as an index.js file for Cloud Functions. You can also set up predeploy or postdeploy hooks in the firebase.json file.

Note: If you run firebase init again for any Firebase service, the command will overwrite the corresponding section of the firebase.json file back to the default configuration for that service.
The following is an example firebase.json file with default settings if you select Firebase Hosting, Cloud Firestore, and Cloud Functions for Firebase (with TypeScript source and lint options selected) during initialization.

([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
{
  "hosting": {
    "public": "public",
    "ignore": [
      "firebase.json",
      "**/.*",
      "**/node_modules/**"
    ]
  },
  "firestore": {
      "rules": "firestore.rules",
      "indexes": "firestore.indexes.json"
  },
  "functions": {
    "predeploy": [
      "npm --prefix \"$RESOURCE_DIR\" run lint",
      "npm --prefix \"$RESOURCE_DIR\" run build"
    ]
  }
}
While firebase.json is used by default, you can pass the --config PATH flag to specify an alternate configuration file.

Configuration for multiple Cloud Firestore databases
When you run firebase init, your firebase.json file will contain a single firestore key corresponding to your project's default database, as shown above.

If your project contains multiple Cloud Firestore databases, edit your firebase.json file to associate different Cloud Firestore Security Rules and database index source files with each database. Modify the file with a JSON array, with one entry for each database.
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
      "firestore": [
        {
          "database": "(default)",
          "rules": "firestore.default.rules",
          "indexes": "firestore.default.indexes.json"
        },
        {
          "database": "ecommerce",
          "rules": "firestore.ecommerce.rules",
          "indexes": "firestore.ecommerce.indexes.json"
        }
      ],
Cloud Functions files to ignore on deploy
At function deployment time, the CLI automatically specifies a list of files in the functions directory to ignore. This prevents deploying to the backend extraneous files that could increase the data size of your deployment.

The list of files ignored by default, shown in JSON format, is:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
"ignore": [
  ".git",
  ".runtimeconfig.json",
  "firebase-debug.log",
  "firebase-debug.*.log",
  "node_modules"
]
If you add your own custom values for ignore in firebase.json, make sure that you keep (or add, if it is missing) the list of files shown above.
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
Manage project aliases
You can associate multiple Firebase projects with the same project directory. For example, you might want to use one Firebase project for staging and another for production. By using different project environments, you can verify changes before deploying to production. The firebase use command allows you to switch between aliases as well as create new aliases.

Add a project alias
When you select a Firebase project during project initialization, the project is automatically assigned the alias of default. However, to allow project-specific commands to run against a different Firebase project but still use the same project directory, run the following command from within your project directory:

firebase use --add
This command prompts you to select another Firebase project and assign the project as alias. Alias assignments are written to a .firebaserc file inside your project directory.

Use project aliases
To use assigned Firebase project aliases, run any of the following commands from within your project directory.

Command	Description
firebase use	View a list of currently defined aliases for your project directory
firebase use \
PROJECT_ID|ALIAS	Directs all commands to run against the specified Firebase project.
The CLI uses this project as the currently "active project".
firebase use --clear	Clears the active project.
Run firebase use PROJECT_ID|ALIAS to set a new active project before running other CLI commands.

firebase use \
--unalias PROJECT_ALIAS	Removes an alias from your project directory.
You can override what's being used as the currently active project by passing the --project flag with any CLI command. As an example: You can set your CLI to run against a Firebase project that you've assigned the staging alias. If you want to run a single command against the Firebase project that you've assigned the prod alias, then you can run, for example, firebase deploy --project=prod.

Source control and project aliases
In general, you should check your .firebaserc file into source control to allow your team to share project aliases. However, for open source projects or starter templates, you should generally not check in your .firebaserc file.

If you have a development project that's for your use only, you can either pass the --project flag with each command or run firebase use PROJECT_ID without assigning an alias to the Firebase project.

Serve and test your Firebase project locally
You can view and test your Firebase project on locally hosted URLs before deploying to production. If you only want to test select features, you can use a comma-separated list in a flag on the firebase serve command.

Run the following command from the root of your local project directory if you want to do either of the following tasks:

View the static content for your Firebase-hosted app.
Use Cloud Functions to generate dynamic content for Firebase Hosting and you want to use your production (deployed) HTTP functions to emulate Hosting on a local URL.
firebase serve --only hosting
Emulate your project using local HTTP functions
Run any of the following commands from your project directory to emulate your project using local HTTP functions.

To emulate HTTP functions and hosting for testing on local URLs, use either of the following commands:

firebase serve
firebase serve --only functions,hosting // uses a flag
To emulate HTTP functions only, use the following command:

firebase serve --only functions
Test from other local devices
By default, firebase serve only responds to requests from localhost. This means that you'll be able to access your hosted content from your computer's web browser but not from other devices on your network. If you'd like to test from other local devices, use the --host flag, like so:

firebase serve --host 0.0.0.0  // accepts requests to any host
Deploy to a Firebase project
The Firebase CLI manages deployment of code and assets to your Firebase project, including:

New releases of your Firebase Hosting sites
New, updated, or existing Cloud Functions for Firebase
New or updated schemas and connectors for Firebase Data Connect
Rules for Firebase Realtime Database
Rules for Cloud Storage for Firebase
Rules for Cloud Firestore
Indexes for Cloud Firestore
To deploy to a Firebase project, run the following command from your project directory:

firebase deploy
You can optionally add a comment to each of your deployments. This comment will display with the other deployment information on your project's Firebase Hosting page. For example:

firebase deploy -m "Deploying the best new feature ever."
When you use the firebase deploy command, be aware of the following:

To deploy resources from a project directory, the project directory must have a firebase.json file. This file is automatically created for you by the firebase init command.

By default, firebase deploy creates a release for all deployable resources in your project directory. To deploy specific Firebase services or features, use partial deployment.

Deployment conflicts for security rules
For Firebase Realtime Database, Cloud Storage for Firebase, and Cloud Firestore, you can define security rules either in your local project directory or in the Firebase console.

Note: When you deploy security rules using the Firebase CLI, the rules defined in your project directory overwrite any existing rules in the Firebase console. So, if you choose to define or edit your security rules using the Firebase console, make sure that you also update the rules defined in your project directory.
Another option to avoid deployment conflicts is to use partial deployment and only define rules in the Firebase console.

Deployment quotas
It's possible (though unlikely) that you might exceed a quota that limits the rate or volume of your Firebase deployment operations. For example, when deploying very large numbers of functions, you might receive an HTTP 429 Quota error message. To solve such issues, try using partial deployment.

Roll back a deployment
You can roll back a Firebase Hosting deployment from your project's Firebase Hosting page by selecting the Rollback action for the desired release.

It's not currently possible to roll back releases of security rules for Firebase Realtime Database, Cloud Storage for Firebase, or Cloud Firestore.

Deploy specific Firebase services
If you only want to deploy specific Firebase services or features, you can use a comma-separated list in a flag on the firebase deploy command. For example, the following command deploys Firebase Hosting content and Cloud Storage security rules.

firebase deploy --only hosting,storage
The following table lists the services and features available for partial deployment. The names in the flags correspond to the keys in your firebase.json configuration file.

Flag syntax	Service or feature deployed
--only hosting	Firebase Hosting content
--only database	Firebase Realtime Database rules
--only dataconnect	Firebase Data Connect schemas and connectors
--only storage	Cloud Storage for Firebase rules
--only firestore	Cloud Firestore rules and indexes for all configured databases
--only functions	Cloud Functions for Firebase (more specific versions of this flag are possible)
Note: The --only rules syntax used by older versions of the CLI is deprecated.
Deploy specific functions
When deploying functions, you can target specific functions. For example:

firebase deploy --only functions:function1
firebase deploy --only functions:function1,functions:function2
Another option is to group functions into export groups in your /functions/index.js file. Grouping functions allows you to deploy multiple functions using a single command.

For example, you can write the following functions to define a groupA and a groupB:
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
var functions = require('firebase-functions/v1');

exports.groupA = {
  function1: functions.https.onRequest(...),
  function2: functions.database.ref('\path').onWrite(...)
}
exports.groupB = require('./groupB');
In this example, a separate functions/groupB.js file contains additional functions that specifically define the functions in groupB. For example:

var functions = require('firebase-functions/v1');

exports.function3 = functions.storage.object().onChange(...);
exports.function4 = functions.analytics.event('in_app_purchase').onLog(...);
In this example, you can deploy all the groupA functions by running the following command from your project directory:

firebase deploy --only functions:groupA
Or you can target a specific function within a group by running the following command:

firebase deploy --only functions:groupA.function1,groupB.function4
Important: To avoid running to quota errors and other server errors, limit function group size to 10 or fewer for each deployment operation.
Delete functions
The Firebase CLI supports the following commands and options for deleting previously deployed functions:

Deletes all functions that match the specified name in all regions:

firebase functions:delete FUNCTION-1_NAME
Deletes a specified function running in a non-default region:

firebase functions:delete FUNCTION-1_NAME --region REGION_NAME
Deletes more than one function:

firebase functions:delete FUNCTION-1_NAME FUNCTION-2_NAME
Deletes a specified functions group:

firebase functions:delete GROUP_NAME
Bypasses the confirmation prompt:

firebase functions:delete FUNCTION-1_NAME --force
Set up predeploy and postdeploy scripted tasks
You can connect shell scripts to the firebase deploy command to perform predeploy or postdeploy tasks. For example, a predeploy script could transpile TypeScript code into JavaScript, and a postdeploy hook could notify administrators of new site content deploys to Firebase Hosting.

To set up predeploy or postdeploy hooks, add bash scripts to your firebase.json configuration file. You can define brief scripts directly in the firebase.json file, or you can reference other files that are in your project directory.

For example, the following script is the firebase.json expression for a postdeploy task that sends a Slack message upon successful deployment to Firebase Hosting.
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
"hosting": {
  // ...

  "postdeploy": "./messageSlack.sh 'Just deployed to Firebase Hosting'",
  "public": "public"
}
The messageSlack.sh script file resides in the project directory and looks like this:

curl -X POST -H 'Content-type: application/json' --data '{"text":"$1"}'
     \https://SLACK_WEBHOOK_URL
You can set up predeploy and postdeploy hooks for any of the assets that you can deploy. Note that running firebase deploy triggers all the predeploy and postdeploy tasks defined in your firebase.json file. To run only those tasks associated with a specific Firebase service, use partial deployment commands.

Both predeploy and postdeploy hooks print the standard output and error streams of the scripts to the terminal. For failure cases, note the following:

If a predeploy hook fails to complete as expected, deployment is canceled.
If deployment fails for any reason, postdeploy hooks are not triggered.
Environment variables
Within scripts running in the predeploy and postdeploy hooks, the following environment variables are available:

$GCLOUD_PROJECT: The active project's project ID
$PROJECT_DIR: The root directory containing the firebase.json file
$RESOURCE_DIR: (For hosting and functions scripts only) The location of the directory that contains the Hosting or Cloud Functions resources to be deployed
Manage multiple Realtime Database instances
A Firebase project can have multiple Firebase Realtime Database instances. By default, CLI commands interact with your default database instance.

However, you can interact with a non-default database instance by using the --instance DATABASE_NAME flag. The following commands support the --instance flag:

firebase database:get
firebase database:profile
firebase database:push
firebase database:remove
firebase database:set
firebase database:update
Command reference
CLI administrative commands
Command	Description
help	Displays help information about the CLI or specific commands.
init	Associates and sets up a new Firebase project in the current directory. This command creates a firebase.json configuration file in the current directory.
login	Authenticates the CLI with your Google Account. Requires access to a web browser.
To log into the CLI in remote environments that don't allow access to localhost, use the --no-localhost flag.
login:ci	Generates an authentication token for use in non-interactive environments.
logout	Signs out your Google Account from the CLI.
open	Opens a browser to relevant project resources.
projects:list	Lists all the Firebase projects to which you have access.
use	Sets the active Firebase project for the CLI.
Manages project aliases.
Project management commands
Command	Description
Management of Firebase projects
projects:addfirebase	Adds Firebase resources to an existing Google Cloud project.
projects:create	Creates a new Google Cloud project, then adds Firebase resources to the new project.
projects:list	Lists all the Firebase projects to which you have access.
Management of Firebase Apps (iOS, Android, Web)
apps:create	Creates a new Firebase App in the active project.
apps:list	Lists the registered Firebase Apps in the active project.
apps:sdkconfig	Prints the Google services configuration of a Firebase App.
setup:web	Deprecated. Instead, use apps:sdkconfig and specify web as the platform argument.
Prints the Google services configuration of a Firebase Web App.
Management of SHA certificate hashes (Android only)
apps:android:sha:create \
FIREBASE_APP_ID SHA_HASH	Adds the specified SHA certificate hash to the specified Firebase Android App.
apps:android:sha:delete \
FIREBASE_APP_ID SHA_HASH	Deletes the specified SHA certificate hash from the specified Firebase Android App.
apps:android:sha:list \
FIREBASE_APP_ID	Lists the SHA certificate hashes for the specified Firebase Android App.
Deployment and local development
These commands let you deploy and interact with your Firebase Hosting site.

Command	Description
deploy	Deploys code and assets from your project directory to the active project. For Firebase Hosting, a firebase.json configuration file is required.
serve	Starts a local web server with your Firebase Hosting configuration. For Firebase Hosting, a firebase.json configuration file is required.
App Distribution commands
Command	Description
appdistribution:distribute \
--app FIREBASE_APP_ID	Makes the build available to testers.
appdistribution:testers:add	Adds testers to the project.
appdistribution:testers:remove	Removes testers from the project.
App Hosting commands
Command	Description
apphosting:backends:create \
--project PROJECT_ID \
--location REGION --app APP_ID	Creates the collection of managed resources linked to a single codebase that comprises an App Hosting backend. Optionally specify an existing Firebase Web app by its Firebase app ID.
apphosting:backends:get \
BACKEND_ID \
--project PROJECT_ID \
--location REGION	Retrieves specific details, including the public URL, of a backend.
apphosting:backends:list \
--project PROJECT_ID	Retrieves a list of all active backends associated with a project.
firebase apphosting:backends:delete \
BACKEND_ID \
--project PROJECT_ID \
--location REGION	Deletes a backend from the project.
firebase apphosting:config:export \
--project PROJECT_ID \
--secrets ENVIRONMENT_NAME	Exports secrets for use in app emulation.
Defaults to secrets stored in apphosting.yaml, or takes --secrets to specify any environment that has a corresponding apphosting.ENVIRONMENT_NAME.yaml file.
firebase apphosting:rollouts:create \
BACKEND_ID \
--git_branch BRANCH_NAME \
--git_commit COMMIT_ID	Creates a manually triggered rollout.
Optionally specify the latest commit to a branch or a specific commit. If no options are provided, prompts selection from a list of branches.
apphosting:secrets:set KEY --project PROJECT_ID \
--location REGION \
--data-file DATA_FILE_PATH	Stores secret material in Secret Manager.
Optionally provide a file path from which to read secret data. Set to _ to read secret data from standard input.
apphosting:secrets:grantaccess KEY BACKEND_ID \
--project PROJECT_ID \
--location REGION	Grants the backend service account access to the provided secret so that it can be accessed by App Hosting at build or run time.
apphosting:secrets:describe KEY \
--project PROJECT_ID	Gets the metadata for a secret and its versions.
firebase apphosting:secrets:access \
KEY[@version] \
--project PROJECT_ID	Accesses a secret value given the secret and its version. Defaults to accessing the latest version.
Authentication (user management) commands
Command	Description
auth:export	Exports the active project's user accounts to a JSON or CSV file. For more details, refer to the auth:import and auth:export page.
auth:import	Imports the user accounts from a JSON or CSV file into the active project. For more details, refer to the auth:import and auth:export page.
Cloud Firestore commands
Command	Description
firestore:locations	
List available locations for your Cloud Firestore database.

firestore:databases:create DATABASE_ID	
Create a database instance in native mode in your Firebase project.

The command takes the following flags:

--location <region name> to specify the deployment location for the database. Note you can run firebase firestore:locations to list available locations. Required.
--delete-protection <deleteProtectionState> to allow or prevent deletion of the specified database. Valid values are ENABLED or DISABLED. Defaults to DISABLED.
--point-in-time-recovery <PITRState> to set whether point-in-time recovery is enabled. Valid values are ENABLED or DISABLED. Defaults to DISABLED. Optional.
firestore:databases:list	
List databases in your Firebase project.

firestore:databases:get DATABASE_ID	
Get database configuration for a specified database in your Firebase project.

firestore:databases:update DATABASE_ID	
Update database configuration of a specified database in your Firebase project.

At least one flag is required. The command takes the following flags:

--delete-protection <deleteProtectionState> to allow or prevent deletion of the specified database. Valid values are ENABLED or DISABLED. Defaults to DISABLED.
--point-in-time-recovery <PITRState> to set whether point-in-time recovery is enabled. Valid values are ENABLED or DISABLED. Defaults to DISABLED. Optional.
firestore:databases:delete DATABASE_ID	
Delete a database in your Firebase project.

firestore:indexes	
List indexes for a database in your Firebase project.

The command takes the following flag:

--database DATABASE_ID to specify the name of the database for which to list indexes. If not provided, indexes are listed for the default database.
firestore:delete	
Deletes documents in the active project's database. Using the CLI, you can recursively delete all the documents in a collection.

Note that deleting Cloud Firestore data with the CLI incurs read and delete costs. For more information, see Understand Cloud Firestore billing.

The command takes the following flag:

--database DATABASE_ID to specify the name of the database from which documents are deleted. If not specified, documents are deleted from the default database. Optional.
Cloud Functions for Firebase commands
Command	Description
functions:config:clone	Clones another project's environment into the active Firebase project.
functions:config:get	Retrieves existing configuration values of the active project's Cloud Functions.
functions:config:set	Stores runtime configuration values of the active project's Cloud Functions.
functions:config:unset	Removes values from the active project's runtime configuration.
functions:log	Reads logs from deployed Cloud Functions.
For more information, refer to the environment configuration documentation.

Crashlytics commands
Command	Description
crashlytics:mappingfile:generateid \
--resource-file=PATH/TO/ANDROID_RESOURCE.XML	Generates a unique mapping file ID in the specified Android resource (XML) file.
crashlytics:mappingfile:upload \
--app=FIREBASE_APP_ID \
--resource-file=PATH/TO/ANDROID_RESOURCE.XML \
PATH/TO/MAPPING_FILE.TXT	Uploads a Proguard-compatible mapping (TXT) file for this app, and associates it with the mapping file ID declared in the specified Android resource (XML) file.
crashlytics:symbols:upload \
--app=FIREBASE_APP_ID \
PATH/TO/SYMBOLS	Generates a Crashlytics-compatible symbol file for native library crashes on Android and uploads it to Firebase servers.
Data Connect commands
These commands and their use cases are covered in more detail in the Data Connect CLI reference guide.

Command	Description
dataconnect:services:list	Lists all deployed Data Connect services in your Firebase project.
dataconnect:sql:diff \
SERVICE_ID	For the specified service, displays the differences between a local Data Connect schema and your Cloud SQL database schema.
dataconnect:sql:migrate \
--force \
SERVICE_ID	Migrates your Cloud SQL database's schema to match your local Data Connect schema.
dataconnect:sql:grant\
--role=ROLE \
--email=EMAIL \
SERVICE_ID	Grants the SQL role to the specified user or service account email.
For the --role flag, the SQL role to grant is one of: owner, writer, or reader.
For the --email flag, provide the email address of the user or service account to grant the role to.
dataconnect:sdk:generate	Generates typed SDKs for your Data Connect connectors.
Extensions commands
Command	Description
ext	Displays information on how to use Firebase Extensions commands.
Lists the extension instances installed in the active project.
ext:configure \
EXTENSION_INSTANCE_ID	Reconfigures the parameter values of an extension instance in your extension manifest.
ext:info \
PUBLISHER_ID/EXTENSION_ID	Prints detailed information about an extension.
ext:install \
PUBLISHER_ID/EXTENSION_ID	Adds a new instance of an extension into your extension manifest.
ext:list	Lists all the extension instances installed in a Firebase project.
Prints the instance ID for each extension.
ext:uninstall \
EXTENSION_INSTANCE_ID	Removes an extension instance from your extension manifest.
ext:update \
EXTENSION_INSTANCE_ID	Updates an extension instance to the latest version in your extension manifest.
ext:export	Exports all installed extension instances from your project to your extension manifest.
Extensions publisher commands
Command	Description
ext:dev:init	Initializes a skeleton codebase for a new extension in the current directory.
ext:dev:list \
PUBLISHER_ID	Prints a list of all extensions uploaded by a publisher.
ext:dev:register	Registers a Firebase project as an extensions publisher project.
ext:dev:deprecate \
PUBLISHER_ID/EXTENSION_ID \
VERSION_PREDICATE	Deprecates extension versions that match the version predicate.
A version predicate can be a single version (such as 1.0.0), or a range of versions (such as >1.0.0).
If no version predicate is provided, deprecates all versions of that extension.
ext:dev:undeprecate \
PUBLISHER_ID/EXTENSION_ID \
VERSION_PREDICATE	Undeprecates extension versions that match the version predicate.
A version predicate can be a single version (such as 1.0.0), or a range of versions (such as >1.0.0).
If no version predicate is provided, undeprecates all versions of that extension.
ext:dev:upload \
PUBLISHER_ID/EXTENSION_ID	Uploads a new version of an extension.
ext:dev:usage \
PUBLISHER_ID	Displays install counts and usage metrics for extensions uploaded by a publisher.
Hosting commands
Command	Description
hosting:disable	
Stops serving Firebase Hosting traffic for the active Firebase project.

Your project's Hosting URL will display a "Site Not Found" message after running this command.

Management of Hosting sites
firebase hosting:sites:create \
SITE_ID	
Creates a new Hosting site in the active Firebase project using the specified SITE_ID

(Optional) Specify an existing Firebase Web App to associate with the new site by passing the following flag: --app FIREBASE_APP_ID

firebase hosting:sites:delete \
SITE_ID	
Deletes the specified Hosting site

The CLI displays a confirmation prompt before deleting the site.

(Optional) Skip the confirmation prompt by passing the following flags: -f or --force

firebase hosting:sites:get \
SITE_ID	
Retrieves information about the specified Hosting site

firebase hosting:sites:list	
Lists all Hosting sites for the active Firebase project

Management of preview channels
firebase hosting:channel:create \
CHANNEL_ID	
Creates a new preview channel in the default Hosting site using the specified CHANNEL_ID

This command does not deploy to the channel.

firebase hosting:channel:delete \
CHANNEL_ID	
Deletes the specified preview channel

You cannot delete a site's live channel.

firebase hosting:channel:deploy \
CHANNEL_ID	
Deploys your Hosting content and config to the specified preview channel

If the preview channel does not yet exist, this command creates the channel in the default Hosting site before deploying to the channel.

firebase hosting:channel:list	Lists all channels (including the "live" channel) in the default Hosting site
firebase hosting:channel:open \
CHANNEL_ID	Opens a browser to the specified channel's URL or returns the URL if opening in a browser isn't possible
Version cloning
firebase hosting:clone \
SOURCE_SITE_ID:SOURCE_CHANNEL_ID \
TARGET_SITE_ID:TARGET_CHANNEL_ID	
Clones the most recently deployed version on the specified "source" channel to the specified "target" channel

This command also deploys to the specified "target" channel. If the "target" channel does not yet exist, this command creates a new preview channel in the "target" Hosting site before deploying to the channel.

firebase hosting:clone \
SOURCE_SITE_ID:@VERSION_ID \
TARGET_SITE_ID:TARGET_CHANNEL_ID	
Clones the specified version to the specified "target" channel

This command also deploys to the specified "target" channel. If the "target" channel does not yet exist, this command creates a new preview channel in the "target" Hosting site before deploying to the channel.

You can find the VERSION_ID in the Hosting dashboard of the Firebase console.

Realtime Database commands
Note that you can create your initial, default Realtime Database instance in the Firebase console or by using the general firebase init workflow or the specific firebase init database flow.

Once instances are created, you can manage them as discussed in Manage multiple Realtime Database instances.

Command	Description
database:get	Fetches data from the active project's database and displays it as JSON. Supports querying on indexed data.
database:instances:create	Creates a database instance with a specified instance name. Accepts the --location option for creating a database in a specified region. For region names to use with this option, see select locations for your project. If no database instance exists for the current project, you are prompted to run the firebase init flow to create an instance.
database:instances:list	List all database instances for this project. Accepts the --location option for listing databases in a specified region. For region names to use with this option see select locations for your project.
database:profile	Builds a profile of operations on the active project's database. For more details, refer to Realtime Database operation types.
database:push	Pushes new data to a list at a specified location in the active project's database. Takes input from a file, STDIN, or a command-line argument.
database:remove	Deletes all data at a specified location in the active project's database.
database:set	Replaces all data at a specified location in the active project's database. Takes input from a file, STDIN, or a command-line argument.
database:update	Performs a partial update at a specified location in the active project's database. Takes input from a file, STDIN, or a command-line argument.
Remote Config commands
Command	Description
remoteconfig:versions:list \
--limit NUMBER_OF_VERSIONS	Lists the most recent ten versions of the template. Specify 0 to return all existing versions, or optionally pass the --limit option to limit the number of versions being returned.
remoteconfig:get \
--v, version_number VERSION_NUMBER
--o, output FILENAME	Gets the template by version (defaults to the latest version) and outputs the parameter groups, parameters, and condition names and version into a table. Optionally, you can write the output to a specified file with -o, FILENAME.
remoteconfig:rollback \
--v, version_number VERSION_NUMBER
--force	Rolls back Remote Config template to a specified previous version number or defaults to the immediate previous version (current version -1). Unless --force is passed, prompts Y/N before proceeding to rollback.
Send feedback
Except as otherwise noted, the content of this page is licensed under the Creative Commons Attribution 4.0 License, and code samples are licensed under the Apache 2.0 License. For details, see the Google Developers Site Policies. Java is a registered trademark of Oracle and/or its affiliates.

Last updated 2025-06-04 UTC.

Learn
Developer guides
SDK & API reference
Samples
Libraries
GitHub
Stay connected
Check out the blog
Find us on Reddit
Follow on X
Subscribe on YouTube
Attend an event
Support
Contact support
Stack Overflow
Slack community
Google group
Release notes
Brand guidelines
FAQs
Google Developers
Android
Chrome
Firebase
Google Cloud Platform
All products
Terms
Privacy

English

skip to:contentpackage searchsign in
❤
Pro
Teams
Pricing
Documentation
npm
Search packages
Search
firebase
TypeScript icon, indicating that this package has built-in type declarations
11.9.1 • Public • Published 4 days ago
Build Status Version Coverage Status

Firebase - App success made simple
Upgrade to Version 9
Version 9 has a redesigned API that supports tree-shaking. Read the Upgrade Guide to learn more.

Overview
Firebase provides the tools and infrastructure you need to develop, grow, and earn money from your app. This package supports web (browser), mobile-web, and server (Node.js) clients.

For more information, visit:

Firebase Realtime Database - The Firebase Realtime Database lets you store and query user data, and makes it available between users in realtime.
Cloud Firestore - Cloud Firestore is a flexible, scalable database for mobile, web, and server development from Firebase and Google Cloud Platform.
Firebase Storage - Firebase Storage lets you upload and store user generated content, such as files, and images.
Cloud Functions for Firebase - Cloud Functions for Firebase is a serverless framework that lets you automatically run backend code in response to events triggered by Firebase features and HTTPS requests.
Firebase Cloud Messaging - Firebase Cloud Messaging is a cross-platform messaging solution that lets you reliably deliver messages at no cost.
Firebase Performance Monitoring - Firebase Performance Monitoring helps you gain insight into your app's performance issues.
Google Analytics - Google Analytics is a free app measurement solution that provides insight on app usage and user engagement.
Remote Config - Firebase Remote Config is a cloud service that lets you change the behavior and appearance of your app without requiring users to reload your app.
App Check - App Check helps protect your backend resources from abuse, such as billing fraud and phishing. It works with both Firebase services and your own backends to keep your resources safe.
Create and setup your account - Get started using Firebase for free.
This SDK is intended for end-user client access from environments such as the Web, mobile Web (e.g. React Native, Ionic), Node.js desktop (e.g. Electron), or IoT devices running Node.js. If you are instead interested in using a Node.js SDK which grants you admin access from a privileged environment (like a server), you should use the Firebase Admin Node.js SDK.

Install the SDK
Install the Firebase NPM module:

$ npm init
$ npm install --save firebase
import { initializeApp } from 'firebase/app';

// TODO: Replace the following with your app's Firebase project configuration
const firebaseConfig = {
  //...
};

const app = initializeApp(firebaseConfig);
Access Firebase services in your app
Firebase services (like Cloud Firestore, Authentication, Realtime Database, Remote Config, and more) are available to import within individual sub-packages.

The example below shows how you could use the Cloud Firestore Lite SDK to retrieve a list of data.
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
import { initializeApp } from 'firebase/app';
import { getFirestore, collection, getDocs } from 'firebase/firestore/lite';
// Follow this pattern to import other Firebase services
// import { } from 'firebase/<service>';

// TODO: Replace the following with your app's Firebase project configuration
const firebaseConfig = {
  //...
};

const app = initializeApp(firebaseConfig);
const db = getFirestore(app);

// Get a list of cities from your database
async function getCities(db) {
  const citiesCol = collection(db, 'cities');
  const citySnapshot = await getDocs(citiesCol);
  const cityList = citySnapshot.docs.map(doc => doc.data());
  return cityList;
}
Use a module bundler for size reduction
The Firebase Web SDK is designed to work with module bundlers to remove any unused code (tree-shaking). We strongly recommend using this approach for production apps. Tools such as the Angular CLI, Next.js, Vue CLI, or Create React App automatically handle module bundling for libraries installed through npm and imported into your codebase.

See Using module bundlers with Firebase for more information.

Script include
You can also load Firebase packages as script modules in browsers that support native ES modules.

<!-- use script module by specifying type="module" -->
<script type="module">
    import { initializeApp } from 'https://www.gstatic.com/firebasejs/${FIREBASE_VERSION}/firebase-app.js';
    import { getFirestore, collection, getDocs } from 'https://www.gstatic.com/firebasejs/${FIREBASE_VERSION}/firebase-firestore-lite.js';
    // Follow this pattern to import other Firebase services
    // import {} from "https://www.gstatic.com/firebasejs/${FIREBASE_VERSION}/firebase-analytics.js";
    // import {} from "https://www.gstatic.com/firebasejs/${FIREBASE_VERSION}/firebase-app-check.js";
    // import {} from "https://www.gstatic.com/firebasejs/${FIREBASE_VERSION}/firebase-auth.js";
    // import {} from "https://www.gstatic.com/firebasejs/${FIREBASE_VERSION}/firebase-functions.js";
    // import {} from "https://www.gstatic.com/firebasejs/${FIREBASE_VERSION}/firebase-firestore.js";
    // import {} from "https://www.gstatic.com/firebasejs/${FIREBASE_VERSION}/firebase-storage.js";
    // import {} from "https://www.gstatic.com/firebasejs/${FIREBASE_VERSION}/firebase-performance.js";
    // import {} from "https://www.gstatic.com/firebasejs/${FIREBASE_VERSION}/firebase-remote-config.js";
    // import {} from "https://www.gstatic.com/firebasejs/${FIREBASE_VERSION}/firebase-messaging.js";
    // import {} from "https://www.gstatic.com/firebasejs/${FIREBASE_VERSION}/firebase-database.js";
    
    // TODO: Replace the following with your app's Firebase project configuration
    const firebaseConfig = {
    //...
    };

    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);

    // Get a list of cities from your database
    async function getCities(db) {
    const citiesCol = collection(db, 'cities');
    const citySnapshot = await getDocs(citiesCol);
    const cityList = citySnapshot.docs.map(doc => doc.data());
    return cityList;
    }
</script>
Note: To get a filled in version of the above code snippet, go to the Firebase console for your app and click on "Add Firebase to your web app".

Get the code (Node.js - server and command line)
Install the SDK
While you can write entire Firebase applications without any backend code, many developers want to write server applications or command-line utilities using the Node.js JavaScript runtime.

You can use the same npm module to use Firebase in the Node.js runtime (on a server or running from the command line):

$ npm init
$ npm install --save firebase
In your code, you can access Firebase using:

const { initializeApp } = require('firebase/app');
const { getFirestore, collection, getDocs } = require('firebase/firestore');
// ...
If you are using native ES6 module with --experimental-modules flag (or Node 12+) you should do:

import { initializeApp } from 'firebase/app';
import { getFirestore, collection, getDocs } from 'firebase/firestore';
// ...
Please see Environment Support for which packages are available in Node.js.

Compat packages
Version 9 provides a set of compat packages that are API compatible with Version 8. They are intended to be used to make the upgrade to the modular API easier by allowing you to upgrade your app piece by piece. See the Upgrade Guide for more detail.

To access the compat packages, use the subpath compat like so:

// v9 compat packages are API compatible with v8 code
import firebase from 'firebase/compat/app';
import 'firebase/compat/auth';
import 'firebase/compat/firestore';
Changelog
The Firebase changelog can be found at firebase.google.com.

Browser/environment compatibility
Please see Environment Support.

Readme
Keywords
authenticationdatabaseFirebasefirebaserealtimestorageperformanceremote-config
Package Sidebar
Install
npm i firebase

Repository
github.com/firebase/firebase-js-sdk

Homepage
firebase.google.com/

Weekly Downloads
2,822,766

Version
11.9.1

License
Apache-2.0

Unpacked Size
25.9 MB

Total Files
2756

Last publish
21 hours ago

Collaborators
firebase-ops
feiyang.chen
google-wombot
chholland
Try on RunKit
Report malware
Footer
Support
Help
Advisories
Status
Contact npm
Company
About
Blog
Press
Terms & Policies
Policies
Terms of Use
Code of Conduct
Privacy

Skip to main content
Firebase
More
Search
/


English
Blog
Studio
Go to console

Documentation
Overview
Fundamentals

AI

Build

Run

Test Lab
App Distribution
Crashlytics
Performance Monitoring
Remote Config
A/B Testing
Analytics
Cloud Messaging
In-App Messaging
Dynamic Links
Google AdMob
Google Ads
Reference
Samples
Filter

Here's everything we announced at I/O, from new Firebase Studio features to more ways to integrate AI. Read blog.
Firebase
Documentation
Reference
Was this helpful?

Send feedbackFirebase CLI reference 

bookmark_border


The Firebase CLI (GitHub) provides a variety of tools for managing, viewing, and deploying to Firebase projects.

Before using the Firebase CLI, set up a Firebase project.

Set up or update the CLI
Install the Firebase CLI
You can install the Firebase CLI using a method that matches your operating system, experience level, and/or use case. Regardless of how you install the CLI, you have access to the same functionality and the firebase command.

Windows macOS Linux

Windows
You can install the Firebase CLI for Windows using one of the following options:

Option	Description	Recommended for...
standalone binary	Download the standalone binary for the CLI. Then, you can access the executable to open a shell where you can run the firebase command.	New developers

Developers not using or unfamiliar with Node.js
npm	Use npm (the Node Package Manager) to install the CLI and enable the globally available firebase command.	Developers using Node.js
standalone binary
npm
To download and run the binary for the Firebase CLI, follow these steps:

Download the Firebase CLI binary for Windows.

Access the binary to open a shell where you can run the firebase command.

Continue to log in and test the CLI.

macOS or Linux
You can install the Firebase CLI for macOS or Linux using one of the following options:

Option	Description	Recommended for...
automatic install script	Run a single command that automatically detects your operating system, downloads the latest CLI release, then enables the globally available firebase command.	New developers

Developers not using or unfamiliar with Node.js

Automated deploys in a CI/CD environment
standalone binary	Download the standalone binary for the CLI. Then, you can configure and run the binary to suit your workflow.	Fully customizable workflows using the CLI
npm	Use npm (the Node Package Manager) to install the CLI and enable the globally available firebase command.	Developers using Node.js
auto install script
standalone binary
npm
To install the Firebase CLI using the automatic install script, follow these steps:

Run the following cURL command:

curl -sL https://firebase.tools | bash
This script automatically detects your operating system, downloads the latest Firebase CLI release, then enables the globally available firebase command.

Continue to log in and test the CLI.

For more examples and details about the automatic install script, refer to the script's source code at firebase.tools.

Log in and test the Firebase CLI
After installing the CLI, you must authenticate. Then you can confirm authentication by listing your Firebase projects.

Log into Firebase using your Google account by running the following command:

firebase login
This command connects your local machine to Firebase and grants you access to your Firebase projects.

Note: The firebase login command opens a web page that connects to localhost on your machine. If you're using a remote machine and don't have access to localhost, run the command with the flag --no-localhost.
Note: You can also use the Firebase CLI with CI systems.
Test that the CLI is properly installed and accessing your account by listing your Firebase projects. Run the following command:


firebase projects:list
The displayed list should be the same as the Firebase projects listed in the Firebase console.

Update to the latest CLI version
Generally, you want to use the most up-to-date Firebase CLI version.

In many cases, new features and bug fixes are available only with the latest version of the Firebase CLI. It's a good practice to frequently update the CLI to its latest version.
How you update the CLI version depends on your operating system and how you installed the CLI.

Windows
macOS
Linux
standalone binary: Download the new version, then replace it on your system
npm: Run npm install -g firebase-tools
Use the CLI with CI systems
We recommend that you authenticate using Application Default Credentials when using the CLI with CI systems.

(Recommended) Use Application Default Credentials
The Firebase CLI will detect and use Application Default Credentials if they're set. The simplest way to authenticate the CLI in CI and other headless environments is to set up Application Default Credentials.

(Legacy) Use FIREBASE_TOKEN
Alternatively, you can authenticate using FIREBASE_TOKEN. This is less secure than Application Default Credentials and is no longer recommended.

On a machine with a browser, install the Firebase CLI.

Start the signin process by running the following command:


firebase login:ci
Visit the URL provided, then log in using a Google account.

Print a new refresh token. The current CLI session will not be affected.

Store the output token in a secure but accessible way in your CI system.

Use this token when running firebase commands. You can use either of the following two options:

Option 1: Store the token as the environment variable FIREBASE_TOKEN. Your system will automatically use the token.

Option 2: Run all firebase commands with the --token TOKEN flag in your CI system.
This is the order of precedence for token loading: flag, environment variable, desired Firebase project.

Note: On any machine with the Firebase CLI installed, you can immediately revoke access for the specified token by running the following command: firebase logout --token TOKEN
Initialize a Firebase project
Many common tasks performed using the CLI, such as deploying to a Firebase project, require a project directory. You establish a project directory using the firebase init command. A project directory is usually the same directory as your source control root, and after running firebase init, the directory contains a firebase.json configuration file.

To initialize a new Firebase project, run the following command from within your app's directory:


firebase init
Note: The firebase init command does not create a new directory. If you're starting a new app, you must first make a directory, then run firebase init from within that directory.
The firebase init command steps you through setting up your project directory and some Firebase products. During project initialization, the Firebase CLI asks you to complete the following tasks:

Select a default Firebase project.

This step associates the current project directory with a Firebase project so that project-specific commands (like firebase deploy) run against the appropriate Firebase project.

It's also possible to associate multiple Firebase projects (such as a staging project and a production project) with the same project directory.

Select desired Firebase products to set up in your Firebase project.

This step prompts you to set configurations for specific files for the selected products. For more details on these configurations, refer to the specific product's documentation (for example, Hosting). Note that you can always run firebase init later to set up more Firebase products.

At the end of initialization, Firebase automatically creates the following two files at the root of your local app directory:

A firebase.json configuration file that lists your project configuration.

A .firebaserc file that stores your project aliases.

The firebase.json file
The firebase init command creates a firebase.json configuration file in the root of your project directory.

The firebase.json file is required to deploy assets with the Firebase CLI because it specifies which files and settings from your project directory are deployed to your Firebase project. Since some settings can be defined in either your project directory or the Firebase console, make sure that you resolve any potential deployment conflicts.

You can configure most Firebase Hosting options directly in the firebase.json file. However, for other Firebase services that can be deployed with the Firebase CLI, the firebase init command creates specific files where you can define settings for those services, such as an index.js file for Cloud Functions. You can also set up predeploy or postdeploy hooks in the firebase.json file.

Note: If you run firebase init again for any Firebase service, the command will overwrite the corresponding section of the firebase.json file back to the default configuration for that service.
The following is an example firebase.json file with default settings if you select Firebase Hosting, Cloud Firestore, and Cloud Functions for Firebase (with TypeScript source and lint options selected) during initialization.

([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
{
  "hosting": {
    "public": "public",
    "ignore": [
      "firebase.json",
      "**/.*",
      "**/node_modules/**"
    ]
  },
  "firestore": {
      "rules": "firestore.rules",
      "indexes": "firestore.indexes.json"
  },
  "functions": {
    "predeploy": [
      "npm --prefix \"$RESOURCE_DIR\" run lint",
      "npm --prefix \"$RESOURCE_DIR\" run build"
    ]
  }
}
While firebase.json is used by default, you can pass the --config PATH flag to specify an alternate configuration file.

Configuration for multiple Cloud Firestore databases
When you run firebase init, your firebase.json file will contain a single firestore key corresponding to your project's default database, as shown above.

If your project contains multiple Cloud Firestore databases, edit your firebase.json file to associate different Cloud Firestore Security Rules and database index source files with each database. Modify the file with a JSON array, with one entry for each database.

([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
      "firestore": [
        {
          "database": "(default)",
          "rules": "firestore.default.rules",
          "indexes": "firestore.default.indexes.json"
        },
        {
          "database": "ecommerce",
          "rules": "firestore.ecommerce.rules",
          "indexes": "firestore.ecommerce.indexes.json"
        }
      ],
Cloud Functions files to ignore on deploy
At function deployment time, the CLI automatically specifies a list of files in the functions directory to ignore. This prevents deploying to the backend extraneous files that could increase the data size of your deployment.

The list of files ignored by default, shown in JSON format, is:

([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
"ignore": [
  ".git",
  ".runtimeconfig.json",
  "firebase-debug.log",
  "firebase-debug.*.log",
  "node_modules"
]
If you add your own custom values for ignore in firebase.json, make sure that you keep (or add, if it is missing) the list of files shown above.

Manage project aliases
You can associate multiple Firebase projects with the same project directory. For example, you might want to use one Firebase project for staging and another for production. By using different project environments, you can verify changes before deploying to production. The firebase use command allows you to switch between aliases as well as create new aliases.

Add a project alias
When you select a Firebase project during project initialization, the project is automatically assigned the alias of default. However, to allow project-specific commands to run against a different Firebase project but still use the same project directory, run the following command from within your project directory:


firebase use --add
This command prompts you to select another Firebase project and assign the project as alias. Alias assignments are written to a .firebaserc file inside your project directory.

Use project aliases
To use assigned Firebase project aliases, run any of the following commands from within your project directory.

Command	Description
firebase use	View a list of currently defined aliases for your project directory
firebase use \
PROJECT_ID|ALIAS	Directs all commands to run against the specified Firebase project.
The CLI uses this project as the currently "active project".
firebase use --clear	Clears the active project.
Run firebase use PROJECT_ID|ALIAS to set a new active project before running other CLI commands.

firebase use \
--unalias PROJECT_ALIAS	Removes an alias from your project directory.
You can override what's being used as the currently active project by passing the --project flag with any CLI command. As an example: You can set your CLI to run against a Firebase project that you've assigned the staging alias. If you want to run a single command against the Firebase project that you've assigned the prod alias, then you can run, for example, firebase deploy --project=prod.

Source control and project aliases
In general, you should check your .firebaserc file into source control to allow your team to share project aliases. However, for open source projects or starter templates, you should generally not check in your .firebaserc file.

If you have a development project that's for your use only, you can either pass the --project flag with each command or run firebase use PROJECT_ID without assigning an alias to the Firebase project.

Serve and test your Firebase project locally
You can view and test your Firebase project on locally hosted URLs before deploying to production. If you only want to test select features, you can use a comma-separated list in a flag on the firebase serve command.

Run the following command from the root of your local project directory if you want to do either of the following tasks:

View the static content for your Firebase-hosted app.
Use Cloud Functions to generate dynamic content for Firebase Hosting and you want to use your production (deployed) HTTP functions to emulate Hosting on a local URL.

firebase serve --only hosting
Emulate your project using local HTTP functions
Run any of the following commands from your project directory to emulate your project using local HTTP functions.

To emulate HTTP functions and hosting for testing on local URLs, use either of the following commands:


firebase serve

firebase serve --only functions,hosting // uses a flag
To emulate HTTP functions only, use the following command:


firebase serve --only functions
Test from other local devices
By default, firebase serve only responds to requests from localhost. This means that you'll be able to access your hosted content from your computer's web browser but not from other devices on your network. If you'd like to test from other local devices, use the --host flag, like so:


firebase serve --host 0.0.0.0  // accepts requests to any host
Deploy to a Firebase project
The Firebase CLI manages deployment of code and assets to your Firebase project, including:

New releases of your Firebase Hosting sites
New, updated, or existing Cloud Functions for Firebase
New or updated schemas and connectors for Firebase Data Connect
Rules for Firebase Realtime Database
Rules for Cloud Storage for Firebase
Rules for Cloud Firestore
Indexes for Cloud Firestore
To deploy to a Firebase project, run the following command from your project directory:


firebase deploy
You can optionally add a comment to each of your deployments. This comment will display with the other deployment information on your project's Firebase Hosting page. For example:


firebase deploy -m "Deploying the best new feature ever."
When you use the firebase deploy command, be aware of the following:

To deploy resources from a project directory, the project directory must have a firebase.json file. This file is automatically created for you by the firebase init command.

By default, firebase deploy creates a release for all deployable resources in your project directory. To deploy specific Firebase services or features, use partial deployment.

Deployment conflicts for security rules
For Firebase Realtime Database, Cloud Storage for Firebase, and Cloud Firestore, you can define security rules either in your local project directory or in the Firebase console.

Note: When you deploy security rules using the Firebase CLI, the rules defined in your project directory overwrite any existing rules in the Firebase console. So, if you choose to define or edit your security rules using the Firebase console, make sure that you also update the rules defined in your project directory.
Another option to avoid deployment conflicts is to use partial deployment and only define rules in the Firebase console.

Deployment quotas
It's possible (though unlikely) that you might exceed a quota that limits the rate or volume of your Firebase deployment operations. For example, when deploying very large numbers of functions, you might receive an HTTP 429 Quota error message. To solve such issues, try using partial deployment.

Roll back a deployment
You can roll back a Firebase Hosting deployment from your project's Firebase Hosting page by selecting the Rollback action for the desired release.

It's not currently possible to roll back releases of security rules for Firebase Realtime Database, Cloud Storage for Firebase, or Cloud Firestore.

Deploy specific Firebase services
If you only want to deploy specific Firebase services or features, you can use a comma-separated list in a flag on the firebase deploy command. For example, the following command deploys Firebase Hosting content and Cloud Storage security rules.


firebase deploy --only hosting,storage
The following table lists the services and features available for partial deployment. The names in the flags correspond to the keys in your firebase.json configuration file.

Flag syntax	Service or feature deployed
--only hosting	Firebase Hosting content
--only database	Firebase Realtime Database rules
--only dataconnect	Firebase Data Connect schemas and connectors
--only storage	Cloud Storage for Firebase rules
--only firestore	Cloud Firestore rules and indexes for all configured databases
--only functions	Cloud Functions for Firebase (more specific versions of this flag are possible)
Note: The --only rules syntax used by older versions of the CLI is deprecated.
Deploy specific functions
When deploying functions, you can target specific functions. For example:


firebase deploy --only functions:function1

firebase deploy --only functions:function1,functions:function2
Another option is to group functions into export groups in your /functions/index.js file. Grouping functions allows you to deploy multiple functions using a single command.

For example, you can write the following functions to define a groupA and a groupB:


var functions = require('firebase-functions/v1');

exports.groupA = {
  function1: functions.https.onRequest(...),
  function2: functions.database.ref('\path').onWrite(...)
}
exports.groupB = require('./groupB');
In this example, a separate functions/groupB.js file contains additional functions that specifically define the functions in groupB. For example:


var functions = require('firebase-functions/v1');

exports.function3 = functions.storage.object().onChange(...);
exports.function4 = functions.analytics.event('in_app_purchase').onLog(...);
In this example, you can deploy all the groupA functions by running the following command from your project directory:


firebase deploy --only functions:groupA
Or you can target a specific function within a group by running the following command:


firebase deploy --only functions:groupA.function1,groupB.function4
Important: To avoid running to quota errors and other server errors, limit function group size to 10 or fewer for each deployment operation.
Delete functions
The Firebase CLI supports the following commands and options for deleting previously deployed functions:

Deletes all functions that match the specified name in all regions:


firebase functions:delete FUNCTION-1_NAME
Deletes a specified function running in a non-default region:


firebase functions:delete FUNCTION-1_NAME --region REGION_NAME
Deletes more than one function:


firebase functions:delete FUNCTION-1_NAME FUNCTION-2_NAME
Deletes a specified functions group:


firebase functions:delete GROUP_NAME
Bypasses the confirmation prompt:


firebase functions:delete FUNCTION-1_NAME --force
Set up predeploy and postdeploy scripted tasks
You can connect shell scripts to the firebase deploy command to perform predeploy or postdeploy tasks. For example, a predeploy script could transpile TypeScript code into JavaScript, and a postdeploy hook could notify administrators of new site content deploys to Firebase Hosting.

To set up predeploy or postdeploy hooks, add bash scripts to your firebase.json configuration file. You can define brief scripts directly in the firebase.json file, or you can reference other files that are in your project directory.

For example, the following script is the firebase.json expression for a postdeploy task that sends a Slack message upon successful deployment to Firebase Hosting.
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")

"hosting": {
  // ...

  "postdeploy": "./messageSlack.sh 'Just deployed to Firebase Hosting'",
  "public": "public"
}
The messageSlack.sh script file resides in the project directory and looks like this:


curl -X POST -H 'Content-type: application/json' --data '{"text":"$1"}'
     \https://SLACK_WEBHOOK_URL
You can set up predeploy and postdeploy hooks for any of the assets that you can deploy. Note that running firebase deploy triggers all the predeploy and postdeploy tasks defined in your firebase.json file. To run only those tasks associated with a specific Firebase service, use partial deployment commands.

Both predeploy and postdeploy hooks print the standard output and error streams of the scripts to the terminal. For failure cases, note the following:

If a predeploy hook fails to complete as expected, deployment is canceled.
If deployment fails for any reason, postdeploy hooks are not triggered.
Environment variables
Within scripts running in the predeploy and postdeploy hooks, the following environment variables are available:

$GCLOUD_PROJECT: The active project's project ID
$PROJECT_DIR: The root directory containing the firebase.json file
$RESOURCE_DIR: (For hosting and functions scripts only) The location of the directory that contains the Hosting or Cloud Functions resources to be deployed
Manage multiple Realtime Database instances
A Firebase project can have multiple Firebase Realtime Database instances. By default, CLI commands interact with your default database instance.

However, you can interact with a non-default database instance by using the --instance DATABASE_NAME flag. The following commands support the --instance flag:

firebase database:get
firebase database:profile
firebase database:push
firebase database:remove
firebase database:set
firebase database:update
Command reference
CLI administrative commands
Command	Description
help	Displays help information about the CLI or specific commands.
init	Associates and sets up a new Firebase project in the current directory. This command creates a firebase.json configuration file in the current directory.
login	Authenticates the CLI with your Google Account. Requires access to a web browser.
To log into the CLI in remote environments that don't allow access to localhost, use the --no-localhost flag.
login:ci	Generates an authentication token for use in non-interactive environments.
logout	Signs out your Google Account from the CLI.
open	Opens a browser to relevant project resources.
projects:list	Lists all the Firebase projects to which you have access.
use	Sets the active Firebase project for the CLI.
Manages project aliases.
Project management commands
Command	Description
Management of Firebase projects
projects:addfirebase	Adds Firebase resources to an existing Google Cloud project.
projects:create	Creates a new Google Cloud project, then adds Firebase resources to the new project.
projects:list	Lists all the Firebase projects to which you have access.
Management of Firebase Apps (iOS, Android, Web)
apps:create	Creates a new Firebase App in the active project.
apps:list	Lists the registered Firebase Apps in the active project.
apps:sdkconfig	Prints the Google services configuration of a Firebase App.
setup:web	Deprecated. Instead, use apps:sdkconfig and specify web as the platform argument.
Prints the Google services configuration of a Firebase Web App.
Management of SHA certificate hashes (Android only)
apps:android:sha:create \
FIREBASE_APP_ID SHA_HASH	Adds the specified SHA certificate hash to the specified Firebase Android App.
apps:android:sha:delete \
FIREBASE_APP_ID SHA_HASH	Deletes the specified SHA certificate hash from the specified Firebase Android App.
apps:android:sha:list \
FIREBASE_APP_ID	Lists the SHA certificate hashes for the specified Firebase Android App.
Deployment and local development
These commands let you deploy and interact with your Firebase Hosting site.

Command	Description
deploy	Deploys code and assets from your project directory to the active project. For Firebase Hosting, a firebase.json configuration file is required.
serve	Starts a local web server with your Firebase Hosting configuration. For Firebase Hosting, a firebase.json configuration file is required.
App Distribution commands
Command	Description
appdistribution:distribute \
--app FIREBASE_APP_ID	Makes the build available to testers.
appdistribution:testers:add	Adds testers to the project.
appdistribution:testers:remove	Removes testers from the project.
App Hosting commands
Command	Description
apphosting:backends:create \
--project PROJECT_ID \
--location REGION --app APP_ID	Creates the collection of managed resources linked to a single codebase that comprises an App Hosting backend. Optionally specify an existing Firebase Web app by its Firebase app ID.
apphosting:backends:get \
BACKEND_ID \
--project PROJECT_ID \
--location REGION	Retrieves specific details, including the public URL, of a backend.
apphosting:backends:list \
--project PROJECT_ID	Retrieves a list of all active backends associated with a project.
firebase apphosting:backends:delete \
BACKEND_ID \
--project PROJECT_ID \
--location REGION	Deletes a backend from the project.
firebase apphosting:config:export \
--project PROJECT_ID \
--secrets ENVIRONMENT_NAME	Exports secrets for use in app emulation.
Defaults to secrets stored in apphosting.yaml, or takes --secrets to specify any environment that has a corresponding apphosting.ENVIRONMENT_NAME.yaml file.
firebase apphosting:rollouts:create \
BACKEND_ID \
--git_branch BRANCH_NAME \
--git_commit COMMIT_ID	Creates a manually triggered rollout.
Optionally specify the latest commit to a branch or a specific commit. If no options are provided, prompts selection from a list of branches.
apphosting:secrets:set KEY --project PROJECT_ID \
--location REGION \
--data-file DATA_FILE_PATH	Stores secret material in Secret Manager.
Optionally provide a file path from which to read secret data. Set to _ to read secret data from standard input.
apphosting:secrets:grantaccess KEY BACKEND_ID \
--project PROJECT_ID \
--location REGION	Grants the backend service account access to the provided secret so that it can be accessed by App Hosting at build or run time.
apphosting:secrets:describe KEY \
--project PROJECT_ID	Gets the metadata for a secret and its versions.
firebase apphosting:secrets:access \
KEY[@version] \
--project PROJECT_ID	Accesses a secret value given the secret and its version. Defaults to accessing the latest version.
Authentication (user management) commands
Command	Description
auth:export	Exports the active project's user accounts to a JSON or CSV file. For more details, refer to the auth:import and auth:export page.
auth:import	Imports the user accounts from a JSON or CSV file into the active project. For more details, refer to the auth:import and auth:export page.
Cloud Firestore commands
Command	Description
firestore:locations	
List available locations for your Cloud Firestore database.

firestore:databases:create DATABASE_ID	
Create a database instance in native mode in your Firebase project.

The command takes the following flags:

--location <region name> to specify the deployment location for the database. Note you can run firebase firestore:locations to list available locations. Required.
--delete-protection <deleteProtectionState> to allow or prevent deletion of the specified database. Valid values are ENABLED or DISABLED. Defaults to DISABLED.
--point-in-time-recovery <PITRState> to set whether point-in-time recovery is enabled. Valid values are ENABLED or DISABLED. Defaults to DISABLED. Optional.
firestore:databases:list	
List databases in your Firebase project.

firestore:databases:get DATABASE_ID	
Get database configuration for a specified database in your Firebase project.

firestore:databases:update DATABASE_ID	
Update database configuration of a specified database in your Firebase project.

At least one flag is required. The command takes the following flags:

--delete-protection <deleteProtectionState> to allow or prevent deletion of the specified database. Valid values are ENABLED or DISABLED. Defaults to DISABLED.
--point-in-time-recovery <PITRState> to set whether point-in-time recovery is enabled. Valid values are ENABLED or DISABLED. Defaults to DISABLED. Optional.
firestore:databases:delete DATABASE_ID	
Delete a database in your Firebase project.

firestore:indexes	
List indexes for a database in your Firebase project.

The command takes the following flag:

--database DATABASE_ID to specify the name of the database for which to list indexes. If not provided, indexes are listed for the default database.
firestore:delete	
Deletes documents in the active project's database. Using the CLI, you can recursively delete all the documents in a collection.

Note that deleting Cloud Firestore data with the CLI incurs read and delete costs. For more information, see Understand Cloud Firestore billing.

The command takes the following flag:

--database DATABASE_ID to specify the name of the database from which documents are deleted. If not specified, documents are deleted from the default database. Optional.
Cloud Functions for Firebase commands
Command	Description
functions:config:clone	Clones another project's environment into the active Firebase project.
functions:config:get	Retrieves existing configuration values of the active project's Cloud Functions.
functions:config:set	Stores runtime configuration values of the active project's Cloud Functions.
functions:config:unset	Removes values from the active project's runtime configuration.
functions:log	Reads logs from deployed Cloud Functions.
For more information, refer to the environment configuration documentation.

Crashlytics commands
Command	Description
crashlytics:mappingfile:generateid \
--resource-file=PATH/TO/ANDROID_RESOURCE.XML	Generates a unique mapping file ID in the specified Android resource (XML) file.
crashlytics:mappingfile:upload \
--app=FIREBASE_APP_ID \
--resource-file=PATH/TO/ANDROID_RESOURCE.XML \
PATH/TO/MAPPING_FILE.TXT	Uploads a Proguard-compatible mapping (TXT) file for this app, and associates it with the mapping file ID declared in the specified Android resource (XML) file.
crashlytics:symbols:upload \
--app=FIREBASE_APP_ID \
PATH/TO/SYMBOLS	Generates a Crashlytics-compatible symbol file for native library crashes on Android and uploads it to Firebase servers.
Data Connect commands
These commands and their use cases are covered in more detail in the Data Connect CLI reference guide.

Command	Description
dataconnect:services:list	Lists all deployed Data Connect services in your Firebase project.
dataconnect:sql:diff \
SERVICE_ID	For the specified service, displays the differences between a local Data Connect schema and your Cloud SQL database schema.
dataconnect:sql:migrate \
--force \
SERVICE_ID	Migrates your Cloud SQL database's schema to match your local Data Connect schema.
dataconnect:sql:grant\
--role=ROLE \
--email=EMAIL \
SERVICE_ID	Grants the SQL role to the specified user or service account email.
For the --role flag, the SQL role to grant is one of: owner, writer, or reader.
For the --email flag, provide the email address of the user or service account to grant the role to.
dataconnect:sdk:generate	Generates typed SDKs for your Data Connect connectors.
Extensions commands
Command	Description
ext	Displays information on how to use Firebase Extensions commands.
Lists the extension instances installed in the active project.
ext:configure \
EXTENSION_INSTANCE_ID	Reconfigures the parameter values of an extension instance in your extension manifest.
ext:info \
PUBLISHER_ID/EXTENSION_ID	Prints detailed information about an extension.
ext:install \
PUBLISHER_ID/EXTENSION_ID	Adds a new instance of an extension into your extension manifest.
ext:list	Lists all the extension instances installed in a Firebase project.
Prints the instance ID for each extension.
ext:uninstall \
EXTENSION_INSTANCE_ID	Removes an extension instance from your extension manifest.
ext:update \
EXTENSION_INSTANCE_ID	Updates an extension instance to the latest version in your extension manifest.
ext:export	Exports all installed extension instances from your project to your extension manifest.
Extensions publisher commands
Command	Description
ext:dev:init	Initializes a skeleton codebase for a new extension in the current directory.
ext:dev:list \
PUBLISHER_ID	Prints a list of all extensions uploaded by a publisher.
ext:dev:register	Registers a Firebase project as an extensions publisher project.
ext:dev:deprecate \
PUBLISHER_ID/EXTENSION_ID \
VERSION_PREDICATE	Deprecates extension versions that match the version predicate.
A version predicate can be a single version (such as 1.0.0), or a range of versions (such as >1.0.0).
If no version predicate is provided, deprecates all versions of that extension.
ext:dev:undeprecate \
PUBLISHER_ID/EXTENSION_ID \
VERSION_PREDICATE	Undeprecates extension versions that match the version predicate.
A version predicate can be a single version (such as 1.0.0), or a range of versions (such as >1.0.0).
If no version predicate is provided, undeprecates all versions of that extension.
ext:dev:upload \
PUBLISHER_ID/EXTENSION_ID	Uploads a new version of an extension.
ext:dev:usage \
PUBLISHER_ID	Displays install counts and usage metrics for extensions uploaded by a publisher.
Hosting commands
Command	Description
hosting:disable	
Stops serving Firebase Hosting traffic for the active Firebase project.

Your project's Hosting URL will display a "Site Not Found" message after running this command.

Management of Hosting sites
firebase hosting:sites:create \
SITE_ID	
Creates a new Hosting site in the active Firebase project using the specified SITE_ID

(Optional) Specify an existing Firebase Web App to associate with the new site by passing the following flag: --app FIREBASE_APP_ID

firebase hosting:sites:delete \
SITE_ID	
Deletes the specified Hosting site

The CLI displays a confirmation prompt before deleting the site.

(Optional) Skip the confirmation prompt by passing the following flags: -f or --force

firebase hosting:sites:get \
SITE_ID	
Retrieves information about the specified Hosting site

firebase hosting:sites:list	
Lists all Hosting sites for the active Firebase project

Management of preview channels
firebase hosting:channel:create \
CHANNEL_ID	
Creates a new preview channel in the default Hosting site using the specified CHANNEL_ID

This command does not deploy to the channel.

firebase hosting:channel:delete \
CHANNEL_ID	
Deletes the specified preview channel

You cannot delete a site's live channel.

firebase hosting:channel:deploy \
CHANNEL_ID	
Deploys your Hosting content and config to the specified preview channel

If the preview channel does not yet exist, this command creates the channel in the default Hosting site before deploying to the channel.

firebase hosting:channel:list	Lists all channels (including the "live" channel) in the default Hosting site
firebase hosting:channel:open \
CHANNEL_ID	Opens a browser to the specified channel's URL or returns the URL if opening in a browser isn't possible
Version cloning
firebase hosting:clone \
SOURCE_SITE_ID:SOURCE_CHANNEL_ID \
TARGET_SITE_ID:TARGET_CHANNEL_ID	
Clones the most recently deployed version on the specified "source" channel to the specified "target" channel

This command also deploys to the specified "target" channel. If the "target" channel does not yet exist, this command creates a new preview channel in the "target" Hosting site before deploying to the channel.

firebase hosting:clone \
SOURCE_SITE_ID:@VERSION_ID \
TARGET_SITE_ID:TARGET_CHANNEL_ID	
Clones the specified version to the specified "target" channel

This command also deploys to the specified "target" channel. If the "target" channel does not yet exist, this command creates a new preview channel in the "target" Hosting site before deploying to the channel.

You can find the VERSION_ID in the Hosting dashboard of the Firebase console.

Realtime Database commands
Note that you can create your initial, default Realtime Database instance in the Firebase console or by using the general firebase init workflow or the specific firebase init database flow.

Once instances are created, you can manage them as discussed in Manage multiple Realtime Database instances.

Command	Description
database:get	Fetches data from the active project's database and displays it as JSON. Supports querying on indexed data.
database:instances:create	Creates a database instance with a specified instance name. Accepts the --location option for creating a database in a specified region. For region names to use with this option, see select locations for your project. If no database instance exists for the current project, you are prompted to run the firebase init flow to create an instance.
database:instances:list	List all database instances for this project. Accepts the --location option for listing databases in a specified region. For region names to use with this option see select locations for your project.
database:profile	Builds a profile of operations on the active project's database. For more details, refer to Realtime Database operation types.
database:push	Pushes new data to a list at a specified location in the active project's database. Takes input from a file, STDIN, or a command-line argument.
database:remove	Deletes all data at a specified location in the active project's database.
database:set	Replaces all data at a specified location in the active project's database. Takes input from a file, STDIN, or a command-line argument.
database:update	Performs a partial update at a specified location in the active project's database. Takes input from a file, STDIN, or a command-line argument.
Remote Config commands
Command	Description
remoteconfig:versions:list \
--limit NUMBER_OF_VERSIONS	Lists the most recent ten versions of the template. Specify 0 to return all existing versions, or optionally pass the --limit option to limit the number of versions being returned.
remoteconfig:get \
--v, version_number VERSION_NUMBER
--o, output FILENAME	Gets the template by version (defaults to the latest version) and outputs the parameter groups, parameters, and condition names and version into a table. Optionally, you can write the output to a specified file with -o, FILENAME.
remoteconfig:rollback \
--v, version_number VERSION_NUMBER
--force	Rolls back Remote Config template to a specified previous version number or defaults to the immediate previous version (current version -1). Unless --force is passed, prompts Y/N before proceeding to rollback.
Send feedback
Except as otherwise noted, the content of this page is licensed under the Creative Commons Attribution 4.0 License, and code samples are licensed under the Apache 2.0 License. For details, see the Google Developers Site Policies. Java is a registered trademark of Oracle and/or its affiliates.

Last updated 2025-06-04 UTC.

Learn
Developer guides
SDK & API reference
Samples
Libraries
GitHub
Stay connected
Check out the blog
Find us on Reddit
Follow on X
Subscribe on YouTube
Attend an event
Support
Contact support
Stack Overflow
Slack community
Google group
Release notes
Brand guidelines
FAQs
Google Developers
Android
Chrome
Firebase
Google Cloud Platform
All products
Terms
Privacy

English
The new page has loaded..

type User @table {
  displayName: String!
  email: String
  photoUrl: String
  shippingAddress: String
  createdAt: Timestamp!
}

type Product @table {
  name: String!
  description: String!
  price: Float!
  imageUrl: String!
  inventoryCount: Int
  category: String
  createdAt: Timestamp!
}

type Order @table {
  user: User!
  orderDate: Timestamp!
  totalAmount: Float!
  status: String!
  shippingAddress: String
  trackingNumber: String
}

type OrderItem @table {
  order: Order!
  product: Product!
  quantity: Int!
  price: Float!
}

type Category @table {
  name: String!
  description: String
  createdAt: Timestamp!
}

Skip to main content
Firebase
More
Search
/


English
Blog
Studio
Go to console

Documentation
Crashlytics
Overview
Fundamentals

AI

Build

Run

Test Lab
App Distribution
Crashlytics
Performance Monitoring
Remote Config
A/B Testing
Analytics
Cloud Messaging
In-App Messaging
Dynamic Links
Google AdMob
Google Ads
Reference
Samples
Filter

Here's everything we announced at I/O, from new Firebase Studio features to more ways to integrate AI. Read blog.
Firebase
Documentation
Crashlytics
Run
Was this helpful?

Send feedbackGet started with Firebase Crashlytics 

bookmark_border
iOS+ Android Flutter Unity


This quickstart describes how to set up Firebase Crashlytics in your app with the Firebase Crashlytics SDK so that you can get comprehensive crash reports in the Firebase console. With Crashlytics for Android, you get reports for crashes, non-fatal errors, and "Application Not Responding" (ANR) errors.

Setting up Crashlytics requires tasks both in the Firebase console and your IDE (like adding a Firebase configuration file and the Crashlytics SDK). To finish setup, you'll need to force a test crash to send your first crash report to Firebase.

Before you begin
If you haven't already, add Firebase to your Android project. If you don't have an Android app, you can download a sample app.

Recommended: To automatically get breadcrumb logs to understand user actions leading up to a crash, non-fatal, or ANR event, you need to enable Google Analytics in your Firebase project.

If your existing Firebase project doesn't have Google Analytics enabled, you can enable Google Analytics from the Integrations tab of your settings > Project settings in the Firebase console.

If you're creating a new Firebase project, enable Google Analytics during the project creation workflow.

Make sure your app has the following minimum required versions:

Gradle 8.0
Android Gradle plugin 8.1.0
Google services Gradle plugin 4.4.1
Step 1: Add the Crashlytics SDK to your app
Does your app use NDK? Go to the NDK crash reporting documentation to learn how to configure Crashlytics to report crashes that occur in your app's underlying NDK libraries.
In your module (app-level) Gradle file (usually <project>/<app-module>/build.gradle.kts or <project>/<app-module>/build.gradle), add the dependency for the Crashlytics library for Android. We recommend using the Firebase Android BoM to control library versioning.
To take advantage of breadcrumb logs, also add the Firebase SDK for Google Analytics to your app. Make sure that Google Analytics is enabled in your Firebase project.

([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
dependencies {
    // Import the BoM for the Firebase platform
    implementation(platform("com.google.firebase:firebase-bom:33.15.0"))

    // Add the dependencies for the Crashlytics and Analytics libraries
    // When using the BoM, you don't specify versions in Firebase library dependencies
    implementation("com.google.firebase:firebase-crashlytics")
    implementation("com.google.firebase:firebase-analytics")
}
By using the Firebase Android BoM, your app will always use compatible versions of Firebase Android libraries.

(Alternative)  Add Firebase library dependencies without using the BoM

Looking for a Kotlin-specific library module? Starting in October 2023 (Firebase BoM 32.5.0), both Kotlin and Java developers can depend on the main library module (for details, see the FAQ about this initiative).
Step 2: Add the Crashlytics Gradle plugin to your app
In your root-level (project-level) Gradle file (<project>/build.gradle.kts or <project>/build.gradle), add the Crashlytics Gradle plugin to the plugins block:

Kotlin
Groovy
Are you still using the buildscript syntax? Learn how to add Firebase plugins using that syntax.
plugins {
    // Make sure that you have the AGP plugin 8.1+ dependency
    id("com.android.application") version "8.1.4" apply false
    // ...

    // Make sure that you have the Google services Gradle plugin 4.4.1+ dependency
    id("com.google.gms.google-services") version "4.4.2" apply false

    // Add the dependency for the Crashlytics Gradle plugin
    id("com.google.firebase.crashlytics") version "3.0.4" apply false
}
Is your app using a lower version of Gradle? Consider upgrading; otherwise, you should use v2.9.9 of the Crashlytics Gradle plugin.
In your module (app-level) Gradle file (usually <project>/<app-module>/build.gradle.kts or <project>/<app-module>/build.gradle), add the Crashlytics Gradle plugin:

Kotlin
Groovy
plugins {
  id("com.android.application")
  // ...

  // Make sure that you have the Google services Gradle plugin
  id("com.google.gms.google-services")

  // Add the Crashlytics Gradle plugin
  id("com.google.firebase.crashlytics")
}
Step 3: Force a test crash to finish setup
To finish setting up Crashlytics and see initial data in the Crashlytics dashboard of the Firebase console, you need to force a test crash.

Add code to your app that you can use to force a test crash.

You can use the following code in your app's MainActivity to add a button to your app that, when pressed, causes a crash. The button is labeled "Test Crash".

Kotlin
Java
val crashButton = Button(this)
crashButton.text = "Test Crash"
crashButton.setOnClickListener {
   throw RuntimeException("Test Crash") // Force a crash
}

addContentView(crashButton, ViewGroup.LayoutParams(
       ViewGroup.LayoutParams.MATCH_PARENT,
       ViewGroup.LayoutParams.WRAP_CONTENT))
Build and run your app.

Force the test crash in order to send your app's first crash report:

Open your app from your test device or emulator.

In your app, press the "Test Crash" button that you added using the code above.

After your app crashes, restart it so that your app can send the crash report to Firebase.

Go to the Crashlytics dashboard of the Firebase console to see your test crash.

If you've refreshed the console and you're still not seeing the test crash after five minutes, enable debug logging to see if your app is sending crash reports.



And that's it! Crashlytics is now monitoring your app for crashes, non-fatal errors, and ANRs. Visit the Crashlytics dashboard to view and investigate all your reports and statistics.
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
Next steps
Customize your crash report setup by adding opt-in reporting, logs, keys, and tracking of non-fatal errors.
Integrate with Google Play so that you can filter your Android app's crash reports by Google Play track directly in the Crashlytics dashboard. This allows you to better focus your dashboard on specific builds.
In Android Studio, view and filter Crashlytics data.
Use the App Quality Insights (AQI) window in Android Studio to view Crashlytics data alongside your code — no need to jump back and forth between the Crashlytics dashboard and the IDE to start debugging top issues.
Learn how to use the AQI window in the Android Studio documentation.
We'd love to hear from you! Send us feedback about the AQI window by filing a bug report.
Send feedback
Except as otherwise noted, the content of this page is licensed under the Creative Commons Attribution 4.0 License, and code samples are licensed under the Apache 2.0 License. For details, see the Google Developers Site Policies. Java is a registered trademark of Oracle and/or its affiliates.

Last updated 2025-06-12 UTC.

Learn
Developer guides
SDK & API reference
Samples
Libraries
GitHub
Stay connected
Check out the blog
Find us on Reddit
Follow on X
Subscribe on YouTube
Attend an event
Support
Contact support
Stack Overflow
Slack community
Google group
Release notes
Brand guidelines
FAQs
Google Developers
Android
Chrome
Firebase
Google Cloud Platform
All products
Terms
Privacy

English
([ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh")
The MIT License (MIT)

Copyright (c) 2010 Tim Caswell

Copyright (c) 2014 Jordan Harband

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of
the Software, and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.





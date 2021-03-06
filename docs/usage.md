# HEMTT Usage

<pre>
Usage:
    hemtt <a href="/HEMTT/#/usage?id=init">init</a>
    hemtt <a href="/HEMTT/#/usage?id=bug">bug</a>
    hemtt <a href="/HEMTT/#/usage?id=addon">addon</a> &lt;name&gt;
    hemtt <a href="/HEMTT/#/usage?id=build">build</a> [<a href="/HEMTT/#/usage?id=addons">&lt;addons&gt;</a>] [<a href="/HEMTT/#/usage?id=-release">--release</a>] [<a href="/HEMTT/#/usage?id=-force">-f</a>] [<a href="/HEMTT/#/usage?id=-nowarn">--nowarn</a>] [<a href="/HEMTT/#/usage?id=-opts">--opts</a>=&lt;addons&gt;] [<a href="/HEMTT/#/usage?id=-compats">--compats</a>=&lt;addons&gt;]
    hemtt <a href="/HEMTT/#/usage?id=clean">clean</a> [--force]
    hemtt <a href="/HEMTT/#/usage?id=update">update</a>
    hemtt (-h | --help)
    hemtt --version

Options:
        --ci               Run in CI mode
        --debug            Turn debugging information on
    -f, --force            Rebuild existing files
        --force-release    Remove an existing release
    -h, --help             Prints help information
        --no-progress      No progress bars
        --release          Build a release
        --time             Time the execution
    -V, --version          Prints version information
</pre>
<hr/>

# init

Initialize a project file in the current directory. `init` is used when you have existing files or do not want to use the CBA structure.
<hr/>

# bug

Opens a new issue page on GitHub with some info already filled out.
<hr/>

# addon

Create a new addon folder. Requires a name to be used for the addon.

```
./hemtt addon common
```
<pre>
.
└── <a href="https://github.com/synixebrett/HEMTT-Example/tree/master/addons">addons/</a>
    └── <a href="https://github.com/synixebrett/HEMTT-Example/tree/master/addons/common">common</a>
        ├── <a href="https://github.com/synixebrett/HEMTT-Example/blob/master/addons/common/%24PBOPREFIX%24">$PBOPREFIX$</a>
        ├── <a href="https://github.com/synixebrett/HEMTT-Example/blob/master/addons/common/CfgEventHandlers.hpp">CfgEventHandlers.hpp</a>
        ├── <a href="https://github.com/synixebrett/HEMTT-Example/blob/master/addons/common/XEH_PREP.hpp">XEH_PREP.hpp</a>
        ├── <a href="https://github.com/synixebrett/HEMTT-Example/blob/master/addons/common/XEH_postInit.sqf">XEH_postInit.sqf</a>
        ├── <a href="https://github.com/synixebrett/HEMTT-Example/blob/master/addons/common/XEH_preInit.sqf">XEH_preInit.sqf</a>
        ├── <a href="https://github.com/synixebrett/HEMTT-Example/blob/master/addons/common/XEH_preStart.sqf">XEH_preStart.sqf</a>
        ├── <a href="https://github.com/synixebrett/HEMTT-Example/blob/master/addons/common/config.cpp">config.cpp</a>
        ├── <a href="https://github.com/synixebrett/HEMTT-Example/blob/master/addons/common/script_component.hpp">script_component.hpp</a>
        └── <a href="https://github.com/synixebrett/HEMTT-Example/tree/master/addons/common/functions">functions/</a>
            └── <a href="https://github.com/synixebrett/HEMTT-Example/blob/master/addons/common/functions/script_component.hpp">script_component.hpp</a>
</pre>
<hr>

# build
Build the project into PBO files. HEMTT will only build the files that have changed.

## addons
A list of addon to build. HEMTT will build all addons in the `./addons` folder if no addons are specified. HEMTT will always build all addons when using `--release`.

**Build all**  
`hemtt build`

**Build a single addon**  
`hemtt build tracers`

**Build multiple addons**  
`hemtt build tracers,hearing`

## --nowarn
Hide warnings from the armake2 build process.

## --force
Remove existing built files before starting the next build.

## --release
Create and sign a release build of the project.

A `hemtt.toml` file of 
```toml
name = "Test Mod"
prefix = "TST"
author = "SynixeBrett"
files = [
    "mod.cpp"
]
```
would produce
<pre>
.
└── releases/
    └── 0.1.0.0/
        └── <a href="https://github.com/synixebrett/HEMTT-Example/tree/master/releases/0.1.0.0/%40TST">@TST/</a>
            ├── mod.cpp
            └── addons/
                ├── TST_common.pbo
                ├── TST_example.pbo
                └── TST_main.pbo
</pre>
This example is from the [HEMTT Example Project](https://github.com/synixebrett/HEMTT-Example)

## --opts
A list of addtional addons to build. HEMTT will look for these in the `./optionals` folder. Using `--opts all` will build all addons in the `./optionals` folder. All optionals are built when no filtering is specified (`hemtt build`).

`hemtt build --opts all`  
`hemtt build --opts tracers`  
`hemtt build --opts tracers patrticles`

## --compats
A list of compat addons to build. HEMTT will look for these in the `./compats` folder. Using `--compats all` will build all compats in the `./compats` folder. All compats are built when no filtering is specified (`hemtt build`).

`hemtt build --compats hearing`  
`hemtt build --compats hearing zeus`

<hr/>

# clean
Cleans all the files generated from previous builds.
<hr>

# run
Run a [Script](/scripts.md).
<hr/>

# utility
Run a [Utility](/utilities.md).
<hr/>

# update

HEMTT will look for a more recent version online. If one is available you will be prompted to download the updated version.

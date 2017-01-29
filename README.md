This is the local manifest for Nvertigo/LineageOS cm-14.1 for oneplus3t.

The repos are optimized for oneplus3t and does NOT work
for oneplus3.

git clone this wherever you want and make symblic links
to .repo/local_manifest for xml file/files.

oneplus3t.xml: imports all neccessary files (including
               blobs and toolchains) to build laos for op3t

zz-remove-unused.xml: removes darwin build environment;
                      it's not mandatory, but makes syncs
		      smaller

How to build this from source
=============================

This is more a step by step guide, then a HOWTO. To understand
what this all is about, try to learn as much as possible on
git, gnu-make, bash, c, c++, java, python, repo, android and 
linux.


Prerequisites
-------------

Setup your build environment for the linuxdistribution of choice.
There are quite some tutorials around; as general starting 
point you may want to read:
https://source.android.com/source/initializing.html

I assume you are using bash as shell.

You need about 60 GB of diskspace to compile LineageOS plus
that amount of space you configure ccache (compiler cache
to speed up future buildings) for.


General preperation
-------------------

Shell commnds:
cd /where/you/want/to/your/source-tree
mkdir -p cm14/my_tmp
cd cm14
repo init -u git://github.com/LineageOS/android.git -b cm-14.1
cd my_tmp
git clone https://github.com/nvertigo/local_manifest.git
cd local_manifest
git checkout cm-14.1
cd ../../.repo
mkdir local_manifest
cd local_manifest
ln -s ../../my_tmp/local_manifest/oneplus3t.xml .
#if you are on macos (aka darwin) skip the next command
ln -s ../../my_tmp/local_manifest/zz-remove-unused.xml .
cd ../..
ln -s my_tmp/my_build.sh ./my-build


Syncing (aka download) the sources
----------------------------------

Shell command:
repo sync #this takes some time; it's about 20GB to fetch

Meanwhile check my-build and edit to meet your needs.

When the sync has finished, adjust TARGET_UNOFFICIAL_BUILD_ID
in device/oneplus/oneplus3t/lineage.mk


Building LineageOS
------------------

Shell command:
./my-build

If every thing works, you will get a flashable zip in:
out/target/product/oneplus3t/

If not, check make.log for errors.

Congrats, you have just build your own rom!

Happy flashing!

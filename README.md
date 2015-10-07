# ndn-brite-helper
This repository contains a custom extension for ndnSIM 2.0/2.1, the Brite Topology Helper.

 The sourcecode is based on the ns-3 version (brite-topology-helper). See https://www.nsnam.org for more information about ns-3. See https://www.nsnam.org/docs/models/html/brite.html for more information about brite and ns-3.

#How-To
Assuming that ndnSIM is the sub-directory where you have ndnSIM and all the remaining sources installed, follow these commands to build BRITE:

	cd ndnSIM
	hg clone http://code.nsnam.org/BRITE
	cd BRITE
	make
	export BRITE_HOME=$(pwd)
	cd ..

Next, you have to clone this repository and move the files to the helper directory of ns-3/src/ndnSIM:

	git clone https://github.com/ChristianKreuzberger/ndn-brite-helper
	cp ndn-brite-helper/helper/ndn-brite-helper.* ns-3/src/ndnSIM/helper/


You have to add two lines to ```ns-3/src/ndnSIM/wscript``` to make sure the compiler finds the Brite.h includes when compiling the newly added helpers. You can do this manually or apply the patch file.
### Manual
Open ```ns-3/src/ndnSIM/wscript``` and locate the lines where it says
```
     module.ndncxx_headers = bld.path.ant_glob(['ndn-cxx/src/**/*.hpp'],
                                               excl=['src/**/*-osx.hpp', 'src/detail/**/*'])
```

Then append these two lines (please watch out for proper indentation with 4 spaces)
```
    if bld.env['ENABLE_BRITE']:
        module.includes.append(os.path.abspath(os.path.join(bld.env['WITH_BRITE'],'.')))
```
### Patch

	cd ns-3/src/ndnSIM
	patch < ../../../ndn-brite-helper/patch_wscript.diff

## Compile

Last but not least, you have to configure and compile the whole ns-3/ndnSIM repository:

	cd ns-3
	./waf configure -d optimized --with-brite=$BRITE_HOME
	./waf


## Running Examples
Work in Progress


# Acknowledgements:
 This work was partially funded by the Austrian Science Fund (FWF) under the CHIST-ERA project CONCERT (A Context-Adaptive Content Ecosystem Under Uncertainty), project number I1402.


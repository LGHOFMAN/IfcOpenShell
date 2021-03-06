VERSION:=`date '+%y%m%d'`
ifeq ($(PLATFORM), win)
PYTHONOCC_URL:=https://anaconda.org/DLR-SC/pythonocc-core/0.17.3/download/win-64/pythonocc-core-0.17.3-py37he980bc4_10.tar.bz2
OCE_URL:=https://anaconda.org/DLR-SC/oce/0.17.2/download/win-64/oce-0.17.2-he980bc4_14.tar.bz2
TBB_URL:=https://anaconda.org/DLR-SC/tbb/2019.5/download/win-64/tbb-2019.5-he980bc4_0.tar.bz2
endif
ifeq ($(PLATFORM), macos)
PYTHONOCC_URL:=https://anaconda.org/DLR-SC/pythonocc-core/0.17.3/download/osx-64/pythonocc-core-0.17.3-py37h04f5b5a_10.tar.bz2
OCE_URL:=https://anaconda.org/DLR-SC/oce/0.17.2/download/osx-64/oce-0.17.2-h04f5b5a_12.tar.bz2
TBB_URL:=https://anaconda.org/DLR-SC/tbb/4.3.6/download/osx-64/tbb-4.3.6-0.tar.bz2
endif
ifeq ($(PLATFORM), linux)
PYTHONOCC_URL:=https://anaconda.org/DLR-SC/pythonocc-core/0.17.3/download/linux-64/pythonocc-core-0.17.3-py37h6bb024c_10.tar.bz2
OCE_URL:=https://anaconda.org/DLR-SC/oce/0.17.2/download/linux-64/oce-0.17.2-h6bb024c_14.tar.bz2
TBB_URL:=https://anaconda.org/DLR-SC/tbb/4.3.6/download/linux-64/tbb-4.3.6-0.tar.bz2
endif

.PHONY: dist
dist:
ifndef PLATFORM
	$(error PLATFORM is not set)
endif
	rm -rf dist
	mkdir -p dist/working
	mkdir -p dist/blenderbim
	cp -r blenderbim/* dist/blenderbim/

	cd dist/working && wget https://s3.amazonaws.com/ifcopenshell-builds/ifcblender-python-37-v0.6.0-0d93633-$(PLATFORM)64.zip
	cd dist/working && unzip ifcblender*
	cp -r dist/working/io_import_scene_ifc/ifcopenshell dist/blenderbim/libs/site/packages/
	# See bug #812
	cd dist/working && wget https://raw.githubusercontent.com/IfcOpenShell/IfcOpenShell/v0.6.0/src/ifcblenderexport/occ_utils.py
	cd dist/working && mv occ_utils.py ../blenderbim/libs/site/packages/ifcopenshell/geom/occ_utils.py
	rm -rf dist/working

	mkdir dist/working
	cd dist/working && wget $(PYTHONOCC_URL)
	cd dist/working && tar -xjvf pythonocc-core*
ifeq ($(PLATFORM), win)
	cd dist/working && cp -r Lib/site-packages/OCC ../blenderbim/libs/site/packages/
else
	cd dist/working && cp -r lib/python3.7/site-packages/OCC ../blenderbim/libs/site/packages/
endif
	rm -rf dist/working

	mkdir dist/working
	cd dist/working && wget $(OCE_URL)
	cd dist/working && tar -xjvf oce*
ifeq ($(PLATFORM), win)
	cd dist/working && cp -r Library/bin/* ../blenderbim/libs/site/packages/OCC/
else
	# Unix Conda builds of PythonOCC expect OCE libs to have a RPATH of ../../../
	cd dist/working && cp -r lib/* ../blenderbim/libs/
endif
ifeq ($(PLATFORM), linux)
	rm -rf dist/blenderbim/libs/oce-0.17
endif
	rm -rf dist/working

	mkdir dist/working
	cd dist/working && wget $(TBB_URL)
	cd dist/working && tar -xjvf tbb*
ifeq ($(PLATFORM), win)
	cd dist/working && cp -r Library/bin/* ../blenderbim/libs/site/packages/OCC/
else
	cd dist/working && cp -r lib/* ../blenderbim/libs/
endif
	rm -rf dist/working

ifeq ($(PLATFORM), macos)
	mkdir dist/working
	cd dist/working && wget https://blenderbim.org/builds/patch-blender28-bim-macos.zip
	cd dist/working && unzip patch*
	cd dist/working && cp -r *.dylib ../blenderbim/libs/
	rm -rf dist/working
endif

	mkdir dist/working
	cd dist/working && wget https://files.pythonhosted.org/packages/d6/fd/eb8c212053addd941cc90baac307c00ac246ac3fce7166b86434c6eae963/pystache-0.5.4.tar.gz
	cd dist/working && tar -xzvf pystache*
	cd dist/working/pystache-0.5.4/ && python setup.py build && cp -r build/lib/pystache ../../blenderbim/libs/site/packages/
	rm -rf dist/working

	mkdir dist/working
	cd dist/working && wget https://files.pythonhosted.org/packages/79/e8/7eb2ba188eda14a4b47e33b51f3b4978985f4116655c699bcd18c79279b5/svgwrite-1.3.1.zip
	cd dist/working && unzip svgwrite*
	cp -r dist/working/svgwrite-1.3.1/svgwrite dist/blenderbim/libs/site/packages/
	rm -rf dist/working

	mkdir dist/working
	cd dist/working && wget https://github.com/Moult/deepdiff/archive/master.zip
	cd dist/working && unzip master.zip
	cp -r dist/working/deepdiff-master/deepdiff dist/blenderbim/libs/site/packages/
	rm -rf dist/working

	mkdir dist/working
	cd dist/working && wget https://files.pythonhosted.org/packages/00/55/ce2cbc6d64034b30cad81a29ba61bdba456f190f5e83c09831304bf68d6b/jsonpickle-1.2.tar.gz
	cd dist/working && tar -xzvf jsonpickle*
	cp -r dist/working/jsonpickle-1.2/jsonpickle dist/blenderbim/libs/site/packages/
	rm -rf dist/working

	mkdir dist/working
	cd dist/working && wget https://files.pythonhosted.org/packages/a3/b7/d4d69641cbe707a45c23b190f2d717466ba5accc4c70b5f7a8a450387895/ordered-set-3.1.1.tar.gz
	cd dist/working && tar -xzvf ordered-set*
	cp -r dist/working/ordered-set-3.1.1/ordered_set.py dist/blenderbim/libs/site/packages/
	rm -rf dist/working

	mkdir dist/working
	cd dist/working && wget https://files.pythonhosted.org/packages/00/32/8076fa13e832bb4dcff379f18f228e5a53412be0631808b9ca2610c0f566/pyparsing-2.4.5.tar.gz
	cd dist/working && tar -xzvf pyparsing*
	cp -r dist/working/pyparsing-2.4.5/pyparsing.py dist/blenderbim/libs/site/packages/
	rm -rf dist/working

	mkdir dist/working
	cd dist/working && wget https://files.pythonhosted.org/packages/82/c3/534ddba230bd4fbbd3b7a3d35f3341d014cca213f369a9940925e7e5f691/pytz-2019.3.tar.gz
	cd dist/working && tar -xzvf pytz*
	cp -r dist/working/pytz-2019.3/pytz dist/blenderbim/libs/site/packages/
	rm -rf dist/working

	mkdir dist/working
	cd dist/working && wget https://files.pythonhosted.org/packages/be/ed/5bbc91f03fa4c839c4c7360375da77f9659af5f7086b7a7bdda65771c8e0/python-dateutil-2.8.1.tar.gz
	cd dist/working && tar -xzvf python-dateutil*
	cp -r dist/working/python-dateutil-2.8.1/dateutil dist/blenderbim/libs/site/packages/
	rm -rf dist/working

	mkdir dist/working
	cd dist/working && wget https://files.pythonhosted.org/packages/21/9f/b251f7f8a76dec1d6651be194dfba8fb8d7781d10ab3987190de8391d08e/six-1.14.0.tar.gz
	cd dist/working && tar -xzvf six*
	cp -r dist/working/six-1.14.0/six.py dist/blenderbim/libs/site/packages/
	rm -rf dist/working

	mkdir dist/working
	cd dist/working && wget https://files.pythonhosted.org/packages/bb/41/ad9ce53bb978b68af8ae415293cafc89b165b8ad55a593725299dca76729/xmlschema-1.1.1.tar.gz
	cd dist/working && tar -xzvf xmlschema*
	cp -r dist/working/xmlschema-1.1.1/xmlschema dist/blenderbim/libs/site/packages/
	rm -rf dist/working

	mkdir dist/working
	cd dist/working && wget https://files.pythonhosted.org/packages/12/f9/f9960222d5274944b01391749e55e4dcdf28d8f0c108b64ac931ceff6fdb/elementpath-1.4.3.tar.gz
	cd dist/working && tar -xzvf elementpath*
	cp -r dist/working/elementpath-1.4.3/elementpath dist/blenderbim/libs/site/packages/
	rm -rf dist/working

	mkdir dist/working
	cd dist/working && wget https://github.com/podestplatz/bcf/archive/master.zip
	cd dist/working && unzip master*
	cp -r dist/working/bcf-master/bcfplugin dist/blenderbim/libs/site/packages/
	rm -rf dist/working

	mkdir dist/working
	cd dist/working && wget https://raw.githubusercontent.com/buildingSMART/BCF-XML/release_2_1/Schemas/project.xsd
	cd dist/working && wget https://raw.githubusercontent.com/buildingSMART/BCF-XML/release_2_1/Extension%20Schemas/extensions.xsd
	cd dist/working && wget https://raw.githubusercontent.com/buildingSMART/BCF-XML/release_2_1/Schemas/markup.xsd
	cd dist/working && wget https://raw.githubusercontent.com/buildingSMART/BCF-XML/release_2_1/Schemas/version.xsd
	cd dist/working && wget https://raw.githubusercontent.com/buildingSMART/BCF-XML/release_2_1/Schemas/visinfo.xsd
	mkdir dist/blenderbim/libs/site/packages/bcfplugin/schemas/
	cp -r dist/working/*.xsd dist/blenderbim/libs/site/packages/bcfplugin/schemas/
	rm -rf dist/working

	mkdir dist/working
	cd dist/working && wget https://files.pythonhosted.org/packages/18/4d/8d522136c37d9e1ea74062b41b8d5e1318ebf45063ae46ce72ed60af223b/lark-parser-0.8.5.tar.gz
	cd dist/working && tar -xzvf lark-parser*
	cp -r dist/working/lark-parser-0.8.5/lark dist/blenderbim/libs/site/packages/
	rm -rf dist/working

ifeq ($(PLATFORM), linux)
	mkdir dist/working
	cd dist/working && wget https://files.pythonhosted.org/packages/0c/fa/00d85f893b02289e2942849d97f8818dde8e2111182e825fb3a735677791/python_fcl-0.0.12-cp37-cp37m-manylinux1_x86_64.whl
	cd dist/working && unzip python_fcl*
	cp -r dist/working/fcl dist/blenderbim/libs/site/packages/
	rm -rf dist/working
endif

ifeq ($(PLATFORM), win)
	mkdir dist/working
	cd dist/working && wget https://files.pythonhosted.org/packages/19/e6/6e9f33fb59e8f27c0e1592bd26e644bc92b85c942b072b2d3854105d5887/python_fcl_win32-0.0.12.post3-py3-none-win_amd64.whl
	cd dist/working && unzip python_fcl*
	cp -r dist/working/fcl dist/blenderbim/libs/site/packages/
	rm -rf dist/working
endif

	cd dist/blenderbim/libs/site/packages/ && wget https://raw.githubusercontent.com/IfcOpenShell/IfcOpenShell/v0.6.0/src/ifcclash/collision.py
	cd dist/blenderbim/libs/site/packages/ && wget https://raw.githubusercontent.com/IfcOpenShell/IfcOpenShell/v0.6.0/src/ifcclash/ifcclash.py

	cd dist/blenderbim/libs/site/packages/ && wget https://raw.githubusercontent.com/IfcOpenShell/IfcOpenShell/v0.6.0/src/ifcdiff/ifcdiff.py
	cd dist/blenderbim/libs/site/packages/ && wget https://raw.githubusercontent.com/IfcOpenShell/IfcOpenShell/v0.6.0/src/ifccsv/ifccsv.py

	cd dist/blenderbim && sed -i "s/999999/$(VERSION)/" __init__.py
	cd dist && zip -r blender28-bim-$(VERSION)-$(PLATFORM).zip ./*
	rm -rf dist/blenderbim

.PHONY: clean
clean:
	rm -rf dist

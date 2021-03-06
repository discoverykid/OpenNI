#############################################################################
# OpenNI makefile.
# 
# default configuration is Release. for a debug version use:
# 	make CFG=Debug
#
# default compiler is g++. for another one use:
#   make CXX=<comp>
#
#############################################################################

# default config is Release
ifndef CFG
	CFG = Release
endif

# tools
CP = cp
RM = rm

# Bin directory
BIN_DIR = ../Bin
# output directory
OUT_DIR = $(BIN_DIR)/$(CFG)

# list all modules
ALL_MODULES = \
	Modules/nimCodecs \
	Modules/nimMockNodes \
	Modules/nimRecorder

# list all utils
ALL_UTILS = \
	Utils/niReg \
	Utils/niLicense

ALL_MONO_PROJS = \
	Wrappers/OpenNI.net

# list all core projects
ALL_CORE_PROJS = \
	OpenNI \
	$(ALL_MODULES) \
	$(ALL_UTILS)

# list all samples
CORE_SAMPLES = \
	Samples/NiSimpleRead \
	Samples/NiViewer \
	Samples/NiBackRecorder \
	Samples/NiConvertXToONI \
	Samples/NiRecordSynthetic \
	Samples/NiSampleModule \
	Samples/NiSimpleCreate \
	Samples/NiCRead \
	Samples/NiSimpleViewer \
	Samples/NiAudioSample \
	Samples/NiUserTracker

MONO_SAMPLES = \
	Samples/SimpleRead.net

MONO_FORMS_SAMPLES = \
	Samples/SimpleViewer.net \
	Samples/UserTracker.net

ALL_SAMPLES = \
	$(CORE_SAMPLES)

# list all projects that are build
ALL_BUILD_PROJS = \
	$(ALL_CORE_PROJS) \
	$(ALL_SAMPLES)

ALL_PROJS = \
	$(ALL_BUILD_PROJS) 
ifneq "$(realpath /usr/bin/gmcs)" ""
	ALL_PROJS += $(ALL_MONO_PROJS)
	ALL_PROJS += $(MONO_SAMPLES)
	ALL_PROJS += $(MONO_FORMS_SAMPLES)
endif

ALL_PROJS_CLEAN = $(foreach proj,$(ALL_PROJS),$(proj)-clean)

# define a function which creates a target for each proj
define CREATE_PROJ_TARGET
$1: 
	$(MAKE) -C $1 CFG=$(CFG)

$1-clean: 
	$(MAKE) -C $1 CFG=$(CFG) clean
endef

################ TARGETS ##################

.PHONY: all $(ALL_PROJS) $(ALL_PROJS_CLEAN) install uninstall clean 

# make all makefiles
all: $(ALL_PROJS)

core: $(ALL_CORE_PROJS)

samples: $(ALL_SAMPLES)

mono_wrapper: Wrappers/OpenNI.net

mono_samples: $(MONO_SAMPLES) $(MONO_FORMS_SAMPLES)

# create projects targets
$(foreach proj,$(ALL_PROJS),$(eval $(call CREATE_PROJ_TARGET,$(proj))))

# additional dependencies
Modules/nimCodecs: OpenNI
Modules/nimMockNodes: OpenNI
Modules/nimRecorder: OpenNI
Utils/niReg: OpenNI
Utils/niLicense: OpenNI
Wrappers/OpenNI.net: OpenNI
Samples/NiSimpleRead: OpenNI
Samples/NiViewer: OpenNI
Samples/NiBackRecorder: OpenNI
Samples/NiConvertXToONI: OpenNI
Samples/NiRecordSynthetic: OpenNI
Samples/NiSampleModule: OpenNI
Samples/NiSimpleCreate: OpenNI
Samples/NiCRead: OpenNI
Samples/NiSimpleViewer: OpenNI
Samples/SimpleRead.net: Wrappers/OpenNI.net
Samples/SimpleViewer.net: Wrappers/OpenNI.net
Samples/UserTracker.net: Wrappers/OpenNI.net

# clean is cleaning all projects
clean: $(ALL_PROJS_CLEAN)

# redist target
redist: all
	cd ../CreateRedist; ./RedistMaker; cd -

# install target
install: redist
	cd ../Redist; ./install.sh; cd -

# uninstall target
uninstall:
	cd ../Redist; ./install.sh -u; cd -



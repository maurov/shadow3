#
# Makefile for shadow3
#
#
#
# Usage:
#       make preprocess : creates *.f90 files (to be exported to other platforms)
#
# HINTS:
#
#   customize next section (only) 
#
#


##-------------------------------------------------------------------------------
##                   THIS SECTION CAN BE CUSTOMIZED 
##-------------------------------------------------------------------------------

#for 32 bits compilation, set this
#(in Ubuntu needs: sudo apt-get install gfortran-multilib )
#32BITS=-m32

#setings for linux
#SO=
#EXE=
#COMPILEOPT=-D_COMPILE4NIX
#STATIC = -static
#STATIC = -static -static-libgfortran -static-libgcc

#settings for mac
#SO=.so
#EXE=
#COMPILEOPT=-D_COMPILE4MAX
#STATIC = 

#settings for windows
SO=.dll
EXE=.exe
COMPILEOPT=-D_COMPILE4WIN
STATIC = -static


#
# customize compiler and flags
#
FC = gfortran
FFLAGS = -cpp -fPIC -ffree-line-length-none $(32BITS) $(STATIC) -O2 -fomit-frame-pointer $(COMPILEOPT)
LINKFLAGS = $(32BITS) $(STATIC)

CPP = cpp -traditional

# LIST OF SOURCE FILES
#

FMODULES = \
	shadow_globaldefinitions.F90 \
	stringio.F90 \
	gfile.F90 \
	shadow_beamio.F90 \
	shadow_math.F90 \
	shadow_variables.F90 \
	shadow_roughness.F90 \
	shadow_kernel.F90 \
	shadow_synchrotron.F90 \
	shadow_pre_sync.F90 \
	shadow_pre_sync_urgent.F90 \
	shadow_preprocessors.F90 \
	shadow_postprocessors.F90 \
	shadow_bind_f.F90 \
	shadow_crl.F90


FMODULESPRE = ${FMODULES:.F90=.f90}

#
# targets
#


preprocess: $(FMODULESPRE) shadow3.f90
	for myfile in $(FMODULESPRE); do \
		echo "Removing lines starting with # in: " $$myfile ; \
		sed -i '/^#/d' $$myfile ; \
	done
	echo "Removing lines starting with # in: shadow3.f90"
	sed -i '/^#/d' shadow3.f90 


all: preprocess

# 
# dependencies and rules
#

%.f90: %.F90
	$(CPP) $(COMPILEOPT) $< -o $@

#
# cleaning 
#
clean:  
	/bin/rm -f *.o *.mod 

	



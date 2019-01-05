
SCRIPTS_DIR=$(abspath $(dir $(lastword $(MAKEFILE_LIST))))
EDAPACK_GCC_DIR=$(abspath $(SCRIPTS_DIR)/..)
BUILD_DIR=$(EDAPACK_GCC_DIR)/build
PACKAGES_DIR=$(EDAPACK_GCC_DIR)/packages

GNU_MIRROR_URL ?= http://mirrors.kernel.org/gnu
GCC_VERSION=7.3.0
GCC_DIR=gcc-$(GCC_VERSION)
GCC_TGZ=$(GCC_DIR).tar.gz
GCC_URL=$(GNU_MIRROR_URL)/gcc/$(GCC_DIR)/$(GCC_TGZ)

ISL_VERSION=0.18
ISL_DIR=isl-$(ISL_VERSION)
ISL_TBZ=$(ISL_DIR).tar.bz2
ISL_URL=ftp://gcc.gnu.org/pub/gcc/infrastructure/$(ISL_TBZ)

GMP_VERSION=6.1.0
GMP_DIR=gmp-$(GMP_VERSION)
GMP_TBZ=$(GMP_DIR).tar.bz2
GMP_URL=$(GNU_MIRROR_URL)/gmp/$(GMP_TBZ)

MPFR_VERSION=3.1.4
MPFR_DIR=mpfr-$(MPFR_VERSION)
MPFR_TBZ=$(MPFR_DIR).tar.bz2
MPFR_URL=$(GNU_MIRROR_URL)/mpfr/$(MPFR_TBZ)

MPC_VERSION=1.0.3
MPC_DIR=mpc-$(MPC_VERSION)
MPC_TGZ=$(MPC_DIR).tar.gz
MPC_URL=$(GNU_MIRROR_URL)/mpc/$(MPC_TGZ)

ifeq (true,$(VERBOSE))
Q=
WGET=wget
TARV=v
else
Q=@
TARV=
WGET=wget -q
endif

UNTARBZ=tar x$(TARV)jf
UNTARGZ=tar x$(TARV)zf
UNTARXZ=tar x$(TARV)Jf

all : $(BUILD_DIR)/gcc.d

$(BUILD_DIR)/gcc.d : \
	$(PACKAGES_DIR)/$(GCC_TGZ) \
	$(PACKAGES_DIR)/$(GMP_TBZ) \
	$(PACKAGES_DIR)/$(MPFR_TBZ) \
	$(PACKAGES_DIR)/$(ISL_TBZ) \
	$(PACKAGES_DIR)/$(MPC_TGZ)
	$(Q)rm -rf $(BUILD_DIR)/gcc
	$(Q)mkdir -p $(BUILD_DIR)/gcc
	$(Q)cd $(BUILD_DIR)/gcc ; $(UNTARGZ) $(PACKAGES_DIR)/$(GCC_TGZ)
	$(Q)cd $(BUILD_DIR)/gcc ; $(UNTARBZ) $(PACKAGES_DIR)/$(GMP_TBZ)
	$(Q)cd $(BUILD_DIR)/gcc ; $(UNTARGZ) $(PACKAGES_DIR)/$(MPC_TGZ)
	$(Q)cd $(BUILD_DIR)/gcc ; $(UNTARBZ) $(PACKAGES_DIR)/$(MPFR_TBZ)
	$(Q)cd $(BUILD_DIR)/gcc ; $(UNTARBZ) $(PACKAGES_DIR)/$(ISL_TBZ)
	$(Q)cd $(BUILD_DIR)/gcc ; mv $(GMP_DIR) $(GCC_DIR)/gmp
	$(Q)cd $(BUILD_DIR)/gcc ; mv $(MPC_DIR) $(GCC_DIR)/mpc
	$(Q)cd $(BUILD_DIR)/gcc ; mv $(MPFR_DIR) $(GCC_DIR)/mpfr
	$(Q)cd $(BUILD_DIR)/gcc ; mv $(ISL_DIR) $(GCC_DIR)/isl
	$(Q)cd $(BUILD_DIR)/gcc/$(GCC_DIR) ; \
		./configure --prefix=$(BUILD_DIR)/gcc/gcc \
			--enable-languages=c,c++ \
			--disable-multilib
	$(Q)cd $(BUILD_DIR)/gcc/$(GCC_DIR) ; $(MAKE)
	$(Q)cd $(BUILD_DIR)/gcc/$(GCC_DIR) ; $(MAKE) install
	$(Q)touch $@


$(PACKAGES_DIR)/$(GCC_TGZ) :
	$(Q)mkdir -p $(PACKAGES_DIR)
	$(Q)$(WGET) -O $@ $(GCC_URL)
 
$(PACKAGES_DIR)/$(GMP_TBZ) :
	$(Q)mkdir -p $(PACKAGES_DIR)
	$(Q)$(WGET) -O $@ $(GMP_URL)

$(PACKAGES_DIR)/$(MPC_TGZ) :
	$(Q)mkdir -p $(PACKAGES_DIR)
	$(Q)$(WGET) -O $@ $(MPC_URL)

$(PACKAGES_DIR)/$(MPFR_TBZ) :
	$(Q)mkdir -p $(PACKAGES_DIR)
	$(Q)$(WGET) -O $@ $(MPFR_URL)

$(PACKAGES_DIR)/$(ISL_TBZ) :
	$(Q)mkdir -p $(PACKAGES_DIR)
	$(Q)$(WGET) -O $@ $(ISL_URL)



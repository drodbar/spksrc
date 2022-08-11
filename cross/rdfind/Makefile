PKG_NAME = rdfind
PKG_VERS = 1.5.0
PKG_EXT = tar.gz
PKG_DOWNLOAD_METHOD = git
PKG_GIT_HASH = 008d07ac8c268710bf25f4f476b72ec61f1a998b
PKG_DIST_SITE = https://github.com/pauldreik/rdfind
PKG_DIST_FILE = $(PKG_NAME)-git$(PKG_GIT_HASH).$(PKG_EXT)
PKG_DIR = $(PKG_NAME)-git$(PKG_GIT_HASH)

DEPENDS = cross/nettle

HOMEPAGE = https://github.com/pauldreik/rdfind/
COMMENT  = rdfind - Search duplicates to delete them or replace them with hard/soft links
LICENSE  = GPLv2

ADDITIONAL_CFLAGS = -fpic -fPIC -O3 -D_FILE_OFFSET_BITS=64

GNU_CONFIGURE = 1

POST_DEPEND_TARGET = test_rdfind_deps
PRE_CONFIGURE_TARGET = bootstrap_rdfind
POST_INSTALL_TARGET = test_rdfind

include ../../mk/spksrc.cross-cc.mk

SYSROOT_LIB = $(PWD)/../../toolchain/$(TC)/work/$(TC_TARGET)/$(TC_TARGET)/sysroot/lib
TEST_LIB_DIR = $(WORK_DIR)/lib
ENV += QEMU_LD_PREFIX=$(WORK_DIR)

green = \033[0;32m
blue = \033[1;34m
clr = \033[m

prepare_test_libs:
	mkdir -pv $(TEST_LIB_DIR) && \
	ln -svf $(SYSROOT_LIB)/* $(TEST_LIB_DIR)/ && \
	ln -svf $(WORK_DIR)/nettle-3.7.2/.lib/libnettle.so.8 $(TEST_LIB_DIR)

.PHONY: bootstrap_rdfind
bootstrap_rdfind:
	@echo "$(green)Bootstraping $(clr)[$(blue)rdfind$(clr)] $(green)repository$(clr)"
	$(RUN) ; ./bootstrap.sh

.PHONY: test_rdfind_deps
test_rdfind_deps: prepare_test_libs
	@echo "$(green)Running rdfind dependency tests $(clr)[$(blue)make check$(clr)] $(green)for $(clr)($(blue)gmp$(clr))"
	$(ENV) $(MAKE) -C $(WORK_DIR)/gmp-* check

.PHONY: test_rdfind
test_rdfind:
	@echo "$(green)Running $(clr)[$(blue)rdfind$(clr)]$(green) tests$(clr)"
	if [ "$(shell id -u)" = 0 ]; then\
	    $(RUN) setpriv --reuid=1000 --regid=1000 --clear-groups $(MAKE) check; \
	else \
	    $(RUN) $(MAKE) check; \
	fi

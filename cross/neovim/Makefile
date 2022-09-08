PKG_NAME = neovim
PKG_VERS = 0.7.2
PKG_EXT = tar.gz
PKG_DOWNLOAD_METHOD = git
PKG_GIT_HASH = e8ee6733926db83ef216497a1d660a173184ff39
PKG_DIST_SITE = https://github.com/neovim/neovim
PKG_DIST_FILE = $(PKG_NAME)-git$(PKG_GIT_HASH).$(PKG_EXT)
PKG_DIR = $(PKG_NAME)-git$(PKG_GIT_HASH)

HOMEPAGE = https://neovim.io
COMMENT  = Hyperextensible Vim-based text editor
LICENSE  = Apache 2.0 and VIM License

#ADDITIONAL_CFLAGS = -fpic -fPIC -O3 -D_FILE_OFFSET_BITS=64

CONFIGURE_TARGET = nop
CMAKE_ARGS = CMAKE_BUILD_TYPE=Release CMAKE_INSTALL_PREFIX=/var/packages/neovim

include ../../mk/spksrc.cross-cc.mk

POST_DEPEND_TARGET = prepare_test_libs
SYSROOT_LIB = $(PWD)/../../toolchain/$(TC)/work/$(TC_TARGET)/$(TC_TARGET)/sysroot/lib
TEST_LIB_DIR = $(WORK_DIR)/lib
ENV += QEMU_LD_PREFIX=$(WORK_DIR)

.PHONY: prepare_test_libs
prepare_test_libs:
	mkdir -pv $(TEST_LIB_DIR) && \
	ln -svf $(SYSROOT_LIB)/* $(TEST_LIB_DIR)/ && \

#.PHONY: test_rdfind_deps
#test_rdfind_deps: prepare_test_libs
#	@echo "$(green)Running rdfind dependency tests $(clr)[$(blue)make check$(clr)] $(green)for $(clr)($(blue)gmp$(clr))"
#	$(ENV) AM_COLOR_TESTS=always $(MAKE) -C $(WORK_DIR)/gmp-* check

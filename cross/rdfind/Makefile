PKG_NAME = rdfind
PKG_VERS = 1.5.0
PKG_EXT = tar.gz
PKG_DOWNLOAD_METHOD = git
PKG_GIT_HASH = 008d07ac8c268710bf25f4f476b72ec61f1a998b
PKG_DIST_SITE = https://github.com/pauldreik/rdfind
PKG_DIST_FILE = $(PKG_NAME)-git$(PKG_GIT_HASH).$(PKG_EXT)
PKG_DIR = $(PKG_NAME)-git$(PKG_GIT_HASH)
BETA = 1

DEPENDS = cross/nettle

HOMEPAGE = https://github.com/pauldreik/rdfind/
COMMENT  = rdfind - Search duplicates to delete them or replace them with hard/soft links
LICENSE  = GPLv2

ADDITIONAL_CFLAGS = -fpic -fPIC -O3 -D_FILE_OFFSET_BITS=64

PRE_CONFIGURE_TARGET = rdfind_pre_configure
GNU_CONFIGURE = 1

#POST_COMPILE_TARGET = rdfind_post_compile

include ../../mk/spksrc.cross-cc.mk

.PHONY: rdfind_pre_configure
rdfind_pre_configure:
	$(RUN) ; ./bootstrap.sh

.PHONY: rdfind_post_compile
rdfind_post_compile:
	$(RUN)
	@if [ "$(shell id -u)" = 0 ]; then \
	    $(RUN) setpriv --reuid=1000 --regid=1000 --clear-groups $(MAKE) check; \
	else \
	    $(RUN) $(MAKE) $(AM_MAKEFLAGS) check; \
	fi

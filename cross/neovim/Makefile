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

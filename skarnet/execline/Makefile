#
# Copyright (C) 2024 Scott Zuk <zooknotic@proton.me>
# SPDX-License-Identifier: ISC
#

include $(TOPDIR)/rules.mk

PKG_NAME:=execline
PKG_VERSION:=2.9.4.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://skarnet.org/software/execline
PKG_HASH:=9ab55d561539dfa76ff4a97906fa995fc4a288e3de5225cb1a9d8fa9e9ebc49b

PKG_LICENSE:=ISC
PKG_LICENSE_FILES:=COPYING

PKG_MAINTAINER:=Scott Zuk <zooknotic@proton.me>

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

PKG_BUILD_DEPENDS:=skalibs

include $(INCLUDE_DIR)/package.mk


define Package/execline
  SECTION:=admin
  CATEGORY:=Administration
  TITLE:=Skarnet.org execline non-interactive scripting language
  URL:=http://skarnet.org/software/execline/
  DEPENDS:=+libpthread
endef

define Package/execline/description
  execline is a (non-interactive) scripting language, like sh - but its syntax is
  quite different from a traditional shell syntax. The execlineb program is meant
  to be used as an interpreter for a text file; the other commands are essentially
  useful inside an execlineb script.
  Used by the s6 suite.
endef


CONFIGURE_ARGS:= \
	--target=$(GNU_TARGET_NAME) \
	--with-sysdeps=$(STAGING_DIR)/usr/lib/skalibs/sysdeps \
	--with-lib=$(STAGING_DIR)/usr/lib/skalibs \
	--enable-multicall


# Static libraries and headers will be available in $STAGING_DIR for s6, s6-rc
define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/include/* $(1)/usr/include/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/* $(1)/usr/lib/
endef

# Multicall binary and symlinks
define Package/execline/install
	$(INSTALL_DIR) $(1)/bin
	$(CP) $(PKG_INSTALL_DIR)/bin/* $(1)/bin/
endef

$(eval $(call BuildPackage,execline))

#
# Copyright (C) 2024 Scott Zuk <zooknotic@proton.me>
# SPDX-License-Identifier: ISC
#

include $(TOPDIR)/rules.mk

PKG_NAME:=skalibs
PKG_VERSION:=2.14.1.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://skarnet.org/software/skalibs
PKG_HASH:=b6b79b816f4ba0b6801676b0ed4179b59c8c7809eeffe26db672e404636befc3

PKG_LICENSE:=ISC
PKG_LICENSE_FILES:=COPYING

PKG_MAINTAINER:=Scott Zuk <zooknotic@proton.me>

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

PKG_BUILD_DEPENDS:=

include $(INCLUDE_DIR)/package.mk


define Package/skalibs
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Skarnet.org skalibs general-purpose libraries
  URL:=http://skarnet.org/software/skalibs/
  DEPENDS:=+libpthread
endef

define Package/skalibs/description
  skalibs is a package centralizing the free software / open source C development
  files used for building all software at skarnet.org. It contains essentially
  general-purpose libraries and is required for building the s6 suite.
endef


CONFIGURE_ARGS:= \
	--target=$(GNU_TARGET_NAME) \
	--enable-iopause-select \
	--with-sysdep-devurandom=yes \
	--with-sysdep-posixspawnearlyreturn=no


# Static libraries and headers will be available in $STAGING_DIR for execline, s6, s6-rc
define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/include/* $(1)/usr/include/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/* $(1)/usr/lib/
endef

# Dynamic library
define Package/skalibs/install
	$(INSTALL_DIR) $(1)/lib
	$(CP) $(PKG_INSTALL_DIR)/lib/*.so* $(1)/lib/
endef

$(eval $(call BuildPackage,skalibs))

#
# Copyright (C) 2024 Scott Zuk <zooknotic@proton.me>
# SPDX-License-Identifier: ISC
#

include $(TOPDIR)/rules.mk

PKG_NAME:=s6
PKG_VERSION:=2.12.0.3
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://skarnet.org/software/s6
PKG_HASH:=800d31226f6c25cdd3ec0b65240f80b56ce5ec137341d0a8d154e77638e58103

PKG_LICENSE:=ISC
PKG_LICENSE_FILES:=COPYING

PKG_MAINTAINER:=Scott Zuk <zooknotic@proton.me>

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

PKG_BUILD_DEPENDS:=skalibs

include $(INCLUDE_DIR)/package.mk


define Package/s6
  SECTION:=admin
  CATEGORY:=Administration
  TITLE:=Skarnet.org small and secure supervision software suite
  URL:=http://skarnet.org/software/s6/
  DEPENDS:=+execline +libpthread
endef

define Package/s6/description
  s6 is a small suite of programs for UNIX, designed to allow process supervision
  (a.k.a service supervision), in the line of daemontools and runit, as well as
  various operations on processes and daemons. It is meant to be a toolbox for
  low-level process and service administration, providing different sets of
  independent tools that can be used within or without the framework, and that can
  be assembled together to achieve powerful functionality with a very small amount
  of code.
endef


CONFIGURE_ARGS:= \
	--target=$(GNU_TARGET_NAME) \
	--with-sysdeps=$(STAGING_DIR)/usr/lib/skalibs/sysdeps \
	--with-lib=$(STAGING_DIR)/usr/lib/skalibs \
	--with-lib=$(STAGING_DIR)/usr/lib/execline


# Static libraries and headers will be available in $STAGING_DIR for s6-rc
define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/include/* $(1)/usr/include/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/* $(1)/usr/lib/
endef

define Package/s6/install
	$(INSTALL_DIR) $(1)/bin
	$(CP) $(PKG_INSTALL_DIR)/bin/* $(1)/bin/
endef

$(eval $(call BuildPackage,s6))

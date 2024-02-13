#
# Copyright (C) 2024 Scott Zuk <zooknotic@proton.me>
# SPDX-License-Identifier: ISC
#

include $(TOPDIR)/rules.mk

PKG_NAME:=s6-rc
PKG_VERSION:=0.5.4.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://skarnet.org/software/s6-rc
PKG_HASH:=00bdfa596fa7161512e972ec9282a2abd8fd0e31f09177bad7a2bc3d8f283982

PKG_LICENSE:=ISC
PKG_LICENSE_FILES:=COPYING

PKG_MAINTAINER:=Scott Zuk <zooknotic@proton.me>

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

PKG_BUILD_DEPENDS:=skalibs

include $(INCLUDE_DIR)/package.mk


define Package/s6-rc
  SECTION:=admin
  CATEGORY:=Administration
  TITLE:=Skarnet.org service manager for s6-based systems
  URL:=http://skarnet.org/software/s6-rc/
  DEPENDS:=+s6 +execline +libpthread
endef

define Package/s6-rc/description
  s6-rc is a service manager for s6-based systems, i.e. a suite of programs that
  can start and stop services, both long-running daemons and one-time
  initialization scripts, in the proper order according to a dependency tree. It
  ensures that long-running daemons are supervised by the s6 infrastructure, and
  that one-time scripts are also run in a controlled environment.
endef


CONFIGURE_ARGS:= \
	--target=$(GNU_TARGET_NAME) \
	--with-sysdeps=$(STAGING_DIR)/usr/lib/skalibs/sysdeps \
	--with-lib=$(STAGING_DIR)/usr/lib/skalibs \
	--with-lib=$(STAGING_DIR)/usr/lib/execline \
	--with-lib=$(STAGING_DIR)/usr/lib/s6


define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/include/* $(1)/usr/include/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/* $(1)/usr/lib/
endef

define Package/s6-rc/install
	$(INSTALL_DIR) $(1)/bin
	$(INSTALL_DIR) $(1)/libexec
	$(CP) $(PKG_INSTALL_DIR)/bin/* $(1)/bin/
	$(CP) $(PKG_INSTALL_DIR)/libexec/* $(1)/libexec/
endef

$(eval $(call BuildPackage,s6-rc))

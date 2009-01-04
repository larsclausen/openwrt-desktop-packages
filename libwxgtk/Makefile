#
# Copyright (C) 2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# $Id$

include $(TOPDIR)/rules.mk

PKG_NAME:=libwxgtk
PKG_VERSION:=2.8.9
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=@SF/wxwindows
#PKG_MD5SUM:=c6d873b254eda073d722064003e304b6

include $(INCLUDE_DIR)/package.mk

PKG_INSTALL=1

EXTRA_CFLAGS+= \
	-I$(STAGING_DIR)/usr/lib/libintl/include \
	-I$(STAGING_DIR)/usr/lib/libiconv/include \

EXTRA_LDFLAGS+= \
	-Wl,-rpath-link=$(STAGING_DIR)/usr/lib \
	-L$(STAGING_DIR)/usr/lib/libintl/lib \
	-L$(STAGING_DIR)/usr/lib/libiconv/lib

define Package/libwxgtk
  SECTION:=xorg-libs
  CATEGORY:=Xorg
  SUBMENU:=framework
  TITLE:=libwxgtk
  URL:=http://www.wxwidgets.org/
  DEPENDS:=+gtk2
  PROVIDES:=libwxbase
endef

define Package/libwxgtk/description
endef

define Build/Configure
	$(call Build/Configure/Default, \
		--enable-unicode \
		--enable-largefile \
		--enable-intl \
		--with-regex \
		--with-x \
		--disable-no_rtti \
	)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(2)/bin
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/usr/bin/wx-config \
		$(2)/bin/wx-config

	$(SED) "s,^\(prefix\|exec_prefix\)=.*,\1=$(STAGING_DIR)/usr,g" $(2)/bin/wx-config

	$(INSTALL_DIR) $(2)/share/aclocal
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/share/aclocal/* \
		$(2)/share/aclocal

	$(INSTALL_DIR) $(1)/usr/include/wx-2.8/wx
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/include/wx-2.8/wx/* \
		$(1)/usr/include/wx-2.8/wx

	$(INSTALL_DIR) $(1)/usr/lib/
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/*.so* \
		$(1)/usr/lib/

	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/wx/ \
		$(1)/usr/lib/
endef

define Package/libwxgtk/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/*.so* \
		$(1)/usr/lib/
endef

$(eval $(call BuildPackage,libwxgtk))

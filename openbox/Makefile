#
# Copyright (C) 2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=openbox
PKG_VERSION:=3.4.7.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://icculus.org/openbox/releases
PKG_MD5SUM:=
PKG_FIXUP:=libtool

include $(INCLUDE_DIR)/package.mk

PKG_INSTALL=1

TARGET_CFLAGS+= \
	-I$(STAGING_DIR)/usr/lib/libintl/include/ \
	-I$(STAGING_DIR)/usr/lib/libiconv/include/

TARGET_LDFLAGS+= \
	-Wl,-rpath-link=$(STAGING_DIR)/usr/lib \
	-L$(STAGING_DIR)/usr/lib/libintl/lib \
	-L$(STAGING_DIR)/usr/lib/libiconv/lib

define Package/libobrender
  SECTION:=xorg-lib
  CATEGORY:=Xorg
  SUBMENU:=libraries
  TITLE:=openbox render library
  DEPENDS:=+glib2 +libxml2
endef

define Package/libobparser
  SECTION:=xorg-lib
  CATEGORY:=Xorg
  SUBMENU:=libraries
  TITLE:=openbox parser library
  DEPENDS:=+glib2 +libobrender +pango +libXft +libXcursor +libxml2
endef

define Package/openbox
  SECTION:=xorg-app
  CATEGORY:=Xorg
  SUBMENU:=app
  TITLE:=openbox windowmanager
  DEPENDS:=+libobrender +libobparser +libstartup-notification
endef

define Package/openbox-themes
  SECTION:=xorg-data
  CATEGORY:=Xorg
  SUBMENU:=data
  TITLE:=openbox
endef

define Build/Configure
	(cd $(PKG_BUILD_DIR); autoreconf)
	$(call Build/Configure/Default)
endef

define Package/libobrender/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libobrender.so* \
		$(1)/usr/lib/
endef

define Package/libobparser/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libobparser.so* \
		$(1)/usr/lib/
endef

define Package/openbox/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/usr/bin/* \
		$(1)/usr/bin

	$(INSTALL_DIR) $(1)/etc/xdg/openbox
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/etc/xdg/openbox/* \
		$(1)/etc/xdg/openbox/

	$(INSTALL_DIR) $(1)/usr/share/{gnome/wm-properties,pixmaps,xsessions}
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/share/gnome/wm-properties/* \
		$(1)/usr/share/gnome/wm-properties/

	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/share/pixmaps/* \
		$(1)/usr/share/pixmaps/

	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/share/xsessions/* \
		$(1)/usr/share/xsessions/
endef

define Package/openbox-themes/install
	$(INSTALL_DIR) $(1)/usr/share/themes/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/share/themes/* \
		$(1)/usr/share/themes/
endef

$(eval $(call BuildPackage,libobparser))
$(eval $(call BuildPackage,libobrender))
$(eval $(call BuildPackage,openbox))
$(eval $(call BuildPackage,openbox-themes))

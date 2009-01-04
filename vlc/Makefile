#
# Copyright (C) 2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# $Id$

include $(TOPDIR)/rules.mk

PKG_NAME:=vlc
PKG_VERSION:=0.8.6i
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=ftp://root24.eu/pub/videolan/vlc/0.8.6i/
#PKG_MD5SUM:=c6d873b254eda073d722064003e304b6
PKG_FIXUP:=libtool

include $(INCLUDE_DIR)/package.mk

PKG_INSTALL=1

EXTRA_CFLAGS+= -fno-fast-math \
	-I$(STAGING_DIR)/usr/lib/libintl/include \
	-I$(STAGING_DIR)/usr/lib/libiconv/include \

EXTRA_LDFLAGS+= \
	-Wl,-rpath-link=$(STAGING_DIR)/usr/lib \
	-Wl,-rpath-link=$(STAGING_DIR)/usr/lib/libintl/lib \
	-Wl,-rpath-link=$(STAGING_DIR)/usr/lib/libiconv/lib \
	-L$(STAGING_DIR)/usr/lib/libintl/lib \
	-L$(STAGING_DIR)/usr/lib/libiconv/lib \
	-lX11 -lgtk-x11-2.0 -lgdk-x11-2.0 -latk-1.0 -lgdk_pixbuf-2.0 -lpango-1.0 -lgobject-2.0 -lgmodule-2.0 -lgthread-2.0 -lglib-2.0

define Package/vlc
  SECTION:=multimedia
  CATEGORY:=Multimedia
  TITLE:=vlc
  URL:=http://www.videolan.org
  DEPENDS:=+libmad +libvorbis +libtheora +libogg +ffmpeg +libgcrypt +dbus +libiconv +libwxgtk
endef

define Package/vlc/description
	gstreamer good plugins
endef

define Build/Configure
	$(call Build/Configure/Default, \
		--enable-libtool \
		--enable-static \
		--enable-shared \
		--disable-postproc \
		--disable-a52 \
		--disable-sdl \
		--disable-sdl-image \
		--disable-qt4 \
		--disable-skins2 \
		--disable-opengl \
		--disable-glx \
		--disable-ffmpeg \
		--disable-libmpeg2 \
		--enable-wxwidgets \
		, \
		CC="$(TARGET_CXX)" \
		GCC="$(TARGET_CXX)" \
	)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(2)/bin
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/bin/vlc-config \
		$(2)/bin/

	$(INSTALL_DIR) $(1)/usr/include/vlc
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/include/vlc/*.h \
		$(1)/usr/include/vlc/

#	$(INSTALL_DIR) $(1)/usr/include/vlc/plugins
#	$(INSTALL_DATA) \
#		$(PKG_INSTALL_DIR)/usr/include/vlc/plugins/*.h \
#		$(1)/usr/include/vlc/plugins/

	$(INSTALL_DIR) $(1)/usr/lib/
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/*.{so*,a} \
		$(1)/usr/lib/

#	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
#	$(INSTALL_DATA) \
#		$(PKG_INSTALL_DIR)/usr/lib/pkgconfig/* \
#		$(1)/usr/lib/pkgconfig/
endef

define Package/vlc/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/usr/bin/* \
		$(1)/usr/bin/

	$(INSTALL_DIR) $(1)/usr/lib/
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/*.{so*,a} \
		$(1)/usr/lib/

	$(INSTALL_DIR) $(1)/usr/lib/vlc
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/vlc/* \
		$(1)/usr/lib/vlc/

	$(INSTALL_DIR) $(1)/usr/share/applications
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/share/applications/* \
		$(1)/usr/share/applications

	$(INSTALL_DIR) $(1)/usr/share/vlc
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/share/vlc/* \
		$(1)/usr/share/vlc
endef

$(eval $(call BuildPackage,vlc))

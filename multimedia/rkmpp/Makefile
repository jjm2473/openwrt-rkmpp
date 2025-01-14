#
# Copyright (C) 2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=rkmpp
PKG_VERSION:=2023-06-12
PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_VERSION:=f91f152a1a8e5bd95174498c834e7a734e2ce4de
PKG_SOURCE_URL_FILE:=$(PKG_SOURCE_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/JeffyCN/mirrors/archive/
PKG_HASH:=1598ae4cb57bebd5140f91cd222ac45d588aec32b91d1a3979a596645363addb

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

TAR_OPTIONS:=--strip-components 1 $(TAR_OPTIONS)
TAR_CMD=$(HOST_TAR) -C $(1) $(TAR_OPTIONS)

define Package/rkmpp
  SECTION:=multimedia
  CATEGORY:=Multimedia
  TITLE:=Rockchip MPP
  DEPENDS:=@aarch64 +libstdcpp
  URL:=https://github.com/JeffyCN/mirrors/tree/mpp-dev
endef

define Package/rkmpp/description
 Rockchip Media Process Platform (MPP)
endef

define Package/rkmpp-demo
$(call Package/rkmpp)
  TITLE+= Demo
  DEPENDS:=+rkmpp
endef

define Package/rkmpp-demo/description
$(call Package/rkmpp/description)

This package provides the demo.
endef

CMAKE_OPTIONS += -DCMAKE_BUILD_TYPE=Release \
	-DHAVE_DRM=ON

define Package/rkmpp/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/lib*.so.* $(1)/usr/lib/
endef

define Package/rkmpp-demo/install
	$(INSTALL_DIR) $(1)/usr
	$(CP) $(PKG_INSTALL_DIR)/usr/bin $(1)/usr/
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/rockchip $(1)/usr/include/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib $(1)/usr/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/*.pc $(1)/usr/lib/pkgconfig/
endef

$(eval $(call BuildPackage,rkmpp))
$(eval $(call BuildPackage,rkmpp-demo))

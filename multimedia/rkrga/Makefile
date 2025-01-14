#
# Copyright (C) 2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=rkrga
PKG_VERSION:=1.9.1
PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_VERSION:=039967ece0d41e67310ce88fb354dce6f64f38a7
PKG_SOURCE_URL_FILE:=$(PKG_SOURCE_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/jjm2473/librga/archive/
PKG_HASH:=2e0f244c113223c7abb737190264d663f1a285500d61c847ead9921d97f26a76

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

TAR_OPTIONS:=--strip-components 1 $(TAR_OPTIONS)
TAR_CMD=$(HOST_TAR) -C $(1) $(TAR_OPTIONS)

define Package/rkrga
  SECTION:=multimedia
  CATEGORY:=Multimedia
  TITLE:=Rockchip RGA
  DEPENDS:=@aarch64 +libstdcpp +libdrm
  URL:=https://github.com/jjm2473/librga
endef

define Package/rkrga/description
 Rockchip RGA (Raster Graphic Acceleration Unit)
 is an independent 2D hardware accelerator that can be used to accelerate point/line drawing and perform common 2D graphics operations such as image scaling, rotation, bitBlt, and alpha blending.The code in this repository implements the RGA user space driver and provides a series of 2D graphics operation APIs.
endef

define Package/rkrga-demo
$(call Package/rkrga)
  TITLE+= Demo
  DEPENDS:=+rkrga
endef

define Package/rkrga-demo/description
$(call Package/rkrga/description)

This package provides the demo.
endef

CMAKE_OPTIONS += -DCMAKE_BUILD_TYPE=Release \
	-DCMAKE_BUILD_TARGET=cmake_linux

define Package/rkrga/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/librga.so $(1)/usr/lib/
endef

define Package/rkrga-demo/install
	$(INSTALL_DIR) $(1)/usr/bin $(1)/usr/data
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/rgaImDemo $(1)/usr/bin/
	$(CP) $(PKG_BUILD_DIR)/samples/sample_file/in0w1280-h720-rgba8888.bin $(1)/usr/data/
	$(CP) $(PKG_BUILD_DIR)/samples/sample_file/in1w1280-h720-rgba8888.bin $(1)/usr/data/
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include $(1)/usr/include/rga
	$(CP) $(PKG_INSTALL_DIR)/usr/lib $(1)/usr/
endef

$(eval $(call BuildPackage,rkrga))
$(eval $(call BuildPackage,rkrga-demo))

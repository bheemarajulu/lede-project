#
# Copyright (C) 2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=u-boot
PKG_VERSION:=2013.01

PKG_RELEASE=$(PKG_SOURCE_VERSION)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL=https://github.com/SolidRun/u-boot-armada38x.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=ea24ac55a2ed199a1f511c1f7ebbfce2976d6c39
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_LICENSE:=GPL-2.0 GPL-2.0+
PKG_LICENSE_FILES:=Licenses/README

PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/uboot-solidrun-clearfog
  SECTION:=boot
  CATEGORY:=Boot Loaders
  DEPENDS:=@TARGET_mvebu @GCC_USE_VERSION_4
  TITLE:=Downstream U-Boot for SolidRun ClearFog A1
  URL:=http://www.denx.de/wiki/U-Boot
endef

define Build/Configure
	+$(MAKE) $(PKG_JOBS) -C $(PKG_BUILD_DIR) armada_38x_clearfog_config
endef

define Build/Compile
	+$(MAKE) $(PKG_JOBS) -C $(PKG_BUILD_DIR) CROSS_COMPILE=$(TARGET_CROSS) \
		u-boot.mmc
endef

define Package/uboot-solidrun-clearfog/install
	$(INSTALL_DIR) $(1)/boot
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/u-boot.mmc $(1)/boot/

	$(CP) $(PKG_BUILD_DIR)/u-boot.mmc $(BIN_DIR)/u-boot.mmc
endef

$(eval $(call BuildPackage,uboot-solidrun-clearfog))

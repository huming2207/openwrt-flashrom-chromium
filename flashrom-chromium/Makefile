#
# Copyright (C) 2010-2017 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=flashrom-chromium

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=a845072c713fa2d5b129d900837b57ca3fe0b9bb
PKG_SOURCE_URL:=https://github.com/huming2207/flashrom_google.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_SOURCE_VERSION)
PKG_MAINTAINER:=Ming Hu <huming@xcloud.cc>

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(BUILD_VARIANT)/$(PKG_SOURCE_SUBDIR)

PKG_LICENSE:=GPL-2.0
PKG_LICENSE_FILES:=COPYING

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include flashrom-chromium.mk

TARGET_CFLAGS+= \
	-std=gnu89

MAKE_FLAGS+= \
	PREFIX="/usr"

define Package/flashrom-chromium/default
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=FlashROM Utility (with ChromiumOS mods)
  URL:=http://www.flashrom.org/
endef

define Package/flashrom-chromium
  $(Package/flashrom-chromium/default)
  TITLE+= (full)
  DEPENDS+= \
    +(TARGET_x86||TARGET_x86_64):dmidecode \
    +libftdi1 \
    +libusb-1.0 \
    +libusb-compat \
    +pciutils
  VARIANT:=full
  DEFAULT_VARIANT:=1
endef

define Package/flashrom-chromium-pci
  $(Package/flashrom-chromium/default)
  TITLE+= (pci)
  DEPENDS+= \
    +(TARGET_x86||TARGET_x86_64):dmidecode \
    +pciutils
  VARIANT:=pci
endef

define Package/flashrom-chromium-spi
  $(Package/flashrom-chromium/default)
  TITLE+= (spi)
  VARIANT:=spi
endef

define Package/flashrom-chromium-usb
  $(Package/flashrom-chromium/default)
  TITLE+= (usb)
  DEPENDS+= \
    +libftdi1 \
    +libusb-1.0 \
    +libusb-compat
  VARIANT:=usb
endef

define Package/flashrom-chromium/default/description
 flashrom is an utility for identifying, reading, writing, verifying
 and erasing flash chips. It's often used to flash BIOS/EFI/coreboot
 /firmware images.
endef
Package/flashrom-chromium/description = $(Package/flashrom-chromium/default/description)
Package/flashrom-chromium-pci/description = $(Package/flashrom-chromium/default/description)
Package/flashrom-chromium-spi/description = $(Package/flashrom-chromium/default/description)
Package/flashrom-chromium-usb/description = $(Package/flashrom-chromium/default/description)

define Package/flashrom-chromium/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/flashrom $(1)/usr/sbin/flashrom
endef
define Package/flashrom-chromium-pci/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/flashrom $(1)/usr/sbin/flashrom-pci
endef
define Package/flashrom-chromium-spi/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/flashrom $(1)/usr/sbin/flashrom-spi
endef
define Package/flashrom-chromium-usb/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/flashrom $(1)/usr/sbin/flashrom-usb
endef

$(eval $(call BuildPackage,flashrom-chromium))
$(eval $(call BuildPackage,flashrom-chromium-pci))
$(eval $(call BuildPackage,flashrom-chromium-spi))
$(eval $(call BuildPackage,flashrom-chromium-usb))

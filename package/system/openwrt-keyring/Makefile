# Copyright (C) 2016 LEDE project

include $(TOPDIR)/rules.mk

PKG_NAME:=openwrt-keyring
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL=https://github.com/immortalwrt/keyring.git
PKG_SOURCE_DATE:=2024-11-01
PKG_SOURCE_VERSION:=c5d6bdf2776ae5b0eaae547ced1767761f1a20d1
PKG_MIRROR_HASH:=4f655d641df907598ae3d745e5ae4278d4f2a1085ff026ea23159cb84eacf014

PKG_MAINTAINER:=John Crispin <john@phrozen.org>
PKG_LICENSE:=GPL-2.0

include $(INCLUDE_DIR)/package.mk

define Package/openwrt-keyring
  SECTION:=base
  CATEGORY:=Base system
  PROVIDES:=lede-keyring
  TITLE:=ImmortalWrt Developer Keyring
  URL:=https://openwrt.org/docs/guide-user/security/signatures
endef

define Package/openwrt-keyring/description
  The keyring of with the developer using and gpg public keys.
endef

Build/Compile=

ifneq ($(CONFIG_USE_APK),)
define Package/openwrt-keyring/install
	$(INSTALL_DIR) $(1)/etc/apk/keys/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/apk/*.pem $(1)/etc/apk/keys/
endef
else
define Package/openwrt-keyring/install
	$(INSTALL_DIR) $(1)/etc/opkg/keys/
	# Public usign key for unattended snapshot builds
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/usign/b5043e70f9a75cde $(1)/etc/opkg/keys/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/usign/8ead5420c4005b0d $(1)/etc/opkg/keys/
endef
endif

$(eval $(call BuildPackage,openwrt-keyring))

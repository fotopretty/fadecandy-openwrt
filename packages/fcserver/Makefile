include $(TOPDIR)/rules.mk

PKG_NAME:=fcserver
PKG_VERSION:=0.2

PKG_REV:=a2e1aef7ad2a81c7ad090148cd01ad4251e12f86

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=git://github.com/pixelmatix/fadecandy
PKG_SOURCE_PROTO:=git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=$(PKG_REV)

#PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

define Package/fcserver
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=FadeCandy Server
	URL:=https://github.com/pixelmatix/fadecandy
	DEPENDS:=+libpthread +librt +uclibcxx +libstdcpp +libc +libusbx 
endef

define Package/fcserver/description
	FadeCandy server
endef

define Build/Compile
	$(MAKE) -C $(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)/server \
		CXX=$(TARGET_CC) \
		CC="$(TARGET_CC) -fhonour-copts" \
		STRIP_CMD="$(TARGET_STRIP) $(TARGET)"
endef

define Package/fcserver/install
	$(INSTALL_DIR) $(1)/usr
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) $(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)/server/fcserver $(1)/usr/bin/
	$(CP) ./src/fcserver.config $(1)/etc/
	$(INSTALL_BIN) ./src/fcserver.init $(1)/etc/init.d/fcserver
endef

define Package/fcserver/postinst
	#!/bin/sh
	echo "Enabling autostart for Fadecandy Server"
	/etc/init.d/fcserver enable
	exit 0
endef

$(eval $(call BuildPackage,fcserver,+libpthread +librt +uclibcxx +libstdcpp))

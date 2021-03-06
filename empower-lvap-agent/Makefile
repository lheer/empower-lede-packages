#
# Copyright (C) 2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=empower-lvap-agent
PKG_VERSION:=20171113
PKG_RELEASE:=1
PKG_REV:=4dfe6421a1d7b784aaf9d185b8b6d91c56b331f0
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=https://github.com/lheer/empower-lvap-agent.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_SOURCE_PROTO:=git

include $(INCLUDE_DIR)/package.mk

define Package/empower-lvap-agent
	SECTION:=net
	CATEGORY:=Network
	TITLE:=The EmPOWER Agent
	MAINTAINER:=Roberto Riggio <roberto.riggio@create-net.org>
	DEPENDS:=+kmod-tun +libpcap +libstdcpp
	URL:=http://www.read.cs.ucla.edu/
endef

define Package/empower-lvap-agent/Description
	The EmPOWER Agent
endef

EXTRA_CFLAGS=-MD

CONFIGURE_ARGS += \
	--enable-tools=host \
	--enable-userlevel \
	--enable-wifi \
	--enable-empower \
	--disable-linuxmodule \
	--disable-dynamic-linking \
	--enable-empsocket \


define Build/Configure
  $(call Build/Configure/Default)
endef


define Package/empower-lvap-agent/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_DIR) $(1)/usr/share/click
	$(INSTALL_DIR) $(1)/etc/init.d/
	$(INSTALL_DIR) $(1)/etc/config/
	$(CP) ./files/empower.config $(1)/etc/config/empower
	$(INSTALL_BIN) ./files/empower.init $(1)/etc/init.d/empower
	$(INSTALL_BIN) ./files/empower_config.sh $(1)/usr/bin/empower_config.sh
	$(INSTALL_BIN) ./files/empower_add_ports.sh $(1)/usr/bin/empower_add_ports.sh
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/conf/wifi/write_handler $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/conf/wifi/read_handler $(1)/usr/bin/
	$(CP) $(PKG_BUILD_DIR)/userlevel/click $(1)/usr/bin/click
	$(CP) $(PKG_BUILD_DIR)/tools/click-align/click-align $(1)/usr/bin/click-align
endef

$(eval $(call BuildPackage,empower-lvap-agent))

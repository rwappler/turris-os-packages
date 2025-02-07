#
# Copyright (C) 2018-2022 CZ.NIC z.s.p.o. (https://www.nic.cz/)
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=turris-webapps
PKG_VERSION:=3.7.1
PKG_RELEASE:=$(AUTORELEASE)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://gitlab.nic.cz/turris/webapps
PKG_MIRROR_HASH:=67e355dd98edd09df77dfc7c2c41655e0d6b40e89c364ac861d108b2d6b287f6
PKG_SOURCE_VERSION:=v$(PKG_VERSION)

PKG_MAINTAINER:=CZ.NIC <packaging@turris.cz>
PKG_LICENSE:=GPL-3.0-or-later

include $(INCLUDE_DIR)/package.mk

define Package/turris-webapps
  SECTION:=web
  CATEGORY:=Web
  SUBMENU:=WebApps
  TITLE:=Turris WebApps
  DEPENDS:=+lighttpd +lighttpd-mod-alias +lighttpd-mod-cgi +lighttpd-mod-setenv
  URL:=https://gitlab.nic.cz/turris/webapps
endef

define Package/turris-webapps/description
 Common landding page for various installed WebApps.
endef

Build/Compile:=:

define Package/turris-webapps/install
	$(INSTALL_DIR) $(1)/etc/lighttpd/conf.d/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/turris-root.conf $(1)/etc/lighttpd/conf.d/90-turris-root.conf

	$(INSTALL_DIR) $(1)/usr/share/turris-webapps
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/turris-webapps-json-cgi $(1)/usr/share/turris-webapps
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/l10n.json $(1)/usr/share/turris-webapps

	$(INSTALL_DIR) $(1)/www/turris-webapps
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/favicon-*.png $(1)/www/turris-webapps
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/favicon.ico $(1)/www/turris-webapps
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/index.html $(1)/www/turris-webapps

	$(INSTALL_DIR) $(1)/www/turris-webapps/css
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/css/*.min.css $(1)/www/turris-webapps/css

	$(INSTALL_DIR) $(1)/www/turris-webapps/js
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/js/*.min.js $(1)/www/turris-webapps/js
	$(INSTALL_DIR) $(1)/www/webapps-icons
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/icons/turris-dark.svg $(1)/www/webapps-icons

endef

define Package/turris-webapps/postinst
#!/bin/sh
[ -n "$$IPKG_INSTROOT" ] || {
	/etc/init.d/lighttpd restart
}
endef

$(eval $(call BuildPackage,turris-webapps))

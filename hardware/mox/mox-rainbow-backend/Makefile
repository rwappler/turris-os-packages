#
## Copyright (C) 2022 CZ.NIC z.s.p.o. (http://www.nic.cz/)
#
## This is free software, licensed under the GNU General Public License v3.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mox-rainbow-backend
PKG_VERSION:=0.1.1
PKG_RELEASE:=$(AUTORELEASE)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://gitlab.nic.cz/turris/rainbow-ng.git
PKG_MIRROR_HASH:=83f86b7c52862f4fcada855b52f70834dbcf4fccab0885348e9a35a3404b8492
PKG_SOURCE_VERSION:=v$(PKG_VERSION)

PKG_MAINTAINER:=CZ.NIC <packaging@turris.cz>
PKG_LICENSE:=GPL-3.0-or-later
PKG_LICENSE_FILES:=COPYING

include $(INCLUDE_DIR)/package.mk

define Package/mox-rainbow-backend
  TITLE:=mox-rainbow-backend
  DEPENDS:=\
    @TARGET_mvebu_cortexa53_DEVICE_cznic_turris-mox \
    +kmod-ledtrig-activity \
    +rainbow-animator \
    +python3-uci
  PROVIDES:=rainbow-backend
endef

Build/Compile:=:

define Package/mox-rainbow-backend/install
	cd $(PKG_BUILD_DIR); make mox-install DESTDIR=$(1)
endef

$(eval $(call BuildPackage,mox-rainbow-backend))

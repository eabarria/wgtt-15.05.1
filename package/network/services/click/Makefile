#
# Copyright (C) 2019 Princeton University
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=click
PKG_VERSION:=20190619
PKG_RELEASE:=2.1
PKG_REV:=f988288748b9fdae137f2ffdb84000eb8254550d

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=git://github.com/sunnyszy/click.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_INSTALL:=1
# PKG_MD5SUM:=c3cba1c923d0a034cc518720b5ba7b40

include $(INCLUDE_DIR)/package.mk

define Package/click
	SECTION:=net
	CATEGORY:=Network
	TITLE:=Click Modular Router
	DEPENDS:=@BROKEN
	MENU:=1
	DEPENDS:= +libpcap +libstdcpp +libiwinfo
endef

TARGET_CPPFLAGS += -fno-rtti -faligned-new
TARGET_LDFLAGS += -liwinfo

define Build/Configure
	( cd $(PKG_BUILD_DIR) ; \
         $(TARGET_CONFIGURE_OPTS) \
         CPPFLAGS="-I$(STAGING_DIR)/usr/include -D__mips__" \
         LDFLAGS="-L$(STAGING_DIR)/usr/lib -liwinfo" \
         $(BUILDOPTS) \
	./configure \
	--target=$(GNU_TARGET_NAME)\
	--host=$(GNU_TARGET_NAME) \
	--build=$(GNU_HOST_NAME) \
	--disable-linuxmodule \
	--enable-userlevel \
	--enable-wifi \
	--disable-bsdmodule \
	--disable-app \
	--enable-aqm \
	--enable-ethernet \
	--enable-etherswitch \
	--enable-icmp \
	--enable-ip \
	--enable-ip6 \
	--enable-local \
	--enable-simple \
	--enable-standard \
	--enable-tcpudp \
	--enable-test \
	--disable-threads \
	--enable-grid \
	--enable-tools=host \
	--enable-dmalloc \
	--prefix=/usr ) ;
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR)
endef

define Package/click/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/tools/click-align/click-align $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/userlevel/click $(1)/usr/bin/
endef
$(eval $(call BuildPackage,click))


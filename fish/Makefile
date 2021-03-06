#
# Copyright (C) 2011-2017 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=fish
PKG_VERSION:=2.7.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://fishshell.com/files/$(PKG_VERSION)
PKG_HASH:=3a76b7cae92f9f88863c35c832d2427fb66082f98e92a02203dc900b8fa87bcb
PKG_INSTALL:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/fish
	SECTION:=utils
	CATEGORY:=Utilities
	SUBMENU:=Shells
	TITLE:=A smart and user-friendly command line shell
	DEPENDS:=+libncurses +libstdcpp +coreutils-whoami +PACKAGE_librt:librt
	URL:=https://fishshell.com
endef

define Package/fish/description
 Fish is a smart and user-friendly command line shell for OS X, Linux, and the rest of the family.
 Fish includes features like syntax highlighting, autosuggest-as-you-type, and fancy tab completions that just work,
 with no configuration required.
endef

CONFIGURE_VARS += ac_cv_file__proc_self_stat=yes
TARGET_CXXFLAGS += -std=c++0x
MAKE_FLAGS += EXTRA_CXXFLAGS="-I$(STAGING_DIR)/opt/include"

define Package/fish/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(CP) $(PKG_INSTALL_DIR)/opt/bin/* $(1)/opt/bin
	$(CP) ./files/apropos $(1)/opt/bin/
	$(INSTALL_DIR) $(1)/opt/etc/fish/conf.d
	$(CP) ./files/config.fish $(1)/opt/etc/fish/
	$(INSTALL_DIR) $(1)/opt/share/fish
	$(CP) $(PKG_INSTALL_DIR)/opt/share/fish/* $(1)/opt/share/fish/
	rm -rf $(1)/opt/share/fish/groff
	rm -rf $(1)/opt/share/fish/man
	rm -rf $(1)/opt/share/fish/tools
endef

$(eval $(call BuildPackage,fish))

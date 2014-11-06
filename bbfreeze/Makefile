#
# Copyright (C) 2006-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=bbfreeze
PKG_VERSION:=1.1.3
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).zip
PKG_SOURCE_URL:=http://pypi.python.org/packages/source/b/$(PKG_NAME)/
PKG_MD5SUM:=5c7bf32800376f1a1305176ad396feba
PKG_BUILD_DIR:=$(BUILD_DIR_HOST)/$(PKG_NAME)-$(PKG_VERSION)/
PKG_BUILD_DEPENDS:=python python-setuptools

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk
$(call include_mk, python-package.mk)

PYTHON:=$(HOST_PYTHON_BIN)

define Package/bbfreeze
  SUBMENU:=Python
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=bbfreeze
  URL:=http://pypi.python.org/pypi/bbfreeze
  DEPENDS:=+python
endef

define Package/bbfreeze/description
	create standalone executables from Python scripts
endef

define Build/Compile
	$(call Build/Compile/PyMod,., \
		install --prefix=/usr --root=$(PKG_INSTALL_DIR), \
		PYTHONPATH=$(PYTHON_LIB_DIR):$(STAGING_DIR_ROOT)/$(PYTHON_PKG_DIR); \
		)
endef

define Package/bbfreeze/install
	$(INSTALL_DIR) $(1)$(PYTHON_PKG_DIR)
	$(CP) \
	    $(PKG_INSTALL_DIR)$(PYTHON_PKG_DIR)/* \
	    $(1)$(PYTHON_PKG_DIR)/
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) \
	    $(PKG_INSTALL_DIR)/usr/bin/* \
	    $(1)/usr/bin/
	$(SED) '1s/#\!.*/#\!\/usr\/bin\/python/' $(1)/usr/bin/*
endef

$(eval $(call BuildPackage,bbfreeze))

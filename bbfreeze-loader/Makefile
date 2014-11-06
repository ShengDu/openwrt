#
# Copyright (C) 2006-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=bbfreeze-loader
PKG_VERSION:=1.1.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).zip
PKG_SOURCE_URL:=http://pypi.python.org/packages/source/b/$(PKG_NAME)/
PKG_MD5SUM:=33cc54a3e9485f082cbc49bb580469f9
PKG_BUILD_DIR:=$(BUILD_DIR_HOST)/$(PKG_NAME)-$(PKG_VERSION)/
PKG_BUILD_DEPENDS:=python python-setuptools

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk
$(call include_mk, python-package.mk)

PYTHON:=$(HOST_PYTHON_BIN)

define Package/bbfreeze-loader
  SUBMENU:=Python
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=bbfreeze-loader
  URL:=http://pypi.python.org/pypi/bbfreeze
  DEPENDS:=+python
endef

define Package/bbfreeze-loader/description
	provide binary loaders for bbfreeze
endef

define Build/Compile
	$(call Build/Compile/PyMod,., \
		install --prefix=/usr --root=$(PKG_INSTALL_DIR), \
		PYTHONPATH=$(PYTHON_LIB_DIR):$(STAGING_DIR_ROOT)/$(PYTHON_PKG_DIR); \
		)
endef

define Package/bbfreeze-loader/install
	$(INSTALL_DIR) $(1)$(PYTHON_PKG_DIR)
	$(CP) \
	    $(PKG_INSTALL_DIR)$(PYTHON_PKG_DIR)/* \
	    $(1)$(PYTHON_PKG_DIR)/
endef

$(eval $(call BuildPackage,bbfreeze-loader))

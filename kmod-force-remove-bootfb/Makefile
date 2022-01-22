#
# Copyright (C) 2006 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# $Id: Makefile 6565 2007-03-14 13:42:21Z nbd $

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=force-remove-bootfb
PKG_RELEASE:=$(AUTORELEASE)

PKG_LICENSE:=GPL-2.0

PKG_BUILD_DIR:=$(KERNEL_BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

define KernelPackage/force-remove-bootfb
  SUBMENU:=Other modules
  TITLE:=force remove bootfb
  VERSION:=$(LINUX_VERSION)-$(BOARD)-$(PKG_RELEASE)
  FILES:= $(PKG_BUILD_DIR)/force-remove-bootfb.$(LINUX_KMOD_SUFFIX)
endef

define KernelPackage/force-remove-bootfb/description
	Force remove bootfb for VFIO GPU Passthrough
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./src/* $(PKG_BUILD_DIR)
endef

MAKE_OPTS:= \
	ARCH="$(LINUX_KARCH)" \
	CROSS_COMPILE="$(TARGET_CROSS)" \
	M="$(PKG_BUILD_DIR)"

define Build/Compile
	$(MAKE) -C "$(LINUX_DIR)" \
		$(MAKE_OPTS) \
		CONFIG_FORCE_REMOVE_BOOTFB=m \
		modules
endef

define KernelPackage/force-remove-bootfb/install
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/etc/init.d/force-remove-bootfb $(1)/etc/init.d/
endef

$(eval $(call KernelPackage,force-remove-bootfb))
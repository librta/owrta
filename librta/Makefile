#
# Copyright (C) 2014 Robert W Smith (bsmith@linuxtoys.org)
#
# This program is distributed under the terms of the MIT License.
# See COPYING for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=librta
PKG_VERSION:=1.1.3.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/librta/librta/archive
PKG_MD5SUM:=70e655f06a2845a1f5ffe00f00020814

PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=COPYING

include $(INCLUDE_DIR)/package.mk

export GCC_HONOUR_COPTS=s

define Package/librta/Default
  SECTION:=libs
  CATEGORY:=Libraries
  URL:=http://www.librta.org
  MAINTAINER:=Frederic Roussel <fr.frasc@gmail.com>
endef

define Package/librta
$(call Package/librta/Default)
  TITLE:=Run-Time Access Library
endef

define Package/librta/description
 Library allowing to expose program internal data structures as database tables.
endef

define Package/librta-examples
$(call Package/librta/Default)
  TITLE:=Example programs for librta, pre-compiled.
  DEPENDS:=+libpq +librta
endef

define Package/librta-examples/description
 Library allowing to expose program internal data structures as database tables.
 Example programs, pre-compiled.
endef

define Build/Configure
endef

define Build/Compile
	echo; \
	echo "=====================" ; \
	echo BUILD_DIR: $(BUILD_DIR) ; \
	echo PKG_BUILD_DIR: $(PKG_BUILD_DIR) ; \
	echo TARGET_CC: $(TARGET_CC) ; \
	type $(TARGET_CC) ; \
	echo $(TARGET_CC_NOCACHE) ; \
	type $(TARGET_CC_NOCACHE) ; \
	echo CFLAGS: $(CFLAGS); \
	echo TARGET_CFLAGS: $(TARGET_CFLAGS); \
	echo TARGET_CPPFLAGS: $(TARGET_CPPFLAGS); \
	echo "=====================" ; \
	echo; \
	echo Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR)/src CC="$(TARGET_CC_NOCACHE)" CFLAGS="$(TARGET_CFLAGS) $(TARGET_CPPFLAGS) $(FPIC) -D_GNU_SOURCE"
	$(MAKE) -C $(PKG_BUILD_DIR)/test CC="$(TARGET_CC_NOCACHE)"
endef

define Build/InstallDev
	echo; \
	echo "=====================" ; \
	echo 1: $(1) ; \
	echo PKG_INSTALL_DIR: $(PKG_INSTALL_DIR) ; \
	echo "=====================" ; \
	echo; \
	echo Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/src/librta.h $(1)/usr/include/
	$(CP) $(PKG_BUILD_DIR)/src/librta*.a $(1)/usr/lib/
endef

define Package/librta/install
	echo; \
	echo "=====================" ; \
	echo $(INSTALL_DIR); \
	echo $(1); \
	echo "=====================" ; \
	echo; \
	echo Package/librta/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/src/librta.so* $(1)/usr/lib/
endef

define Package/librta-examples/install
	echo; \
	echo "=====================" ; \
	echo $(INSTALL_DIR); \
	echo $(1); \
	echo "=====================" ; \
	echo; \
	echo Package/librta-examples/install
	$(INSTALL_DIR) $(1)/usr/bin/librta
	$(CP) $(PKG_BUILD_DIR)/test/{app,app-static,librta_client} $(1)/usr/bin/librta
endef

$(eval $(call BuildPackage,librta))
$(eval $(call BuildPackage,librta-examples))


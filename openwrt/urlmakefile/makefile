#
# Copyright (C) 2017 - 2018 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=asterisk-chan-quectel
PKG_VERSION:=3.5
PKG_RELEASE:=3.5

PKG_SOURCE:=3.5.tar.gz
PKG_SOURCE_URL:=https://github.com/scjtqs2/asterisk-chan-quectel/archive/refs/tags/
PKG_HASH:=skip

PKG_FIXUP:=autoreconf

PKG_LICENSE:=GPL-2.0
PKG_LICENSE_FILES:=COPYRIGHT.txt LICENSE.txt
PKG_MAINTAINER:=Jiri Slachta <jiri@slachta.eu>


MODULES_DIR:=/usr/lib/asterisk/modules

include $(INCLUDE_DIR)/package.mk
# asterisk-chan-quectel needs iconv
include $(INCLUDE_DIR)/nls.mk

define Package/asterisk-chan-quectel/Default
  SUBMENU:=Telephony
  SECTION:=net
  CATEGORY:=Utilities
  URL:=https://github.com/scjtqs2/asterisk-chan-quectel
  DEPENDS:=$(ICONV_DEPENDS) +kmod-usb-acm +kmod-usb-serial +kmod-usb-serial-option +libusb-1.0 +usb-modeswitch +alsa-lib
  TITLE:=Asterisk Mobile Telephony Module
endef

define Package/asterisk16-chan-quectel
$(call Package/asterisk-chan-quectel/Default)
  DEPENDS+=asterisk16
  VARIANT:=asterisk16
endef

define Package/asterisk18-chan-quectel
$(call Package/asterisk-chan-quectel/Default)
  DEPENDS+=asterisk18
  VARIANT:=asterisk18
endef

define Package/asterisk20-chan-quectel
$(call Package/asterisk-chan-quectel/Default)
  DEPENDS+=asterisk20
  VARIANT:=asterisk20
endef

define Package/asterisk22-chan-quectel
$(call Package/asterisk-chan-quectel/Default)
  DEPENDS+=asterisk22
  VARIANT:=asterisk22
endef

define Package/asterisk23-chan-quectel
$(call Package/asterisk-chan-quectel/Default)
  DEPENDS+=asterisk23
  VARIANT:=asterisk23
endef

define Package/asterisk-chan-quectel
$(call Package/asterisk-chan-quectel/Default)
  DEPENDS+=asterisk
  VARIANT:=asterisk
endef

define Package/description/Default
 Asterisk channel driver for Mobile Telephony.
endef

Package/asterisk16-chan-quectel/description = $(Package/description/Default)
Package/asterisk18-chan-quectel/description = $(Package/description/Default)
Package/asterisk20-chan-quectel/description = $(Package/description/Default)
Package/asterisk22-chan-quectel/description = $(Package/description/Default)
Package/asterisk23-chan-quectel/description = $(Package/description/Default)
Package/asterisk-chan-quectel/description = $(Package/description/Default)

ifeq ($(BUILD_VARIANT),asterisk16)
  CHAN_quectel_AST_HEADERS:=$(STAGING_DIR)/usr/include/asterisk-16/include
  CONFIGURE_ARGS+= \
	  --with-astversion=16
endif

ifeq ($(BUILD_VARIANT),asterisk18)
  CHAN_quectel_AST_HEADERS:=$(STAGING_DIR)/usr/include/asterisk-18/include
  CONFIGURE_ARGS+= \
	  --with-astversion=18
endif

ifeq ($(BUILD_VARIANT),asterisk20)
  CHAN_quectel_AST_HEADERS:=$(STAGING_DIR)/usr/include/asterisk-20/include
  CONFIGURE_ARGS+= \
	  --with-astversion=20
endif

ifeq ($(BUILD_VARIANT),asterisk22)
  CHAN_quectel_AST_HEADERS:=$(STAGING_DIR)/usr/include/asterisk-22/include
  CONFIGURE_ARGS+= \
	  --with-astversion=22
endif

ifeq ($(BUILD_VARIANT),asterisk23)
  CHAN_quectel_AST_HEADERS:=$(STAGING_DIR)/usr/include/asterisk-23/include
  CONFIGURE_ARGS+= \
	  --with-astversion=23
endif

ifeq ($(BUILD_VARIANT),asterisk)
  CHAN_quectel_AST_HEADERS:=$(STAGING_DIR)/usr/include
  CONFIGURE_ARGS+= \
	  --with-astversion=22
endif


CONFIGURE_ARGS+= \
	--with-asterisk=$(CHAN_quectel_AST_HEADERS)

TARGET_CFLAGS+= \
	-I$(CHAN_quectel_AST_HEADERS)

MAKE_FLAGS+=LD="$(TARGET_CC)"

CONFIGURE_VARS += \
	DESTDIR="$(MODULES_DIR)" \
	ac_cv_type_size_t=yes \
	ac_cv_type_ssize_t=yes


define Package/conffiles/Default
/etc/asterisk/quectel.conf
endef

Package/asterisk16-chan-quectel/conffiles = $(Package/conffiles/Default)
Package/asterisk18-chan-quectel/conffiles = $(Package/conffiles/Default)
Package/asterisk20-chan-quectel/conffiles = $(Package/conffiles/Default)
Package/asterisk22-chan-quectel/conffiles = $(Package/conffiles/Default)
Package/asterisk23-chan-quectel/conffiles = $(Package/conffiles/Default)
Package/asterisk-chan-quectel/conffiles = $(Package/conffiles/Default)

define Package/Install/Default
	$(INSTALL_DIR) $(1)/etc/asterisk
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/etc/quectel.conf $(1)/etc/asterisk
	$(INSTALL_DIR) $(1)$(MODULES_DIR)
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/chan_quectel.so $(1)$(MODULES_DIR)
endef

Package/asterisk16-chan-quectel/install = $(Package/Install/Default)
Package/asterisk18-chan-quectel/install = $(Package/Install/Default)
Package/asterisk20-chan-quectel/install = $(Package/Install/Default)
Package/asterisk22-chan-quectel/install = $(Package/Install/Default)
Package/asterisk23-chan-quectel/install = $(Package/Install/Default)
Package/asterisk-chan-quectel/install = $(Package/Install/Default)

$(eval $(call BuildPackage,asterisk16-chan-quectel))
$(eval $(call BuildPackage,asterisk18-chan-quectel))
$(eval $(call BuildPackage,asterisk20-chan-quectel))
$(eval $(call BuildPackage,asterisk22-chan-quectel))
$(eval $(call BuildPackage,asterisk23-chan-quectel))
$(eval $(call BuildPackage,asterisk-chan-quectel))

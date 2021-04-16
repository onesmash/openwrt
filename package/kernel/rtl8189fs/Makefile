include $(TOPDIR)/rules.mk

PKG_NAME:=rtl8189fs
PKG_RELEASE=1

PKG_LICENSE:=GPLv2
PKG_LICENSE_FILES:=

PKG_SOURCE_URL:=https://github.com/jwrdegoede/rtl8189ES_linux.git
PKG_MIRROR_HASH:=a1784105b382356540ed32fb853901368ddc252df56b51f7f9bbb53e9b275be1
PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2021-04-12
PKG_SOURCE_VERSION:=62c31d577c385316bb99107f60e63169dacc37db

PKG_MAINTAINER:=onesmash <good122000@qq.com>
PKG_BUILD_PARALLEL:=1

STAMP_CONFIGURED_DEPENDS := $(STAGING_DIR)/usr/include/mac80211-backport/backport/autoconf.h

include $(INCLUDE_DIR)/kernel.mk
include $(INCLUDE_DIR)/package.mk

define KernelPackage/rtl8189fs
  SUBMENU:=Wireless Drivers
  TITLE:=Realtek RTL8189FTV SDIO WiFi
	DEPENDS:=+kmod-mac80211 +kmod-cfg80211 +kmod-mmc +@DRIVER_11N_SUPPORT 
  FILES:=$(PKG_BUILD_DIR)/8189fs.ko
  AUTOLOAD:=$(call AutoLoad,50,mac80211 cfg80211 8189fs)
endef

NOSTDINC_FLAGS := \
	$(KERNEL_NOSTDINC_FLAGS)

define Build/Compile
	+$(MAKE) $(PKG_JOBS) -C $(LINUX_DIR) \
		$(KERNEL_MAKE_FLAGS) \
		M="$(PKG_BUILD_DIR)" \
		CONFIG_RTL8189FS=m \
		NOSTDINC_FLAGS="$(NOSTDINC_FLAGS)" \
		modules
endef

$(eval $(call KernelPackage,rtl8189fs))

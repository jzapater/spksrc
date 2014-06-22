PKG_NAME = domoticz
PKG_VERS = $(PKG_SVN_REV)
PKG_EXT = tar.gz
PKG_DOWNLOAD_METHOD = svn
PKG_SVN_REV = 1801
PKG_DIST_NAME = domoticz
PKG_DIST_SITE = svn://svn.code.sf.net/p/domoticz/code
PKG_DIST_FILE = $(PKG_NAME)-r$(PKG_SVN_REV).$(PKG_EXT)
PKG_DIR = $(PKG_NAME)-r*

DEPENDS = cross/boost cross/sqlite cross/curl

HOMEPAGE = http://www.domoticz.com/
COMMENT  = Domoticz is a Home Automation System
LICENSE  = 

CONFIGURE_TARGET = myConfigure
INSTALL_TARGET = myInstall

BOOST_LIBRARIES = system thread date_time
ENV += BOOST_LIBRARIES="$(BOOST_LIBRARIES)" CMAKE_INCLUDE_PATH="$(STAGING_INSTALL_PREFIX)/include" CMAKE_LIBRARY_PATH="$(STAGING_INSTALL_PREFIX)/lib" PCH_COMPILE_FLAGS="$(CFLAGS)"

include ../../mk/spksrc.cross-cc.mk

.PHONY: myConfigure
myConfigure:
	$(RUN) cmake CMakeLists.txt

.PHONY: myInstall
myInstall:
	mkdir -p $(STAGING_INSTALL_PREFIX)
	install -m 755 $(WORK_DIR)/$(PKG_DIR)/domoticz $(STAGING_INSTALL_PREFIX)/
	install -m 644  $(WORK_DIR)/$(PKG_DIR)/svnversion.h $(STAGING_INSTALL_PREFIX)/
	mkdir -p $(STAGING_INSTALL_PREFIX)/www
	tar -cf - -C $(WORK_DIR)/$(PKG_DIR)/www . | tar -xf - -C $(STAGING_INSTALL_PREFIX)/www
	mkdir -p $(STAGING_INSTALL_PREFIX)/scripts
	tar -cf - -C $(WORK_DIR)/$(PKG_DIR)/scripts . | tar -xf - -C $(STAGING_INSTALL_PREFIX)/scripts

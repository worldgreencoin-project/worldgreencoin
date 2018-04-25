include $(top_srcdir)/src/Makefile.include

AM_CPPFLAGS += -I$(top_srcdir)/src \
  -I$(top_srcdir)/src/qt \
  -I$(top_builddir)/src/qt \
  $(PROTOBUF_CFLAGS) \
    $(QR_CFLAGS)
bin_PROGRAMS = test_worldgreencoin-qt
TESTS = test_worldgreencoin-qt

TEST_QT_MOC_CPP = moc_uritests.cpp

if ENABLE_WALLET
TEST_QT_MOC_CPP += moc_paymentservertests.cpp
endif

TEST_QT_H = \
  uritests.h \
  paymentrequestdata.h \
  paymentservertests.h

BUILT_SOURCES = $(TEST_QT_MOC_CPP)

test_worldgreencoin_qt_CPPFLAGS = $(AM_CPPFLAGS) $(QT_INCLUDES) $(QT_TEST_INCLUDES)

test_worldgreencoin_qt_SOURCES = \
  test_main.cpp \
  uritests.cpp \
  $(TEST_QT_H)
if ENABLE_WALLET
test_worldgreencoin_qt_SOURCES += \
  paymentservertests.cpp
endif

nodist_test_worldgreencoin_qt_SOURCES = $(TEST_QT_MOC_CPP)

test_worldgreencoin_qt_LDADD = $(LIBBITCOINQT)
if ENABLE_WALLET
test_worldgreencoin_qt_LDADD += $(LIBBITCOIN_WALLET) $(LIBBITCOIN_SERVER_WALLET)
endif
test_worldgreencoin_qt_LDADD += $(LIBBITCOIN_SERVER)
if ENABLE_WALLET
test_worldgreencoin_qt_LDADD += $(LIBBITCOIN_SERVER_WALLET)
endif
test_worldgreencoin_qt_LDADD += $(LIBBITCOIN_CLI) $(LIBBITCOIN_COMMON) ${RPCWALLET} $(LIBLEVELDB) \
  $(LIBMEMENV) $(BOOST_LIBS) $(QT_DBUS_LIBS) $(QT_TEST_LIBS) $(QT_LIBS) \
  $(QR_LIBS) $(PROTOBUF_LIBS) $(BDB_LIBS)
test_worldgreencoin_qt_LDFLAGS = $(QT_LDFLAGS)

CLEANFILES = $(BUILT_SOURCES) *.gcda *.gcno

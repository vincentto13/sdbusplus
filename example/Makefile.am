noinst_PROGRAMS = list-users

list_users_SOURCES = list-users.cpp
list_users_CXXFLAGS = $(SYSTEMD_CFLAGS) -I$(top_srcdir)
list_users_LDADD = $(SYSTEMD_LIBS) ../libsdbusplus.la

if BOOST
noinst_PROGRAMS += asio-example
asio_example_SOURCES = asio-example.cpp
asio_example_CXXFLAGS = \
    $(SYSTEMD_CFLAGS) \
    $(PTHREAD_CFLAGS) \
    $(BOOST_CPPFLAGS) \
    -DBOOST_ALL_NO_LIB \
    -DBOOST_SYSTEM_NO_DEPRECATED \
    -DBOOST_ERROR_CODE_HEADER_ONLY \
    -DBOOST_COROUTINES_NO_DEPRECATION_WARNING \
    -I$(top_srcdir)

asio_example_LDADD = \
    $(SYSTEMD_LIBS) \
    $(PTHREAD_LIBS) \
    -lboost_coroutine \
    ../libsdbusplus.la

asio_example_LDFLAGS = \
    $(BOOST_LDFLAGS)
endif

if WANT_SDBUSPP
noinst_PROGRAMS += calculator-server
calculator_server_generated_files = \
	net/poettering/Calculator/server.hpp \
	net/poettering/Calculator/server.cpp \
	net/poettering/Calculator/error.hpp \
	net/poettering/Calculator/error.cpp \
	net/poettering/Calculator/client.hpp

calculator_markdown_generated_files = \
	calculator.md

calculator_server_SOURCES = \
	calculator-server.cpp $(calculator_server_generated_files)
calculator_server_CXXFLAGS = $(SYSTEMD_CFLAGS) -I$(top_srcdir)
calculator_server_LDADD = $(SYSTEMD_LIBS) ../libsdbusplus.la

BUILT_SOURCES = \
	$(calculator_server_generated_files) \
	$(calculator_markdown_generated_files)
CLEANFILES = \
	$(calculator_server_generated_files) \
	$(calculator_markdown_generated_files)

net/poettering/Calculator/server.hpp:
	@mkdir -p $(@D)
	@top_srcdir@/tools/sdbus++ \
	    -r $(srcdir) -t $(top_builddir)/tools/sdbusplus/templates \
	    interface server-header net.poettering.Calculator > $@

net/poettering/Calculator/server.cpp:
	@mkdir -p $(@D)
	@top_srcdir@/tools/sdbus++ \
	    -r $(srcdir) -t $(top_builddir)/tools/sdbusplus/templates \
	    interface server-cpp net.poettering.Calculator > $@

net/poettering/Calculator/error.hpp:
	@mkdir -p $(@D)
	@top_srcdir@/tools/sdbus++ \
	    -r $(srcdir) -t $(top_builddir)/tools/sdbusplus/templates \
	    error exception-header net.poettering.Calculator > $@

net/poettering/Calculator/error.cpp:
	@mkdir -p $(@D)
	@top_srcdir@/tools/sdbus++ \
	    -r $(srcdir) -t $(top_builddir)/tools/sdbusplus/templates \
	    error exception-cpp net.poettering.Calculator > $@

calculator.md:
	@mkdir -p $(@D)
	@top_srcdir@/tools/sdbus++ \
	    -r $(srcdir) -t $(top_builddir)/tools/sdbusplus/templates \
	    interface markdown net.poettering.Calculator > $@
	@top_srcdir@/tools/sdbus++ \
	    -r $(srcdir) -t $(top_builddir)/tools/sdbusplus/templates \
	    error markdown net.poettering.Calculator >> $@

net/poettering/Calculator/client.hpp:
	@mkdir -p $(@D)
	@top_srcdir@/tools/sdbus++ \
	    -r $(srcdir) -t $(top_builddir)/tools/sdbusplus/templates \
	    interface client-header net.poettering.Calculator > $@
endif

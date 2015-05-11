include ../../config.mk

ifneq ($(UNAME),SunOS)
	LIB_LDFLAGS:=$(LDFLAGS) -Wl,-soname,libmosquittopp.so
endif

.PHONY : clean install

all : libmosquittopp.so

install : all
	$(INSTALL) -d ${DESTDIR}$(prefix)/lib${LIB_SUFFIX}/
	$(INSTALL) -s --strip-program=${CROSS_COMPILE}${STRIP} libmosquittopp.so ${DESTDIR}${prefix}/lib${LIB_SUFFIX}/libmosquittopp.so
	$(INSTALL) -d ${DESTDIR}${prefix}/include/
	$(INSTALL) mosquittopp.h ${DESTDIR}${prefix}/include/mosquittopp.h
	
uninstall :
	-rm -f ${DESTDIR}${prefix}/lib${LIB_SUFFIX}/libmosquittopp.so
	-rm -f ${DESTDIR}${prefix}/include/mosquittopp.h

clean :
	-rm -f *.o libmosquittopp.so

libmosquittopp.so : mosquittopp.o
	${CROSS_COMPILE}$(CXX) -shared $(LIB_LDFLAGS) $< -o $@ ../libmosquitto.so

mosquittopp.o : mosquittopp.cpp mosquittopp.h
	${CROSS_COMPILE}$(CXX) $(LIB_CXXFLAGS) -c $< -o $@


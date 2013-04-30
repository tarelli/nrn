
CYTHON = @CYTHON@
PYTHON = @PYTHON@
geosrc = $(top_srcdir)/share/lib/python/neuron/rxd/geometry3d

all: graphicsPrimitives.cpp surfaces.cpp ctng.cpp

ctng.cpp: ctng.pyx
	$(CYTHON) $(geosrc)/ctng.pyx -o ctng.cpp

surfaces.cpp: surfaces.pyx marching_cubes2.c llgramarea.c
	$(CYTHON) $(geosrc)/surfaces.pyx -o surfaces.cpp


graphicsPrimitives.cpp: graphicsPrimitives.pyx
	$(CYTHON) $(geosrc)/graphicsPrimitives.pyx -o graphicsPrimitives.cpp

pkginclude_HEADERS = 
EXTRA_DIST = ctng.cpp ctng.pyx surfaces.cpp surfaces.pyx \
	graphicsPrimitives.cpp graphicsPrimitives.pyx \
	marching_cubes2.c llgramarea.c

install-exec-am: ctng.cpp surfaces.cpp graphicsPrimitives.cpp
	if test ! -f graphicsPrimitives.cpp ; then \
		cp $(geosrc)/graphicsPrimitives.cpp  . ; \
	fi
	if test ! -f ctng.cpp ; then \
		cp $(geosrc)/ctng.cpp  . ; \
	fi
	if test ! -f surfaces.cpp ; then \
		cp $(geosrc)/surfaces.cpp  . ; \
	fi	
	$(PYTHON) setup.py build_ext --inplace

clean-generic:
	rm -r -f build
	if test "$(CYTHON)" != "echo" ; then \
		rm -f ctng.cpp graphicsPrimitives.cpp surfaces.cpp ; \
		rm -fr build/ ; \
	fi
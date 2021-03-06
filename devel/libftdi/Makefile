# $FreeBSD$

PORTNAME=	libftdi
PORTVERSION=	0.20
PORTREVISION=	4
CATEGORIES=	devel
MASTER_SITES=	http://www.intra2net.com/en/developer/libftdi/download/

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Library (using libusb) to talk to FTDI chips

LICENSE=	GPLv2 LGPL21
LICENSE_COMB=	multi
LICENSE_FILE_GPLv2=	${WRKSRC}/COPYING.GPL
LICENSE_FILE_LGPL21=	${WRKSRC}/COPYING.LIB

USES=		cmake pkgconfig
CMAKE_ARGS=	-DDOCUMENTATION:BOOL=OFF -DEXAMPLES:BOOL=OFF
USE_LDCONFIG=	yes

OPTIONS_DEFINE=	BOOST PYTHON
OPTIONS_DEFAULT=BOOST PYTHON
OPTIONS_SUB=	yes

BOOST_DESC=		C++ bindings (requires Boost)
BOOST_LIB_DEPENDS=	libboost_system.so:devel/boost-libs
BOOST_CMAKE_ON=		-DFTDIPP:BOOL=ON
BOOST_CMAKE_OFF=	-DFTDIPP:BOOL=OFF
BOOST_CXXFLAGS=		-I${LOCALBASE}/include

PYTHON_DESC=		Python bindings
PYTHON_BUILD_DEPENDS=	swig2.0:devel/swig20
PYTHON_CMAKE_ON=	-DPYTHON_BINDINGS:BOOL=ON
PYTHON_CMAKE_OFF=	-DPYTHON_BINDINGS:BOOL=OFF
PYTHON_USES=		python

.include <bsd.port.options.mk>

post-patch:
	@${REINPLACE_CMD} \
		-e '/includedir/s|/$${PROJECT_NAME}||' \
		-e '/SET.*LIB_SUFFIX/s/64/""/' \
		-e 's|lib$${LIB_SUFFIX}/pkgconfig|libdata/pkgconfig|' \
		${WRKSRC}/CMakeLists.txt
	@${REINPLACE_CMD} 's|SITEPACKAGE.*ABSOLUTE|SITEPACKAGE ${PYTHON_SITELIBDIR} ABSOLUTE|' \
		${WRKSRC}/bindings/CMakeLists.txt

post-install:
.if ${PORT_OPTIONS:MPYTHON}
	${PYTHON_CMD} -m compileall -d ${PYTHON_SITELIBDIR} ${STAGEDIR}${PYTHON_SITELIBDIR}
	${PYTHON_CMD} -O -m compileall -d ${PYTHON_SITELIBDIR} ${STAGEDIR}${PYTHON_SITELIBDIR}
	${STRIP_CMD} ${STAGEDIR}${PYTHON_SITELIBDIR}/_ftdi.so
.endif

.include <bsd.port.mk>

# $FreeBSD$

PORTNAME=	waifu2x-converter-cpp
DISTVERSION=	1.0.0-377
DISTVERSIONSUFFIX=	-g007e7b1
CATEGORIES=	graphics
MASTER_SITES=	https://aur.archlinux.org/cgit/aur.git/plain/:manpage
DISTFILES=	${DISTNAME}${EXTRACT_SUFX} \
		${PORTNAME:C/-.*//}.1.gz?h=${PORTNAME:C/-.*//}-git\&id=5c150a5:manpage
EXTRACT_ONLY=	${DISTFILES:N*\:manpage:C/:.*//}

MAINTAINER=	jbeich@FreeBSD.org
COMMENT=	Scale and denoise images using convolutional neural networks

LICENSE=	BSD2CLAUSE MIT
LICENSE_COMB=	multi
LICENSE_FILE_BSD2CLAUSE=${WRKSRC}/LICENSE
LICENSE_FILE_MIT=	${WRKSRC}/LICENSE

BUILD_DEPENDS=	${LOCALBASE}/include/CL/opencl.h:${PORTSDIR}/devel/opencl
LIB_DEPENDS=	libopencv_highgui.so:${PORTSDIR}/graphics/opencv \
		libopencv_imgproc.so:${PORTSDIR}/graphics/opencv-core

USE_GITHUB=	yes
GH_ACCOUNT=	tanakamura

USES=		cmake compiler:c++11-lib dos2unix
DOS2UNIX_GLOB=	*.cpp *.hpp
CMAKE_ARGS=	-DOPENCV_PREFIX="${LOCALBASE}" \
		-DOpenCL_LIBRARY="${LOCALBASE}/lib/libOpenCL.so" \
		-DINSTALL_MODELS=on
CFLAGS+=	-D_GLIBCXX_USE_C99 -D_GLIBCXX_USE_C99_MATH_TR1 \
		-D_DECLARE_C99_LDBL_MATH # XXX ports/193528
LDFLAGS+=	-Wl,--as-needed # avoid overlinking (opencv deps)
TEST_TARGET=	test ARGS="-V"
USE_LDCONFIG=	yes
PLIST_FILES=	bin/${PORTNAME} \
		man/man1/${PORTNAME}.1.gz \
		include/w2xconv.h \
		lib/libw2xc.so
PORTDATA=	*
PORTDOCS=	*

OPTIONS_DEFINE=	DOCS SIMD
OPTIONS_DEFAULT=SIMD

DOCS_CMAKE_ON=	-DINSTALL_DOCS=on
SIMD_CMAKE_OFF=	-DARMOPT=off -DX86OPT=off

post-extract:
	@${GZCAT} ${_DISTDIR}/${DISTFILES:M*\:manpage:C/:.*//} \
		>${WRKDIR}/${PORTNAME}.1

post-patch:
	@${REINPLACE_CMD} -e 's,-O2,,; /SYMBOL/s,-s,,' \
		${WRKSRC}/CMakeLists.txt
	@${REINPLACE_CMD} \
		-e '/CmdLine/s,[^"]*"),${DISTVERSIONFULL}"),' \
		${WRKSRC}/src/main.cpp
# Undo AUR rename and use version from |git describe --tags|
	@${REINPLACE_CMD} -e '/AUTHORS/,$$! { /\.B mai/! \
			s,${PORTNAME:C/-.*//},${PORTNAME},; }' \
		-e '1s,\(version\) [^"]*,\1 ${DISTVERSIONFULL},' \
		${WRKDIR}/${PORTNAME}.1

post-install:
	${INSTALL_MAN} ${WRKDIR}/${PORTNAME}.1 \
		${STAGEDIR}${MAN1PREFIX}/man/man1

.include <bsd.port.mk>

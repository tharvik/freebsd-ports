# Created by: FreeBSD GNOME Team <gnome@freebsd.org>
# $FreeBSD$

PORTNAME=	appstream-glib
PORTVERSION=	0.4.1
CATEGORIES=	devel
MASTER_SITES=	http://people.freedesktop.org/~hughsient/appstream-glib/releases/
DIST_SUBDIR=	gnome3

MAINTAINER=	gnome@FreeBSD.org
COMMENT=	Library to help with AppStream metadata

LICENSE=	LGPL21
LICENSE_FILE=	${WRKSRC}/COPYING

BUILD_DEPENDS=	gtkdoc-check:${PORTSDIR}/textproc/gtk-doc \
		gcab:${PORTSDIR}/archivers/gcab
LIB_DEPENDS=	libsoup-2.4.so:${PORTSDIR}/devel/libsoup \
		libyaml.so:${PORTSDIR}/textproc/libyaml \
		libfontconfig.so:${PORTSDIR}/x11-fonts/fontconfig \
		libfreetype.so:${PORTSDIR}/print/freetype2
RUN_DEPENDS=	gcab:${PORTSDIR}/archivers/gcab

USES=		gettext gperf gmake libtool pathfix pkgconfig tar:xz
USE_GNOME=	gdkpixbuf2 glib20 gtk30 intlhack introspection:build \
		libxml2:build pango
USE_LDCONFIG=	yes
GNU_CONFIGURE=	yes
USE_SQLITE=	3
CPPFLAGS+=	-I${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib
CONFIGURE_ARGS=	--with-xml-catalog=${LOCALBASE}/share/xml/catalog \
		--disable-rpm \
		--disable-ostree
INSTALL_TARGET=	install-strip

OPTIONS_DEFINE=	MANPAGES
OPTIONS_DEFAULT=MANPAGES
OPTIONS_SUB=	yes
MANPAGES_CONFIGURE_ENABLE=	man
MANPAGE_BUILD_DEPENDS=	docbook-xml>=0:${PORTSDIR}/textproc/docbook-xml \
		docbook-xsl>=0:${PORTSDIR}/textproc/docbook-xsl
MANPAGES_USE=	GNOME=libxslt:build

.include <bsd.port.options.mk>

.if !exists(/usr/libdata/pkgconfig/libarchive.pc)
LIB_DEPENDS+=	libarchive.so.13:${PORTSDIR}/archivers/libarchive
.endif

.if ${OSVERSION} < 1000000 && ${OPSYS} == FreeBSD
post-patch:
	${REINPLACE_CMD} -e 's|-Wtype-limits||g' \
		${WRKSRC}/configure
.endif

.include <bsd.port.mk>

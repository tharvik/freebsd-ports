# Created by: Kai Wang <kaiw27@gmail.com>
# $FreeBSD$

PORTNAME=	fish
PORTVERSION=	2.1.1
PORTREVISION=	4
CATEGORIES=	shells
MASTER_SITES=	http://fishshell.com/files/${PORTVERSION}/

MAINTAINER=	freebsd.users@gmail.com
COMMENT=	User friendly command line shell

LICENSE=	GPLv2

USES=		autoreconf cpe gmake iconv
GNU_CONFIGURE=	yes

CPE_VENDOR=	fishshell

CPPFLAGS+=	-I${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib -pthread ${ICONV_LIB}

PORTDOCS=	*
MANDIRS=	${DATADIR}/man/man1

OPTIONS_DEFINE=	DOCS NLS
OPTIONS_SUB=	yes

NLS_USES=		gettext
NLS_CONFIGURE_ENV=	ac_cv_func_gettext=yes
NLS_CONFIGURE_OFF=	--without-gettext

DOCS_EXTRA_PATCHES_OFF=	${FILESDIR}/extra-patch-Makefile.in

post-patch:
	@${REINPLACE_CMD} -e \
		'/^all:/s|user_doc|| ; \
		 s| "$$(HAVE_GETTEXT)" = 1| x$$(HAVE_GETTEXT) = x1| ; \
		 s| $$(HAVE_GETTEXT) = 1| x$$(HAVE_GETTEXT) = x1| ; \
		 s|$$(DESTDIR)$$(bindir)/fish|$$(bindir)/fish|g' \
		 ${WRKSRC}/Makefile.in
	@${REINPLACE_CMD} -e \
		's|-rdynamic|-Wl,--export-dynamic| ; \
		 /pthread_create/d ; \
		 s|ncurses curses|curses| ; \
		 s|ncurses.h||' ${WRKSRC}/configure.ac

post-install:
.for i in fish fish_indent fish_pager fishd mimedb
	@${STRIP_CMD} ${STAGEDIR}${PREFIX}/bin/${i}
.endfor

.include <bsd.port.mk>

# Created by: kbyanc
# $FreeBSD$

PORTNAME=	mmencode
PORTVERSION=	2.7
CATEGORIES=	converters
MASTER_SITES=	ftp://ftp.delegate.org/pub/mime/mm2.7/ \
		ftp://ftp.funet.fi/pub/unix/mail/metamail/
DISTNAME=	mm${PORTVERSION}
EXTRACT_SUFX=	.tar.Z

MAINTAINER=	johans@FreeBSD.org
COMMENT=	Translate to and from mail-oriented encoding formats

WRKSRC=		${WRKDIR}/${DISTNAME}/src/metamail

PLIST_FILES=	bin/mmencode bin/mimencode \
		man/man1/mmencode.1.gz man/man1/mimencode.1.gz

ALL_TARGET=	mmencode
MAKE_ARGS=	CFLAGS="${CFLAGS}"

do-install:
	@${INSTALL_PROGRAM} ${WRKSRC}/mmencode ${STAGEDIR}${PREFIX}/bin
	@${INSTALL_MAN} ${WRKSRC}/../man/mmencode.1 \
		${STAGEDIR}${MAN1PREFIX}/man/man1/
	@cd ${STAGEDIR}${MAN1PREFIX}/man/man1 && ${LN} -s mmencode.1 mimencode.1
	@cd ${STAGEDIR}${PREFIX}/bin && ${LN} -s mmencode mimencode

.include <bsd.port.mk>

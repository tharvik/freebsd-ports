# Created by: Jason Bacon <jwbacon@tds.net>
# $FreeBSD$

PORTNAME=	FastTree
PORTVERSION=	2.1.8
CATEGORIES=	biology
MASTER_SITES=	http://www.microbesonline.org/fasttree/
EXTRACT_SUFX=	.c

MAINTAINER=	jwbacon@tds.net
COMMENT=	Approximately-maximum-likelihood phylogenetic trees from alignments

# LICENSE=	unspecified open source

USES=		compiler:openmp

CFLAGS+=	-DOPENMP -fopenmp -O3 -finline-functions -funroll-loops
LDFLAGS+=	-lm

PLIST_FILES=	bin/FastTree

do-extract:
	${MKDIR} ${WRKSRC}
	${CP} ${DISTDIR}/${DISTFILES} ${WRKSRC}

do-build:
	cd ${WRKSRC} && ${CC} ${CFLAGS} -o FastTree ${DISTFILES} ${LDFLAGS}

do-install:
	${MKDIR} ${STAGEDIR}${PREFIX}/bin
	${INSTALL_PROGRAM} ${WRKSRC}/FastTree ${STAGEDIR}${PREFIX}/bin

.include <bsd.port.mk>

# Created by: fernan@iib.unsam.edu.ar
# $FreeBSD$

PORTNAME=	nmzmail
PORTVERSION=	0.1.3
PORTREVISION=	4
CATEGORIES=	mail
MASTER_SITES=	http://www.ecademix.com/JohannesHofmann/

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Fast mail searching for mutt

RUN_DEPENDS=	namazu:${PORTSDIR}/databases/namazu2

GNU_CONFIGURE=	yes
USES=		gmake readline

PLIST_FILES=	bin/nmzmail
PORTDOCS=	README NEWS

OPTIONS_DEFINE=	DOCS

pre-extract:
.if !defined(MAX_MAIL_DIRS)
	@ ${ECHO_MSG} "You can define MAX_MAIL_DIRS=n."
	@ ${ECHO_MSG} "nmzmail will only process this many mailboxes, the default is 32."
.endif

post-extract:
.if defined(MAX_MAIL_DIRS)
	@ ${SED} -i.bak -e 's/MAX_MAIL_DIRS 32/MAX_MAIL_DIRS ${MAX_MAIL_DIRS}/' \
	${WRKSRC}/src/nmzmail.c
.endif

post-install:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${PORTDOCS:S|^|${WRKSRC}/|} ${STAGEDIR}${DOCSDIR}

.include <bsd.port.mk>

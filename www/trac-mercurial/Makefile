# $FreeBSD$

PORTNAME=	mercurial
PORTVERSION=	1.0.0.3
CATEGORIES=	www devel python
MASTER_SITES=	LOCAL/rm
PKGNAMEPREFIX=	trac-
DISTNAME=	${PORTNAME}plugin-${PORTVERSION}
DIST_SUBDIR=	trac

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Plugin to use Mercurial instead of Subversion in Trac

LICENSE=	GPLv2

RUN_DEPENDS=	hg:${PORTSDIR}/devel/mercurial \
		tracd:${PORTSDIR}/www/trac

USES=		python:2
USE_PYTHON=	distutils autoplist

.include <bsd.port.mk>

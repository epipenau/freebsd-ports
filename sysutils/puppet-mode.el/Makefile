# Created by: Dmitry Sivachenko <demon@FreeBSD.org>
# $FreeBSD$

PORTNAME=	puppet-mode.el
PORTVERSION=	0.2
PORTREVISION=	2
CATEGORIES=	sysutils elisp

MAINTAINER=	demon@FreeBSD.org
COMMENT=	Simple mode for editing puppet manifests

USE_GITHUB=	yes
GH_PROJECT=	puppet-syntax-emacs
GH_ACCOUNT=	puppetlabs
GH_TAGNAME=	be5d708

NO_BUILD=	yes
USE_EMACS=	yes

PLIST_FILES=	%%EMACS_SITE_LISPDIR%%/puppet-mode.el

do-install:
	${INSTALL_DATA} ${WRKSRC}/puppet-mode.el ${STAGEDIR}${PREFIX}/${EMACS_SITE_LISPDIR}

.include <bsd.port.mk>

# Created by: Matthew Donovan <kitchetech@gmail.com>
# $FreeBSD$

PORTNAME=	sterm-custom
DISTVERSION=	0.8.2
CATEGORIES=	x11

MAINTAINER=	hukadan@protonmail.com
COMMENT=	Simple X terminal

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/LICENSE

LIB_DEPENDS=	libfontconfig.so:x11-fonts/fontconfig \
		libfreetype.so:print/freetype2

USES=		pkgconfig
USE_XORG=	x11 xext xft
USE_GITHUB=     yes
GH_ACCOUNT=     hukadan
GH_PROJECT=     st
GH_TAGNAME=     cf31822010ac2429c6b93da20ca1886212101a07

PLIST_FILES=	bin/st man/man1/st.1.gz

# This way we avoid running tic on st.info which does not work as expected.
BINARY_ALIAS=	tic=true

PORTDATA=	config.def.h st.info
PORTDOCS=	FAQ LEGACY README TODO

OPTIONS_DEFINE=	DOCS

post-install:
	@${STRIP_CMD} ${STAGEDIR}${PREFIX}/bin/st
	@${MKDIR} ${STAGEDIR}${DATADIR}
	cd ${WRKSRC} && ${INSTALL_DATA} ${PORTDATA} ${STAGEDIR}${DATADIR}

post-install-DOCS-on:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	cd ${WRKSRC} && ${INSTALL_DATA} ${PORTDOCS} ${STAGEDIR}${DOCSDIR}

.include <bsd.port.mk>

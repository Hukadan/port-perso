# Created by: Jeroen Schot <schot@a-eskwadraat.nl>
# $FreeBSD$

PORTNAME=	dwm-custom
DISTVERSION=	6.2
CATEGORIES=	x11-wm
PORTREVISION=   2

MAINTAINER=	hukadan@protonmail.com
COMMENT=	Dynamic, small, fast and simple window manager

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/LICENSE

LIB_DEPENDS=	libfontconfig.so:x11-fonts/fontconfig
# Kyua is not used by the upstream to test. It's only used in the port's
# do-test target.
TEST_DEPENDS=	${LOCALBASE}/libexec/atf-check:devel/kyua

USE_XORG=	x11 xft
USE_GITHUB=     yes
GH_ACCOUNT=     hukadan
GH_PROJECT=     dwm
GH_TAGNAME=     8a38d7e9ff83466f439041b6d4ddc67c069fdf81

MAKE_ARGS=	CC="${CC}" \
		FREETYPEINC="${LOCALBASE}/include/freetype2" \
		MANPREFIX="${MANPREFIX}/man" \
		PREFIX="${PREFIX}" \
		VERSION="${PORTVERSION}" \
		X11INC="${LOCALBASE}/include" \
		X11LIB="${LOCALBASE}/lib"

PLIST_FILES=	bin/dwm \
		man/man1/dwm.1.gz

OPTIONS_DEFINE=	XINERAMA
OPTIONS_DEFAULT=XINERAMA

XINERAMA_USE=	XORG=xinerama
XINERAMA_MAKE_ARGS_OFF=	XINERAMAFLAGS= XINERAMALIBS=


post-configure:
	@${REINPLACE_CMD} -E \
		-e "s|(CFLAGS[[:space:]]*)= |\1+= |" \
		-e "s|(CPPFLAGS[[:space:]]*)= |\1+= |" \
		-e "s|(LDFLAGS[[:space:]]*)= |\1+= |" \
		${WRKSRC}/config.mk

post-install:
	@${STRIP_CMD} ${STAGEDIR}${PREFIX}/bin/dwm

post-install-DOCS-on:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${WRKSRC}/README ${STAGEDIR}${DOCSDIR}

do-test:
	${LOCALBASE}/libexec/atf-check -s exit:1 -e match:"dwm-${PORTVERSION}" \
		${STAGEDIR}${PREFIX}/bin/dwm -v

.include <bsd.port.mk>

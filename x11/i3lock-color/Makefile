# Created by: Jacob House <jacob@jwfh.ca>
# $FreeBSD$

PORTNAME=	i3lock-color
DISTVERSION=	2.12.c
CATEGORIES=	x11

MAINTAINER=	jacob@jwfh.ca
COMMENT=	Slightly improved screen locker based on slock

LICENSE=	BSD3CLAUSE
LICENSE_FILE=	${WRKSRC}/LICENSE

LIB_DEPENDS=	libcairo.so:graphics/cairo \
		libxcb-keysyms.so:x11/xcb-util-keysyms \
		libxcb-image.so:x11/xcb-util-image \
		libev.so:devel/libev \
		libxkbfile.so:x11/libxkbfile \
		libxkbcommon.so:x11/libxkbcommon \
		libxcb-util.so:x11/xcb-util \
		libxcb-xrm.so:x11/xcb-util-xrm \
		libjpeg.so:graphics/libjpeg-turbo

USES=		autoreconf gmake iconv localbase pkgconfig
USE_GITHUB=	yes
GH_ACCOUNT=	PandorasFox
GH_TAGNAME=	${DISTVERSION}
LDFLAGS+=	${ICONV_LIB}
USE_XORG=	x11 xcb xt xorgproto xext
USE_CSTD=	c99
GNU_CONFIGURE=	yes

MAKE_ARGS=	PREFIX="${PREFIX}" X11LIB="${LOCALBASE}/lib" \
		X11INC="${LOCALBASE}/include" CC="${CC}" \
		MANDIR="${MANPREFIX}/man"

CONFLICTS=	i3lock

PORTDOCS=	CHANGELOG README.md

OPTIONS_DEFINE=	DOCS

post-install:
	${STRIP_CMD} ${STAGEDIR}${PREFIX}/bin/i3lock
	${RM} ${STAGEDIR}${PREFIX}/etc/pam.d/i3lock
	${CHMOD} u+s ${STAGEDIR}${PREFIX}/bin/i3lock

post-install-DOCS-on:
	${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${PORTDOCS:S|^|${WRKSRC}/|} ${STAGEDIR}${DOCSDIR}

.include <bsd.port.mk>

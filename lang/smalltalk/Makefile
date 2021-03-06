# Created by: gpalmer
# $FreeBSD$

PORTNAME=	smalltalk
PORTVERSION=	3.2.5
PORTREVISION=	10
CATEGORIES=	lang
MASTER_SITES=	GNU

MAINTAINER=	johans@FreeBSD.org
COMMENT=	GNU Smalltalk

BUILD_DEPENDS=	zip:archivers/zip \
		gawk:lang/gawk
LIB_DEPENDS=	libgdbm.so:databases/gdbm \
		libcairo.so:graphics/cairo

OPTIONS_DEFINE=	PGSQL SDL
OPTIONS_DEFAULT=PGSQL SDL
OPTIONS_SUB=	yes
PGSQL_USES=	pgsql
SDL_USE=	SDL=image,mixer,sdl,sound,ttf

USES=		gmake iconv libtool localbase makeinfo pathfix pkgconfig \
		shebangfix sqlite tar:xz
USE_GNOME=	pango
USE_XORG=	ice xi xmu
USE_GL=		gl glut
GNU_CONFIGURE=	yes
CONFIGURE_ENV=	ac_cv_prog_EMACS=no ac_cv_prog_AWK=gawk
CONFIGURE_ARGS=	--enable-generational-gc=no \
		--enable-gtk=no \
		--localstatedir="${PREFIX}/var" \
		--with-emacs=no \
		--with-gmp=no
USE_LDCONFIG=	yes
SHEBANG_LANG=	sed
sed_OLD_CMD=	/bin/sed
sed_CMD=	${SED}
SHEBANG_FILES=	packages/vfs/deb packages/vfs/mailfs \
		examples/pepe.sed examples/xml.sed
PLIST_SUB=	VERSION="${PORTVERSION}"
PORTDATA=	*

INFO=		gst gst-base gst-libs

BROKEN_aarch64=	Fails to link: undefined reference to sbrk
BROKEN_sparc64=	Fails to install on sparc64

post-patch:
	@${REINPLACE_CMD} -e 's/ia64-\*-\* /&|amd64-*-* /' \
		${WRKSRC}/configure
	@${REINPLACE_CMD} -e 's/lrintl (truncl/lroundl (truncl/' \
		${WRKSRC}/libgst/prims.def \
		${WRKSRC}/libgst/prims.inl
	@${REINPLACE_CMD} -e '/^ac_include/s/\\$$/#include <wctype.h> \\/' \
		${WRKSRC}/snprintfv/configure

post-build:
	@${SED} -e 's|@bindir@|${PREFIX}/bin|g' \
		${WRKSRC}/gst-mode.el.in > ${WRKSRC}/gst-mode.el

post-install:
	@${LN} -sf gst-load.1 ${STAGEDIR}${MANPREFIX}/man/man1/gst-reload.1
	@${MKDIR} ${STAGEDIR}${DATADIR}/gtk
	${INSTALL_DATA} ${WRKSRC}/*.el ${STAGEDIR}${PREFIX}/share/emacs/site-lisp
	@${LS} -1 ${STAGEDIR}${PREFIX}/bin/gst* |grep -v config|${XARGS} ${STRIP_CMD}
	@${STRIP_CMD} ${STAGEDIR}${PREFIX}/lib/smalltalk/*.so
	@${STRIP_CMD} ${STAGEDIR}${PREFIX}/lib/libgst.so

.include <bsd.port.mk>

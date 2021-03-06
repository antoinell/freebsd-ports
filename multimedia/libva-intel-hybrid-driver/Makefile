# $FreeBSD$

PORTNAME=	intel-hybrid-driver
DISTVERSION=	1.0.2
CATEGORIES=	multimedia
PKGNAMEPREFIX=	libva-

PATCH_SITES=	https://github.com/${GH_ACCOUNT}/${GH_PROJECT}/commit/
PATCHFILES=	dfa9c8eba295.patch:-p1 b3b4d9a3a08d.patch:-p1

MAINTAINER=	jbeich@FreeBSD.org
COMMENT=	Hybrid VP8 encoder and VP9 decoder for Intel GPUs

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/COPYING

ONLY_FOR_ARCHS=	amd64 i386
ONLY_FOR_ARCHS_REASON=	Only Intel GPUs on x86 are supported

LIB_DEPENDS=	libdrm_intel.so:graphics/libdrm \
		libcmrt.so:multimedia/cmrt \
		libva.so:multimedia/libva

USES=		autoreconf compiler:c11 gmake libtool pkgconfig
USE_GITHUB=	yes
USE_LDCONFIG=	yes
GH_ACCOUNT=	01org
GNU_CONFIGURE=	yes
INSTALL_TARGET=	install-strip
PLIST_FILES=	lib/dri/hybrid_drv_video.so

post-patch:
	@${REINPLACE_CMD} -e '/__linux__/d; /LINUX/d' \
		${WRKSRC}/src/vp9hdec/Makefile.am

.include <bsd.port.mk>

# Created by: Jean-Baptiste Quenot <jb.quenot@caraldi.com>
# $FreeBSD$

PORTNAME=	rxtx
PORTVERSION=	2.2p2
PORTREVISION=	4
CATEGORIES=	comms java
MASTER_SITES=	http://rxtx.qbang.org/pub/rxtx/
PKGNAMESUFFIX=	-${JAVA_PORT:S/java\///}
DISTNAME=	${PORTNAME}-${PORTVERSION:S/p/pre/}

MAINTAINER=	james@elstone.net
COMMENT=	Native interface to serial ports in Java

LICENSE=	LGPL21
LICENSE_FILE=	${WRKSRC}/COPYING

NOT_FOR_ARCHS=		mips mips64
NOT_FOR_ARCHS_REASON=	Java not available for this architecture

USES=		gmake libtool zip

USE_JAVA=	yes
JAVA_VERSION=	1.6+
JAVA_OS=	native
GNU_CONFIGURE=	yes
CONFIGURE_ENV=	JAVA_HOME=${JAVA_HOME}
INSTALL_TARGET=	install-strip

USE_LDCONFIG=	yes

PLIST_SUB=	JAVA_HOME=${JAVA_HOME:S,^${PREFIX}/,,}

.include <bsd.port.pre.mk>

.if ${ARCH} == "powerpc64"
PLIST_SUB+=	ARCH=ppc64
.else
PLIST_SUB+=	ARCH=${ARCH}
.endif

.include <bsd.port.post.mk>

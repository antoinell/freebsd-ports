# Created by: Koop Mast <kwm@FreeBSD.org>
# $FreeBSD$

PORTNAME=	gstreamer1-editing-services
PORTVERSION=	1.14.4
CATEGORIES=	multimedia
MASTER_SITES=	http://gstreamer.freedesktop.org/src/gstreamer-editing-services/
DISTNAME=	gstreamer-editing-services-${PORTVERSION}

MAINTAINER=	multimedia@FreeBSD.org
COMMENT=	GStreamer editing services

PORTSCOUT=	limitw:1,even

USES=		compiler:c11 gmake gnome libtool pathfix python:3.6+ pkgconfig tar:xz
USE_LDCONFIG=	yes
GNU_CONFIGURE=	yes
USE_GNOME=	glib20 introspection:build libxml2 pygobject3:build
USE_GSTREAMER1=	good
INSTALL_TARGET=	install-strip

CONFIGURE_ARGS=	--enable-introspection=yes \
		--with-bash-completion-dir=${PREFIX}/share/bash-completion/completions
PLIST_SUB=	VERSION=1.0 SOVERSION=0.1404.0

.include <bsd.port.mk>

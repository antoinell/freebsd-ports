# $FreeBSD$

PORTNAME=	SimpleSoapy
DISTVERSION=	1.5.1
PORTREVISION=	1
CATEGORIES=	misc hamradio python
MASTER_SITES=	CHEESESHOP
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	yuri@FreeBSD.org
COMMENT=	Simple pythonic wrapper for SoapySDR library

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/LICENSE

RUN_DEPENDS=	${PYNUMPY} \
		${PYTHON_PKGNAMEPREFIX}SoapySDR>0:misc/py-SoapySDR@${PY_FLAVOR}

USES=		python:3.4+
USE_PYTHON=	distutils autoplist
NO_ARCH=	yes

.include <bsd.port.mk>

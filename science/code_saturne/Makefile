# Created by: thierry@pompo.net
# $FreeBSD$

PORTNAME=	code_saturne
PORTVERSION=	5.3.0
DISTVERSIONPREFIX=	v
CATEGORIES=	science parallel

MAINTAINER=	thierry@FreeBSD.org
COMMENT=	EDF's general purpose Computational Fluid Dynamics (CFD) software

LICENSE=	GPLv2

BUILD_DEPENDS=	python:lang/python
LIB_DEPENDS=	libsysinfo.so:devel/libsysinfo	\
		libcgns.so:science/cgnslib	\
		libhdf5.so:science/hdf5		\
		libomp.so:devel/openmp		\
		libmedC.so:french/med
RUN_DEPENDS=	xmgrace:math/grace	\
		bash:shells/bash	\
		xterm:x11/xterm

USE_GITHUB=	yes
GH_ACCOUNT=	code-saturne

USES=		autoreconf bison fortran gettext gnome gmake iconv libtool	\
		pyqt:5 python:2.7 shebangfix
USE_GNOME=	libxml2
USE_PYQT=	core gui sip widgets xml_build
CPPFLAGS+=	-I${LOCALBASE}/include -I${LOCALBASE}/include/libxml2
GNU_CONFIGURE=	yes
USE_LDCONFIG=	yes

OPTIONS_DEFINE=		DOCS EXAMPLES ATLAS BATCH MPI
OPTIONS_DEFAULT=	BATCH MPI METIS
OPTIONS_RADIO=		METIS
OPTIONS_RADIO_METIS=	METIS PARMETIS
ATLAS_USES=		blaslapack:atlas
ATLAS_CONFIGURE_ON=	--with-blas=yes --with-blas-type=ATLAS
BATCH_DESC=		Use Torque to submit batches
BATCH_RUN_DEPENDS=	pbs-config:sysutils/torque
MPI_LIB_DEPENDS=	libmpi.so:net/mpich
MPI_CONFIGURE_WITH=	mpi
METIS_LIB_DEPENDS=	libmetis.so:math/metis
METIS_CONFIGURE_ON=	--with-metis-include="${LOCALBASE}/include"
PARMETIS_LIB_DEPENDS=	libparmetis.so:math/parmetis
PARMETIS_CONFIGURE_ON=	--with-metis-include="${LOCALBASE}/include/parmetis"	\
			--with-metis-lib="${LOCALBASE}/lib/parmetis"
PARMETIS_CONFIGURE_ENV=	LIBS=-lexecinfo

#TEST_TARGET=	check

.if defined(PACKAGE_BUILDING)
TERM=		vt100	# Force for pointyhat to override su
.else
TERM?=		vt100	# Default value needed for tput in jail or tinderbox
.endif

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MDOCS}
USE_TEX=	tex:build
BUILD_DEPENDS+=	fig2dev:print/transfig		\
		doxygen:devel/doxygen		\
		dot:graphics/graphviz		\
		sphinx-build:textproc/py-sphinx@${PY_FLAVOR}
ALL_TARGET=	all pdf
DOCS=		AUTHORS ChangeLog README
.endif

pre-configure:
	(cd ${WRKSRC} && ${LS} preprocessor/*/*.c src/*/*.c* |	\
		${GREP} -v user_examples > po/POTFILES.in)
	${FLEX} -o ${WRKSRC}/src/mei/mei_scanner.c ${WRKSRC}/src/mei/mei_scanner.l
	${LOCALBASE}/bin/bison --defines=${WRKSRC}/src/mei/mei_parser.h	\
		-o ${WRKSRC}/src/mei/mei_parser.c ${WRKSRC}/src/mei/mei_parser.y

post-install:
.if ${PORT_OPTIONS:MDOCS}
	${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${DOCS:C|^|${WRKSRC}/|} ${STAGEDIR}${DOCSDIR}
.endif
.if ${PORT_OPTIONS:MEXAMPLES}
	${MKDIR} ${STAGEDIR}${EXAMPLESDIR}
	cd ${WRKSRC}/examples && ${COPYTREE_SHARE} \* ${STAGEDIR}${EXAMPLESDIR}
.endif

.include <bsd.port.mk>

PORTNAME=	libXNVCtrl
DISTVERSION=	595.112.07
CATEGORIES=	x11

MAINTAINER=	norotera54@duck.com
COMMENT=	Client library for the NV-CONTROL X extension
WWW=		https://github.com/NVIDIA/nvidia-settings

LICENSE=	MIT

USES=		xorg
USE_XORG=	x11 xext
USE_GITHUB=	yes
GH_ACCOUNT=	NVIDIA
GH_PROJECT=	nvidia-settings
WRKSRC_SUBDIR=	src/libXNVCtrl
USE_LDCONFIG=	yes

PLIST_FILES=	include/NVCtrl/NVCtrl.h \
		include/NVCtrl/NVCtrlLib.h \
		include/NVCtrl/nv_control.h \
		lib/libXNVCtrl.so \
		lib/libXNVCtrl.so.0

# Upstream only builds a static libXNVCtrl.a; build the shared library as well
do-build:
	cd ${WRKSRC} && ${CC} ${CFLAGS} -fPIC -shared -I. -I${LOCALBASE}/include \
		-Wl,-soname,libXNVCtrl.so.0 -o libXNVCtrl.so.0 NVCtrl.c \
		-L${LOCALBASE}/lib -lXext -lX11

do-install:
	${INSTALL_LIB} ${WRKSRC}/libXNVCtrl.so.0 ${STAGEDIR}${PREFIX}/lib/
	${LN} -sf libXNVCtrl.so.0 ${STAGEDIR}${PREFIX}/lib/libXNVCtrl.so
	${MKDIR} ${STAGEDIR}${PREFIX}/include/NVCtrl
	${INSTALL_DATA} ${WRKSRC}/NVCtrl.h ${WRKSRC}/NVCtrlLib.h \
		${WRKSRC}/nv_control.h ${STAGEDIR}${PREFIX}/include/NVCtrl/

.include <bsd.port.mk>

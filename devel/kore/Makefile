PORTNAME=	kore
PORTVERSION=	4.1.0
CATEGORIES=	devel www
MASTER_SITES=	https://kore.io/releases/

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Web application framework for writing web APIs in C
WWW=		http://www.kore.io/

LICENSE=	ISCL
LICENSE_FILE=	${WRKSRC}/LICENSE

BROKEN_SSL=	openssl30 openssl31
BROKEN_SSL_REASON=	Requires OpenSSL 3.0.0 deprecated RSA_* routines

USES=		compiler:c11 gmake ssl

MAKE_ARGS=	OPENSSL_PATH=${OPENSSLBASE}
CFLAGS+=	${CFLAGS_${CHOSEN_COMPILER_TYPE}}
# 12.0 + -pedantic
CFLAGS_clang=	-Wno-error=c11-extensions

PORTEXAMPLES=	*

OPTIONS_DEFINE=		ACME CURL DEBUG EXAMPLES HTTP JSONRPC PGSQL PYTHON \
			TASKS TLS
OPTIONS_DEFAULT=	ACME CURL HTTP JSONRPC PGSQL PYTHON TASKS TLS
OPTIONS_SUB=		yes

ACME_DESC=	Build with ACME support
HTTP_DESC=	Build with HTTP support
JSONRPC_DESC=	Build with JSON-RPC support
TASKS_DESC=	Build with tasks support

ACME_MAKE_ARGS=		ACME=1
CURL_LIB_DEPENDS=	libcurl.so:ftp/curl
CURL_MAKE_ARGS=		CURL=1
DEBUG_MAKE_ARGS=	DEBUG=1
HTTP_MAKE_ARGS_OFF=	NOHTTP=1
JSONRPC_IMPLIES=	HTTP
JSONRPC_LIB_DEPENDS=	libyajl.so:devel/yajl
JSONRPC_MAKE_ARGS=	JSONRPC=1
PGSQL_IMPLIES=		HTTP
PGSQL_USES=		pgsql
PGSQL_MAKE_ARGS=	PGSQL=1
PYTHON_USES=		gettext-runtime python
PYTHON_MAKE_ARGS=	PYTHON=1
PYTHON_BINARY_ALIAS=	python3-config=${PYTHON_CMD}-config
TASKS_MAKE_ARGS=	TASKS=1
TLS_MAKE_ARGS_OFF=	NOTLS=1

.include <bsd.port.options.mk>

.if ( ${OPSYS} == FreeBSD && ${OSVERSION} >= 1400092 && ${SSL_DEFAULT} == base ) || ${SSL_DEFAULT:Mopenssl3*}
CFLAGS+=	-DOPENSSL_API_COMPAT=0x10100000L
.endif

.include <bsd.port.pre.mk>

.if ${COMPILER_TYPE} == clang && ${COMPILER_VERSION} >= 160
CFLAGS+=	-Wno-error=incompatible-pointer-types-discards-qualifiers
.endif

post-patch:
.if ${LOCALBASE} != /usr/local
	@${REINPLACE_CMD} 's|/usr/local/|${LOCALBASE}/|g' \
		${WRKSRC}/Makefile
.endif
	@${REINPLACE_CMD} 's|%%OPENSSLINC%%|${OPENSSLINC}|g' \
		${WRKSRC}/src/cli.c

post-install:
	${STRIP_CMD} ${STAGEDIR}${PREFIX}/bin/kodev \
		${STAGEDIR}${PREFIX}/bin/kore

post-install-EXAMPLES-on:
	@cd ${WRKSRC}/examples && ${COPYTREE_SHARE} . ${STAGEDIR}${EXAMPLESDIR}
	@cd ${WRKSRC}/conf && ${COPYTREE_SHARE} . ${STAGEDIR}${EXAMPLESDIR}

.include <bsd.port.post.mk>

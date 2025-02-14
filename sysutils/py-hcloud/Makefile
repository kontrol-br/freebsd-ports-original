PORTNAME=	hcloud
DISTVERSION=	1.27.2
CATEGORIES=	sysutils python
MASTER_SITES=	PYPI
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	matthew@FreeBSD.org
COMMENT=	Official Hetzner Cloud python library
WWW=		https://hcloud-python.readthedocs.io/en/latest/

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/LICENSE

BUILD_DEPENDS=	${PY_SETUPTOOLS} \
		${PYTHON_PKGNAMEPREFIX}wheel>=0:devel/py-wheel@${PY_FLAVOR}

RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}requests>=2.20,<3:www/py-requests@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}dateutil>=2.7.5:devel/py-dateutil@${PY_FLAVOR}

TEST_DEPENDS=	${PYTHON_PKGNAMEPREFIX}pre-commit>=0:devel/py-pre-commit@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}pyupgrade>=3.6.0:devel/py-pyupgrade@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}flake8>=6.0.0:devel/py-flake8@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}isort>=5.12.0:devel/py-isort@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}mock>=2.0.0:devel/py-mock@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}tox>=3.23.1:devel/py-tox@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}black>=23.3.0:devel/py-black@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}mypy>=1.4.1:devel/py-mypy@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}types-python-dateutil>=0:devel/py-types-python-dateutil@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}types-requests>=0:devel/py-types-requests@${PY_FLAVOR}

NO_ARCH=	yes
USES=		python:3.8+
USE_PYTHON=	autoplist concurrent pep517 pytest

.include <bsd.port.mk>

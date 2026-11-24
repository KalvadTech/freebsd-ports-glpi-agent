PORTNAME=	glpi-agent
DISTVERSION=	1.21
CATEGORIES=	net-mgmt

MAINTAINER=	mazhe@alkumuna.eu
COMMENT=	Generic management agent
WWW=		https://github.com/glpi-project/glpi-agent

LICENSE=	GPLv2

BUILD_DEPENDS=	p5-Module-Install>=0:devel/p5-Module-Install \
		${RUN_DEPENDS}
RUN_DEPENDS=	p5-File-Which>=0:sysutils/p5-File-Which \
		p5-libwww>=0:www/p5-libwww \
		p5-Net-IP>=0:net-mgmt/p5-Net-IP \
		p5-Text-Template>=0:textproc/p5-Text-Template \
		p5-UNIVERSAL-require>=0:devel/p5-UNIVERSAL-require \
		p5-XML-LibXML>=0:textproc/p5-XML-LibXML \
		p5-Cpanel-JSON-XS>=0:converters/p5-Cpanel-JSON-XS \
		p5-DateTime>=0:devel/p5-DateTime \
		p5-Data-UUID>=0:devel/p5-Data-UUID \
		p5-YAML-Tiny>=0:textproc/p5-YAML-Tiny

USES=		perl5
USE_PERL5=	configure
CONFIGURE_ARGS+=LOCALSTATEDIR=/var/glpi-agent
USE_GITHUB=	yes
GH_ACCOUNT=	glpi-project

OPTIONS_DEFINE=		CUPS DAEMON HTTPS WEBSERVER
OPTIONS_GROUP=		TASKS
OPTIONS_GROUP_TASKS=	COLLECT DEPLOY ESX INVENTORY NETDISCOVERY NETINVENTORY REMOTEINVENTORY WAKEONLAN
OPTIONS_DEFAULT=	DAEMON HTTPS INVENTORY
OPTIONS_SUB=		yes
DAEMON_DESC=		Install a rcscript
COLLECT_DESC=		Install Collect task
DEPLOY_DESC=		Install Deploy task
ESX_DESC=		Install ESX task
INVENTORY_DESC=		Install Inventory task
NETDISCOVERY_DESC=	Install NetDiscovery task
NETINVENTORY_DESC=	Install NetInventory task
REMOTEINVENTORY_DESC=	Install RemoteIntentory task
WAKEONLAN_DESC=		Install WakeOnLan task

DAEMON_RUN_DEPENDS=	p5-Proc-Daemon>=0:devel/p5-Proc-Daemon \
			p5-Proc-PID-File>=0:devel/p5-Proc-PID-File
HTTPS_RUN_DEPENDS=	p5-LWP-Protocol-https>=0:www/p5-LWP-Protocol-https
WEBSERVER_RUN_DEPENDS=	p5-HTTP-Daemon>=0:www/p5-HTTP-Daemon
DEPLOY_RUN_DEPENDS=	p5-Archive-Extract>=0:archivers/p5-Archive-Extract \
			p5-Digest-SHA>=0:security/p5-Digest-SHA \
			p5-File-Copy-Recursive>=0:devel/p5-File-Copy-Recursive \
			p5-Any-URI-Escape>=0:www/p5-Any-URI-Escape \
			p5-Net-Ping>=0:net/p5-Net-Ping \
			p5-Parallel-ForkManager>=0:devel/p5-Parallel-ForkManager
INVENTORY_RUN_DEPENDS=	dmidecode:sysutils/dmidecode
NETDISCOVERY_RUN_DEPENDS=	p5-Thread-Queue>=0:devel/p5-Thread-Queue \
				p5-Net-SNMP>=0:net-mgmt/p5-Net-SNMP
NETINVENTORY_RUN_DEPENDS=	p5-Thread-Queue>=0:devel/p5-Thread-Queue \
				p5-Net-SNMP>=0:net-mgmt/p5-Net-SNMP
REMOTEINVENTORY_RUN_DEPENDS=	p5-Net-SSH2>=0:net/p5-Net-SSH2
WAKEONLAN_RUN_DEPENDS=	p5-Net-Write>=0:net/p5-Net-Write

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MCUPS}
INVENTORY_RUN_DEPENDS+=	p5-Net-CUPS>=0:print/p5-Net-CUPS
.endif
.if ${PORT_OPTIONS:MDAEMON}
USE_RC_SUBR=	glpi_agent
.endif

post-install:
	${MV} ${STAGEDIR}${ETCDIR}/agent.cfg ${STAGEDIR}${ETCDIR}/agent.cfg.sample

.include <bsd.port.mk>

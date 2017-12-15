---
title: Servernetzwerkkonfiguration | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/27/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Named Pipes [SQL Server], configuring
- connections [SQL Server], server network configuration
- Database Engine [SQL Server], network configurations
- server network configuration [SQL Server]
- protocols [SQL Server], choosing
- ports [SQL Server], changing
- server configuration [SQL Server]
ms.assetid: 890c09a1-6dad-4931-aceb-901c02ae34c5
caps.latest.revision: "50"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 88db862493213badd36cfcaf4301cc1be6da5881
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="server-network-configuration"></a>Server-Netzwerkkonfiguration
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Zu den Aufgaben, die im Rahmen der Server-Netzwerkkonfiguration durchgeführt werden müssen, gehören das Aktivieren von Protokollen, das Ändern des Anschlusses oder der Pipe, der bzw. die von einem Protokoll verwendet wird, das Konfigurieren der Verschlüsselung, das Konfigurieren des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Browser-Diensts, das Offenlegen oder Verbergen von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] im Netzwerk sowie das Registrieren des Serverprinzipalnamens (SPN). In den meisten Fällen ist es nicht erforderlich, die Server-Netzwerkkonfiguration zu ändern. Konfigurieren Sie die Server-Netzwerkprotokolle nur dann neu, wenn spezielle Netzwerkanforderungen erfüllt werden müssen.  
  
 Die Netzwerkkonfiguration für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erfolgt mithilfe des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Managers. Verwenden Sie für frühere Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]die SQL Server-Netzwerkkonfiguration, die zum Lieferumfang dieser Produkte gehört.  
  
## <a name="protocols"></a>Protokolle  
 Mithilfe des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Managers können Sie die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwendeten Protokolle aktivieren oder deaktivieren und die für die Protokolle verfügbaren Optionen konfigurieren. Es können mehrere Protokolle aktiviert werden. Sie müssen alle Protokolle aktivieren, die von den Clients verwendet werden sollen. Alle Protokolle verfügen über den gleichen Zugriff auf den Server. Informationen dazu, welche Protokolle verwendet werden sollten, finden Sie unter [Aktivieren oder Deaktivieren eines Servernetzwerkprotokolls](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md) und [Standardkonfiguration für das SQL Server-Netzwerkprotokoll](../../database-engine/configure-windows/default-sql-server-network-protocol-configuration.md).  
  
### <a name="changing-a-port"></a>Ändern eines Anschlusses  
 Sie können das TCP/IP-Protokolle konfigurieren, um an einem bestimmten Port zu lauschen. Die Standardinstanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] lauscht an TCP-Port 1433. Benannte Instanzen von [!INCLUDE[ssDE](../../includes/ssde-md.md)] und [!INCLUDE[ssEW](../../includes/ssew-md.md)] sind für dynamische Ports konfiguriert. Dies bedeutet, dass sie einen verfügbaren Port auswählen, wenn der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst gestartet wird. Mithilfe des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browser-Diensts können Clients den Anschluss identifizieren, wenn sie eine Verbindung herstellen.  
  
 Bei der Konfiguration für dynamische Anschlüsse verwendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] möglicherweise bei jedem Start einen anderen Anschluss. Wenn Sie durch eine Firewall eine Verbindung zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen, müssen Sie den von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwendeten Anschluss öffnen. Konfigurieren Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für die Verwendung eines bestimmten Anschlusses, damit Sie die Firewall so konfigurieren können, dass die Kommunikation mit dem Server möglich ist. Weitere Informationen finden Sie unter [Konfigurieren eines Servers zur Überwachung eines bestimmten TCP-Ports &#40;SQL Server-Konfigurations-Manager&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md).  
  
### <a name="changing-a-named-pipe"></a>Ändern einer Named Pipe  
 Sie können das Named Pipe-Protokoll so konfigurieren, dass an einer bestimmte Named Pipe gelauscht wird. Standardmäßig lauscht die Standardinstanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] an der Pipe „\\\\.\pipe\sql\query“ für die Standardinstanz und „\\\\.\pipe\MSSQL$*\<Instanzname>*\sql\query“ für eine benannte Instanz. [!INCLUDE[ssDE](../../includes/ssde-md.md)] kann nur an einer benannten Pipe lauschen, aber Sie können die Pipe bei Bedarf ändern. Mithilfe des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Browser-Diensts können Clients die Pipe identifizieren, wenn sie eine Verbindung herstellen. Weitere Informationen finden Sie unter [Konfigurieren eines Servers für die Überwachung einer alternativen Pipe &#40;SQL Server-Konfigurations-Manager&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-an-alternate-pipe.md).  
  
## <a name="force-encryption"></a>Erzwingen der Verschlüsselung  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] kann so konfiguriert werden, dass bei der Kommunikation mit Clientanwendungen eine Verschlüsselung erforderlich ist. Weitere Informationen finden Sie unter [Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul &#40;SQL Server-Konfigurations-Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
## <a name="extended-protection-for-authentication"></a>Erweiterter Schutz für die Authentifizierung  
 Die Unterstützung für den erweiterten Schutz für die Authentifizierung mit Kanalbindung und Dienstbindung ist für Betriebssysteme verfügbar, die den erweiterten Schutz unterstützen. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit dem Datenbankmodul unter Verwendung von Erweiterter Schutz](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md).  
  
## <a name="authenticating-by-using-kerberos"></a>Authentifizierung durch Kerberos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt die Kerberos-Authentifizierung. Weitere Informationen finden Sie unter [Registrieren eines Dienstprinzipalnamens für Kerberos-Verbindungen](../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md) und [Microsoft Kerberos Configuration Manager for SQL Server](http://www.microsoft.com/download/details.aspx?id=39046).  
  
### <a name="registering-a-server-principal-name-spn"></a>Registrieren eines Serverprinzipalnamens (SPN)  
 Der Kerberos-Authentifizierungsdienst verwendet einen SPN zum Authentifizieren eines Diensts. Weitere Informationen finden Sie unter [Registrieren eines Dienstprinzipalnamens für Kerberos-Verbindungen](../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md).  
  
 SPNs können auch verwendet werden, um die Clientauthentifizierung bei der Verbindung mit NTLM sicherer zu gestalten. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit dem Datenbankmodul unter Verwendung von Erweiterter Schutz](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md).  
  
## <a name="sql-server-browser-service"></a>SQL Server-Browserdienst  
 Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser-Dienst wird auf dem Server ausgeführt und unterstützt Clientcomputer bei der Suche nach [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanzen. Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Browserdienst muss nicht konfiguriert werden, er muss jedoch in einigen Verbindungsszenarien ausgeführt werden. Weitere Informationen zum [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Browser finden Sie unter [SQL Server-Browserdienst &#40;Datenbankmodul und SSAS&#41;](../../database-engine/configure-windows/sql-server-browser-service-database-engine-and-ssas.md).  
  
## <a name="hiding-sql-server"></a>Ausblenden von SQL Server  
 Wenn der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browser ausgeführt wird, antwortet er auf Abfragen mit dem Namen, der Version und den Verbindungsinformationen für jede installierte Instanz. Das Flag **HideInstance** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]für gibt an, dass der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browser nicht mit Informationen zu dieser Serverinstanz reagieren soll. Clientanwendungen können zwar eine Verbindung herstellen, aber sie müssen über die erforderlichen Verbindungsinformationen verfügen. Weitere Informationen finden Sie unter [Ausblenden einer Instanz des SQL Server-Datenbankmoduls](../../database-engine/configure-windows/hide-an-instance-of-sql-server-database-engine.md).  
  
## <a name="related-content"></a>Verwandte Inhalte  
 [Client-Netzwerkkonfiguration](../../database-engine/configure-windows/client-network-configuration.md)  
  
 [Verwalten der Datenbankmoduldienste](../../database-engine/configure-windows/manage-the-database-engine-services.md)  
  
  

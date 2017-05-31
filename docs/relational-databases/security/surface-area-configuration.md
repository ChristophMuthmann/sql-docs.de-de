---
title: "Oberflächenkonfiguration | Microsoft Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- reducing attackable surface area
- upgrading SQL Server, security
- surface area configuration [SQL Server]
- surface area configuration [SQL Server], about surface area configuration
- attackable surface area [SQL Server]
- installing SQL Server, security
ms.assetid: f741169c-1453-4ad2-830b-bf2be27d712f
caps.latest.revision: 79
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6ee5522ce1d173dfd979b64d428be2e6e05ded00
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="surface-area-configuration"></a>Oberflächenkonfiguration
  Bei neuen Installationen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sind viele Funktionen in der Standardkonfiguration nicht aktiviert. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] führt die Installation selektiv durch und startet nur zentrale Dienste und Funktionen, damit möglichst wenige Funktionen eine Angriffsfläche für böswillige Benutzer bieten. Zum Zeitpunkt der Installation können diese Standardeinstellungen von einem Systemadministrator geändert werden. Ebenso ist es möglich, Funktionen einer laufenden Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]selektiv zu aktivieren oder zu deaktivieren. Darüber hinaus sind einige Komponenten beim Herstellen einer Verbindung von anderen Computern möglicherweise erst verfügbar, wenn Protokolle konfiguriert werden.  
  
> [!NOTE]  
>  Im Unterschied zu neuen Installationen werden während eines Upgrades keine bestehenden Dienste oder Funktionen deaktiviert. Es können jedoch nach Abschluss des Upgrades zusätzliche Optionen für die Oberflächenkonfiguration angewendet werden.  
  
## <a name="protocols-connection-and-startup-options"></a>Protokolle, Verbindungs- und Startoptionen  
 Verwenden Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager, um Dienste zu starten oder zu beenden, die Startoptionen zu konfigurieren und Protokolle sowie andere Verbindungsoptionen zu aktivieren.  
  
#### <a name="to-start-sql-server-configuration-manager"></a>So starten Sie den SQL Server-Konfigurations-Manager  
  
1.  Zeigen Sie im Menü **Start** auf **Alle Programme**, dann auf [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], danach auf **Konfigurationstools**, und klicken Sie auf **SQL Server-Konfigurations-Manager**.  
  
    -   Verwenden Sie den Bereich **SQL Server-Dienste** , um Komponenten zu starten und die automatischen Startoptionen zu konfigurieren.  
  
    -   Verwenden Sie den Bereich **SQL Server-Netzwerkkonfiguration** , um Verbindungsprotokolle und Verbindungsoptionen wie feste TCP/IP-Ports zu aktivieren oder die Verschlüsselung zu erzwingen.  
  
 Weitere Informationen finden Sie unter [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md). Remotekonnektivität kann auch von der richtigen Konfiguration einer Firewall abhängen. Weitere Informationen finden Sie unter [Konfigurieren der Windows-Firewall für den SQL Server-Zugriff](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
## <a name="enabling-and-disabling-features"></a>Aktivieren und Deaktivieren von Funktionen  
 Das Aktivieren und Deaktivieren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Funktionen kann mit Facets in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]konfiguriert werden.  
  
#### <a name="to-configure-surface-area-using-facets"></a>So konfigurieren Sie die Oberfläche mit Facets  
  
1.  Stellen Sie in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] eine Verbindung mit einer Komponente von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]her.  
  
2.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf den Server, und klicken Sie dann auf **Facets**.  
  
3.  Erweitern Sie im Dialogfeld **Facets anzeigen** die Liste **Facet** , und wählen Sie das entsprechende **Oberflächenkonfigurations-Facet** (**Oberflächenkonfiguration**, **Oberflächenkonfiguration für Analysis Services**oder **Oberflächenkonfiguration für Reporting Services**) aus.  
  
4.  Wählen Sie im Bereich **Facet-Eigenschaften** die gewünschten Werte für jede Eigenschaft aus.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Verwenden Sie die richtlinienbasierte Verwaltung, um die Konfiguration eines Facets in regelmäßigen Abständen zu überprüfen. Weitere Informationen finden Sie unter [Verwalten von Servern mit der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md).  
  
 Sie können [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Optionen auch mit der gespeicherten Prozedur **sp_configure** festlegen. Weitere Informationen finden Sie unter [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
 Verwenden Sie die Eigenschaftseinstellungen in **, um die** EnableIntegrated Security [!INCLUDE[ssRS](../../includes/ssrs-md.md)]-Eigenschaft von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]zu ändern. Bearbeiten Sie die Konfigurationsdatei **RSReportServer.config** , um die Eigenschaften **Geplante Ereignisse und Berichtsübermittlung** und **Webdienst und HTTP-Zugriff** zu ändern.  
  
## <a name="command-prompt-options"></a>Befehlszeilenoptionen  
 Mit dem PowerShell-Cmdlet **Invoke-PolicyEvaluation** von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] können Sie Oberflächenkonfigurations-Richtlinien aufrufen. Weitere Informationen finden Sie unter [Verwenden der Datenbankmodul-Cmdlets](../../relational-databases/scripting/use-the-database-engine-cmdlets.md).  
  
## <a name="soap-and-service-broker-endpoints"></a>SOAP- und Service Broker-Endpunkte  
 Mithilfe der richtlinienbasierte Verwaltung können Sie Endpunkte ausschalten. Verwenden Sie zum Erstellen und Ändern der Eigenschaften von Endpunkten [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md) und [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md).  
  
## <a name="related-content"></a>Verwandte Inhalte  
 [Sicherheitscenter für SQL Server-Datenbankmodul und Azure SQL-Datenbank](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  

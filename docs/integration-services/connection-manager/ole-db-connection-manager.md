---
title: OLE DB-Verbindungs-Manager | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: connection-manager
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.oledbconnection.f1
helpviewer_keywords:
- OLE DB connection manager
- data sources [Integration Services], connections
- connection managers [Integration Services], OLE DB
- connections [Integration Services], OLE DB
ms.assetid: 91e3622e-4b1a-439a-80c7-a00b90d66979
caps.latest.revision: 59
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 404c238b8b2b74b94f118c6b3303c7778e5d9120
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="ole-db-connection-manager"></a>OLE DB-Verbindungs-Manager
  Durch einen OLE DB-Verbindungs-Manager kann ein Paket mithilfe eines OLE DB-Anbieters eine Verbindung mit einer Datenquelle herstellen. Beispielsweise kann ein OLE DB-Verbindungs-Manager, der eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellt, den [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB-Anbieter für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwenden.    
    
> [!NOTE]    
>  Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 11.0 OLEDB-Anbieter unterstützt die neuen Schlüsselwörter für Verbindungszeichenfolgen (MultiSubnetFailover=True) für Multisubnetz-Failoverclustering nicht. Weitere Informationen finden Sie in den [Versionsanmerkungen zu SQL Server](http://go.microsoft.com/fwlink/?LinkId=247824) und im Blogbeitrag zu [Always On-Multisubnetz-Failover und SSIS](http://www.mattmasson.com/2012/03/alwayson-multi-subnet-failover-and-ssis/)unter www.mattmasson.com.    
    
> [!NOTE]    
>  Wenn es sich bei der Datenquelle um [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007 oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 2007 handelt, erfordert die Datenquelle einen anderen Datenanbieter als frühere Versionen von Excel oder Access. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit einer Excel-Arbeitsmappe](../../integration-services/connection-manager/connect-to-an-excel-workbook.md) und [Herstellen einer Verbindung mit einer Access-Datenbank](../../integration-services/connection-manager/connect-to-an-access-database.md).    
    
 Mehrere Tasks und Datenflusskomponenten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] verwenden einen OLE DB-Verbindungs-Manager. Beispielsweise extrahieren und laden die OLE DB-Quelle und das OLE DB-Ziel mit diesem Verbindungs-Manager Daten. Und der Task SQL ausführen kann damit eine Verbindung mit einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank herstellen, um Abfragen auszuführen.    
    
 Der OLE DB-Verbindungs-Manager wird auch für den Zugriff auf OLE DB-Datenquellen in benutzerdefinierten Tasks verwendet, die in nicht verwaltetem Code und einer Programmiersprache wie z. B. C++ geschrieben sind.    
    
 Wenn Sie einem Paket einen OLE DB-Verbindungs-Manager hinzufügen, erstellt [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] einen Verbindungs-Manager, der zur Laufzeit in eine OLE DB-Verbindung aufgelöst wird, die Eigenschaften des Verbindungs-Managers festlegt und der **Connections** -Sammlung im Paket den Verbindungs-Manager hinzufügt.    
    
 Die **ConnectionManagerType** -Eigenschaft des Verbindungs-Managers ist auf **OLEDB**festgelegt.    
    
 Der OLE DB-Verbindungs-Manager kann wie folgt konfiguriert werden:    
    
-   Stellen Sie eine Verbindungszeichenfolge bereit, die die Anforderungen des ausgewählten Anbieters erfüllt.    
    
-   Schließen Sie in Abhängigkeit vom Anbieter den Namen der Datenquelle ein, mit der eine Verbindung hergestellt werden soll.    
    
-   Stellen Sie entsprechende Sicherheitsanmeldeinformationen für den ausgewählten Anbieter bereit.    
    
-   Geben Sie an, ob die im Verbindungs-Manager erstellte Verbindung zur Laufzeit beibehalten wird.    
    
## <a name="logging"></a>Protokollierung    
 Sie können die vom OLE DB-Verbindungs-Manager an externe Datenanbieter gerichteten Aufrufe protokollieren. Mithilfe dieser Protokollierungsfunktionen können Sie Probleme bei Verbindungen behandeln, die vom OLE DB-Verbindungs-Manager mit externen Datenquellen hergestellt werden. Aktivieren Sie zum Protokollieren der vom OLE DB-Verbindungs-Manager an externe Datenanbieter gerichteten Aufrufe die Paketprotokollierung, und wählen Sie das **Diagnostic** -Ereignis auf Paketebene aus. Weitere Informationen finden Sie unter [Behandeln von Problemen mit Paketausführungstools](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).    
    
## <a name="configuration-of-the-oledb-connection-manager"></a>Konfiguration des OLEDB-Verbindungs-Managers    
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen. Weitere Informationen zu den Eigenschaften, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können, finden Sie unter [Konfigurieren des OLE DB-Verbindungs-Managers](../../integration-services/connection-manager/configure-ole-db-connection-manager.md). Informationen zum programmgesteuerten Konfigurieren eines Verbindungs-Managers finden Sie in der Dokumentation zur **T:Microsoft.SqlServer.Dts.Runtime.ConnectionManager** -Klasse im Entwicklerhandbuch.    
    
## <a name="related-content"></a>Verwandte Inhalte    
    
-   Wiki-Artikel, [SSIS with Oracle Connectors](http://go.microsoft.com/fwlink/?LinkId=220670) , auf social.technet.microsoft.com.    
    
-   Technischer Artikel, [Connection Strings for OLE DB Providers](http://go.microsoft.com/fwlink/?LinkId=220744)(Verbindungszeichenfolgen für OLE DB-Anbieter), auf carlprothman.net.    
    
## <a name="configure-ole-db-connection-manager"></a>OLE DB-Verbindungs-Manager konfigurieren
  Fügen Sie mithilfe des Dialogfelds **OLE DB-Verbindungs-Manager konfigurieren** einer Datenquelle eine Verbindung hinzu. Dabei kann es sich um eine neue Verbindung oder eine Kopie einer vorhandenen Verbindung handeln.  
  
> [!NOTE]  
>  Wenn es sich bei der Datenquelle um [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007 handelt, erfordert die Datenquelle einen anderen Verbindungs-Manager als frühere Versionen von Excel. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit einer Excel-Arbeitsmappe](../../integration-services/connection-manager/connect-to-an-excel-workbook.md).  
>   
>  Wenn es sich bei der Datenquelle um [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 2007 handelt, erfordert die Datenquelle einen anderen OLE DB-Anbieter als frühere Versionen von Access. Weitere Informationen finden Sie unter [Herstellen einer Verbindung zu einer Access-Datenbank](../../integration-services/connection-manager/connect-to-an-access-database.md).  
  
 Weitere Informationen zum OLE DB-Verbindungs-Manager finden Sie unter [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
### <a name="options"></a>Tastatur  
 **Datenverbindungen**  
 Wählen Sie aus der Liste eine vorhandene OLE DB-Datenverbindung aus.  
  
 **Datenverbindungseigenschaften**  
 Zeigt die Eigenschaften und Werte der ausgewählten OLE DB-Datenverbindung an.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **Verbindungs-Manager** eine OLE DB-Datenverbindung.  
  
 **Delete**  
 Wählen Sie eine Datenverbindung aus, und löschen Sie sie mithilfe der Schaltfläche **Löschen** .  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter    
 [OLE DB-Quelle](../../integration-services/data-flow/ole-db-source.md)     
 [OLE DB-Ziel](../../integration-services/data-flow/ole-db-destination.md)     
 [SQL ausführen (Task)](../../integration-services/control-flow/execute-sql-task.md)     
 [Integration Services-Verbindungen &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)    
    
  

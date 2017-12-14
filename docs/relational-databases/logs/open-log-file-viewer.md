---
title: "Öffnen des Protokolldatei-Viewers | Microsoft Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: logs
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Log File Viewer, opening
ms.assetid: a86b89cb-0432-4648-895a-05ecc5450e45
caps.latest.revision: "29"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 58798cfeb515819c081be5fe24261209d96f18fb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="open-log-file-viewer"></a>Öffnen des Protokolldatei-Viewers
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Sie können mithilfe des Protokolldatei-Viewers in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] auf Informationen zu Fehlern und Ereignissen zugreifen, die in folgenden Protokollen aufgezeichnet wurden:  
  
-   Überwachungsauflistung  
  
-   Datensammlung  
  
-   Datenbank-E-Mail  
  
-   Auftragsverlauf  
  
-   SQL Server  
  
-   SQL Server-Agent  
  
-   Windows-Ereignisse (auf diese Windows-Ereignisse kann auch mithilfe der Ereignisanzeige zugegriffen werden)  
  
 Ab [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]können Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Protokolldateien aus lokalen oder Remoteinstanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]mit der Option Registrierte Server anzeigen. Mit Registrierte Server können Sie die Protokolldateien unabhängig davon anzeigen, ob diese online oder offline sind. Weitere Informationen zu Onlinezugriff finden Sie weiter unten in diesem Thema in der Vorgehensweise "So zeigen Sie Onlineprotokolldateien von registrierten Servern an". Weitere Informationen über den Zugriff auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Offlineprotokolldateien finden Sie unter [Anzeigen von Offlineprotokolldateien](../../relational-databases/logs/view-offline-log-files.md).  
  
 Sie können den Protokolldatei-Viewer auf mehrere Arten öffnen, je nach anzuzeigenden Informationen.  
  
##  <a name="BeforeYouBegin"></a> Berechtigungen  
 Zum Zugreifen auf Protokolldateien für Onlineinstanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] müssen Sie Mitglied der festen Serverrolle „securityadmin“ sein.  
  
 Zum Zugreifen auf Protokolldateien für Offlineinstanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] müssen Sie über Lesezugriff für den WMI-Namespace **Root\Microsoft\SqlServer\ComputerManagement10** und den Ordner mit den Protokolldateien verfügen. Weitere Informationen finden Sie im Abschnitt „Sicherheit“ des Themas [Anzeigen von Offlineprotokolldateien](../../relational-databases/logs/view-offline-log-files.md).  
  
### <a name="security"></a>Sicherheit  
 Erfordert die Mitgliedschaft in der festen Serverrolle securityadmin.  
  
### <a name="view-log-files"></a>Anzeigen von Protokolldateien  
  
##### <a name="to-view-logs-that-are-related-to-general-sql-server-activity"></a>So zeigen Sie Protokolle zu allgemeinen SQL Server-Aktivitäten an  
  
1.  Erweitern Sie im Objekt-Explorer den Knoten **Verwaltung**.  
  
2.  Führen Sie eine der folgenden Aktionen aus:  
  
    -   Klicken Sie mit der rechten Maustaste auf **SQL Server-Protokolle**, zeigen Sie auf **Sicht**und dann entweder auf **SQL Server-Protokoll** oder **SQL Server- und Windows-Protokoll**.  
  
    -   Erweitern Sie **SQL Server-Protokolle**, klicken Sie mit der rechten Maustaste auf eine der Protokolldateien, und klicken Sie dann auf **SQL Server-Protokoll anzeigen**. Sie können auch auf jede beliebige Protokolldatei doppelklicken.  
  
     Die Protokolle sind **Datenbank-E-Mail**, **SQL Server**, **SQL Server-Agent**und **Windows NT**-Ereignisse.  
  
##### <a name="to-view-logs-that-are-related-to-jobs"></a>So zeigen Sie Protokolle zu Aufträgen an  
  
-   Erweitern Sie im Objekt-Explorer den Knoten **SQL Server-Agent**, klicken Sie mit der rechten Maustaste auf **Aufträge**, und klicken Sie dann auf **Verlauf anzeigen**.  
  
     Die Protokolle sind **Datenbank-E-Mail**, **Auftragsverlauf**und **SQL Server-Agent**.  
  
##### <a name="to-view-logs-that-are-related-to-maintenance-plans"></a>So zeigen Sie Protokolle zu Wartungsplänen an  
  
-   Erweitern Sie im Objekt-Explorer den Knoten **Verwaltung**, klicken Sie mit der rechten Maustaste auf **Wartungspläne**, und klicken Sie dann auf **Verlauf anzeigen**.  
  
     Die Protokolle sind **Datenbank-E-Mail**, **Auftragsverlauf**, **Wartungspläne**, **Remotewartungspläne**und **SQL Server-Agent**.  
  
##### <a name="to-view-logs-that-are-related-to-data-collection"></a>So zeigen Sie Protokolle zu Datensammlungen an  
  
-   Erweitern Sie im Objekt-Explorer den Knoten **Verwaltung**, klicken Sie mit der rechten Maustaste auf **Datensammlung**, und klicken Sie dann auf **Protokolle anzeigen**.  
  
     Die Protokolle sind **Datensammlung**, **Auftragsverlauf**und **SQL Server-Agent**.  
  
##### <a name="to-view-logs-that-are-related-to-database-mail"></a>So zeigen Sie Protokolle zu Datenbank-E-Mails an  
  
-   Erweitern Sie im Objekt-Explorer den Knoten **Verwaltung**, klicken Sie mit der rechten Maustaste auf **Datenbank-E-Mail**, und klicken Sie dann auf **Datenbank-E-Mail-Protokoll anzeigen**.  
  
     Die Protokolle sind **Datenbank-E-Mail, Auftragsverlauf**, **Wartungspläne**, **Remotewartungspläne**, **SQL Server**, **SQL Server-Agent**und **Windows NT**-Ereignisse.  
  
##### <a name="to-view-logs-that-are-related-to-audits-collections"></a>So zeigen Sie Protokolle zu Überwachungsauflistungen an  
  
-   Erweitern Sie im Objekt-Explorer den Knoten **Sicherheit**, erweitern Sie **Überwachungen**, klicken Sie mit der rechten Maustaste auf eine Überwachung, und klicken Sie dann auf **Überwachungsprotokolle anzeigen**.  
  
     Die Protokolle sind **Überwachungsauflistung** und **Windows NT**.  
  
##### <a name="to-view-logs-that-are-related-to-audits-collections"></a>So zeigen Sie Protokolle zu Überwachungsauflistungen an  
  
-   Erweitern Sie im Objekt-Explorer den Knoten **Sicherheit**, erweitern Sie **Überwachungen**, klicken Sie mit der rechten Maustaste auf eine Überwachung, und klicken Sie dann auf **Überwachungsprotokolle anzeigen**.  
  
     Die Protokolle sind **Überwachungsauflistung** und **Windows NT**.  
  
## <a name="see-also"></a>Siehe auch  
 [Protokolldatei-Viewer](../../relational-databases/logs/log-file-viewer.md)   
 [SQL Server Audit &#40;Datenbankmodul&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)   
 [Anzeigen von Offlineprotokolldateien](../../relational-databases/logs/view-offline-log-files.md)  
  
  

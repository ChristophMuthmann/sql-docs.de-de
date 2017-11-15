---
title: Transaktionen (Master Data Services) | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transactions [Master Data Services], about transactions
- transactions [Master Data Services]
ms.assetid: 4cd2fa6f-9c76-4b7a-ae18-d4e5fd2f03f5
caps.latest.revision: "15"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a2625fbf1a13bc3094d18417a18248547180318c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="transactions-master-data-services"></a>Transaktionen (Master Data Services)


--------------------------------------------------
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]werden Transaktionen jedes Mal aufgezeichnet, wenn für ein Element eine Aktion ausgeführt wird. Transaktionen können von allen Benutzern angezeigt und von Administratoren umgekehrt werden. Für Transaktionen werden das Datum, die Uhrzeit, der Benutzer, der die Aktion ausgeführt hat, sowie weitere Details angezeigt. Benutzer können einer Transaktion eine Anmerkung hinzufügen, um anzugeben, wieso die Transaktion stattgefunden hat.  
  
## <a name="when-transaction-are-recorded"></a>Zeitpunkt der Transaktionsaufzeichnung  
 Transaktionen werden aufgezeichnet, wenn Elemente:  
  
-   Erstellt, gelöscht oder erneut aktiviert werden  
  
-   Attributwertänderungen aufweisen  
  
-   In einer Hierarchie verschoben werden  
  
 Transaktionen werden nicht aufgezeichnet, wenn Attributwerte durch Geschäftsregeln geändert werden.  
  
## <a name="view-and-manage-transactions"></a>Anzeigen und Verwalten von Transaktionen  
 Im Funktionsbereich **Explorer** können Sie von Ihnen erstellte Transaktionen anzeigen und mit Anmerkungen versehen (ihnen Kommentare hinzufügen). 
  
 Im Funktionsbereich **Versionsverwaltung** können Administratoren alle Transaktionen für alle Benutzer für die Modelle anzeigen, auf die sie Zugriff haben, und jede beliebige Transaktion umkehren.
 
> [!NOTE]  
>  Administratoren können alle Transaktionen für alle Benutzer anzeigen, solange nicht die Berechtigungsstufe „schreibgeschützt“ im Funktionsbereich **Versionsverwaltung** festgelegt ist. Wenn z.B. die Berechtigung „schreibgeschützt“ und UPDATE-Berechtigungsebene für den Administrator festgelegt ist, kann dieser keine anderen Transaktionen anzeigen, da die Berechtigung „schreibgeschützt“ Vorrang vor der UPDATE-Berechtigung hat.
  
 Sie können konfigurieren, wie lange Transaktionsprotokolldaten beibehalten werden, indem Sie die Eigenschaft **Protokollaufbewahrung in Tagen** in den Systemeinstellungen für die [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank festlegen, und durch Festlegen der **Tage für Protokollbeibehaltung** , wenn Sie ein Modell erstellen oder bearbeiten. Weitere Informationen finden Sie unter [Systemeinstellungen &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md) und [Erstellen eines Modells &#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md).  
  
 Der SQL Server-Agent-Auftrag „MDS_MDM_Sample_Log_Maintenace“ löst die Bereinigung der Transaktionsprotokolle aus und wird jede Nacht ausgeführt. Sie können den SQL Server-Agent zum Ändern des Zeitplans für diesen Auftrag verwenden.  
  
 Sie können auch die folgenden gespeicherten Prozeduren aufrufen, um die Transaktionsprotokolle zu bereinigen.  
  
|Gespeicherte Prozedur|Description|  
|----------------------|-----------------|  
|mdm.udpTransactionsCleanup|Bereinigt den Transaktionsverlauf|  
|mdm.udpValidationsCleanup|Bereinigt den Überprüfungsverlauf|  
|mdm.udpEntityStagingBatchTableCleanup|Bereinigt die Stagingtabelle|  
  
 **Beispiel**  
  
```  
DECLARE @CleanupOlderThanDate date = '2014-11-11',  
@ModelID INT = 7  
--Clean up Transaction Logs  
EXEC mdm.udpTransactionsCleanup @ModelID, @CleanupOlderThanDate;  
  
--Clean up Validation History  
EXEC mdm.udpValidationsCleanup @ModelID, @CleanupOlderThanDate;  
  
--Clean up EBS tables  
EXEC mdm.udpEntityStagingBatchTableCleanup @ModelID, @CleanupOlderThanDate;  
  
```  
  
## <a name="system-settings"></a>Systemeinstellungen  
 Im [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] ist eine Einstellung verfügbar, die beeinflusst, ob Transaktionen beim Bereitstellen von Datensätzen aufgezeichnet werden. Sie können diese Einstellung in [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] oder direkt in der Tabelle „Systemeinstellungen“ der [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]-Datenbank anpassen. Weitere Informationen finden Sie unter [Systemeinstellungen &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md).  
  
 Wenn Sie Daten in diese Version von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] importieren, können Sie angeben, ob Transaktionen beim Initiieren der gespeicherten Prozedur protokolliert werden. Weitere Informationen finden Sie unter [Gespeicherte Stagingprozedur &#40;Master Data Services&#41;](../master-data-services/staging-stored-procedure-master-data-services.md).  
  
## <a name="concurrency"></a>Parallelität  
 Wenn ein bestimmter Entitätswert gleichzeitig in mehr als einer Explorersitzung angezeigt wird, sind gleichzeitige Bearbeitungen zum gleichen Wert möglich. Gleichzeitige Bearbeitungen werden nicht automatisch von MDS erkannt. Dies kann auftreten, wenn mehrere Benutzer den MDS-Explorer im Webbrowser von mehreren Sitzungen, z. B. von mehreren Computern, mehreren Browserregisterkarten oder Fenstern oder mehreren Benutzerkonten, verwenden.  
  
 Mehr als ein Benutzer kann trotz Transaktionen, die aktiviert werden, die gleichen Entitätswerte ohne Fehler aktualisieren. In der Regel hat die letzte Bearbeitung zum Wert in einer Sequenz der Zeit Vorrang. Der doppelte Bearbeitungskonflikt kann im Transaktionsverlauf manuell beachtet werden und vom Administrator manuell umgekehrt werden. Der Transaktionsverlauf zeigt die einzelnen Transaktionen für den **vorherigen Wert** und den **neuen Wert** für das fragliche Attribut aus jeder Sitzung an, löst aber den Konflikt nicht automatisch, wenn mehrere **neue Werte** für den gleichen alten Wert vorhanden sind.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Aktion durch Umkehren einer Transaktion rückgängig machen (nur Administratoren).|[Umkehren einer Transaktion &#40;Master Data Services&#41;](../master-data-services/reverse-a-transaction-master-data-services.md)|  
  
## <a name="external-resources"></a>Externe Ressourcen  
 Blogbeitrag [Transactions, Validation Issue and Staging table cleanup](http://go.microsoft.com/fwlink/p/?LinkId=615374)(Transaktionen, Überprüfungsprobleme und Bereinigung der Stagingtabelle) auf msdn.com.  
  
## <a name="related-content"></a>Verwandte Inhalte  
  
-   [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)  
  
-   [Anmerkungen &#40;Master Data Services&#41;](../master-data-services/annotations-master-data-services.md)  
  
  

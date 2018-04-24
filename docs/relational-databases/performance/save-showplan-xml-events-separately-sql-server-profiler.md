---
title: Separates Speichern von Showplan XML-Ereignissen (SQL Server Profiler) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: performance
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Showplan XML events
- saving Showplan XML events
- events [SQL Server], Showplan XML
ms.assetid: 33320a7a-36e8-401c-876d-5b82c49abd85
caps.latest.revision: 25
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3e0ff27705828cc5a4175aad63986cc6139a7e25
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="save-showplan-xml-events-separately-sql-server-profiler"></a>Separates Speichern von Showplan XML-Ereignissen (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In diesem Thema wird beschrieben, wie **Showplan XML** -Ereignisse, die in Ablaufverfolgungen erfasst sind, mithilfe von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]in separaten .SQLPlan-Dateien gespeichert werden können. Sie können die **Showplan XML**-Ereignisdateien in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] öffnen, um den grafischen Ausführungsplan für jedes Ereignis anzuzeigen.  
  
## <a name="save-showplan-xml-events-separately"></a>Separates Speichern von Showplan XML-Ereignissen  
  
1. Wählen Sie im Menü **Datei** die Option **Neue Ablaufverfolgung** aus, und stellen Sie dann eine Verbindung mit einer Instanz von SQL Server her.  
  
     Das Dialogfeld **Ablaufverfolgungseigenschaften** wird angezeigt.  
  
    > [!NOTE]  
    >  Wenn Sie **Ablaufverfolgung sofort nach dem Herstellen der Verbindung starten** auswählen, wird das Dialogfeld **Ablaufverfolgungseigenschaften** nicht angezeigt. Stattdessen beginnt die Ablaufverfolgung. Um diese Einstellung zu deaktivieren, wählen Sie im Menü **Extras** **Optionen** aus und deaktivieren das Kontrollkästchen **Ablaufverfolgung sofort nach dem Herstellen der Verbindung starten**.  
  
2. Geben Sie im Dialogfeld **Ablaufverfolgungseigenschaften** im Feld **Ablaufverfolgungsname** einen Namen für die Ablaufverfolgung ein.  
  
3. Wählen Sie in der Liste **Vorlage verwenden** eine Nachverfolgungsvorlage aus, auf der die Nachverfolgung basieren soll. Wenn Sie keine Vorlage verwenden möchten, wählen Sie **Leer** aus.  
  
4. Führen Sie eines der folgenden Verfahren aus:  
  
    -   Aktivieren Sie das Kontrollkästchen **In Datei speichern**, um die Ablaufverfolgung in einer Datei aufzuzeichnen. Geben Sie einen Wert für **Maximale Dateigröße festlegen**an. 
    
        Optional aktivieren Sie die Kontrollkästchen **Dateirollover aktivieren** und **Ablaufverfolgungsdaten von Serverprozessen** .  
  
    -   Aktivieren Sie das Kontrollkästchen **In Tabelle speichern**, um die Ablaufverfolgung in einer Datenbanktabelle aufzuzeichnen. 
    
        Wählen Sie optional **Maximale Zeilenzahl festlegen** aus, und geben Sie einen Wert an.  
  
5. Aktivieren Sie optional das Kontrollkästchen **Beendigungszeit für Ablaufverfolgung aktivieren** , und geben Sie das Datum und die Uhrzeit zum Beenden der Ablaufverfolgung an. 
  
6. Wählen Sie die Registerkarte **Ereignisauswahl** aus.  
  
7. Erweitern Sie in der Datenspalte **Ereignisse** die Ereigniskategorie **Leistung**, und aktivieren Sie dann das Kontrollkästchen **Showplan XML**. Wenn die **Performance**-Ereigniskategorie nicht verfügbar ist, wählen Sie **Alle Ereignisse anzeigen** aus, um sie anzuzeigen.  
  
     Die Registerkarte **Ereignisextraktionseinstellungen** wird dem Dialogfeld **Ablaufverfolgungseigenschaften** hinzugefügt.  
  
8. Wählen Sie auf der Registerkarte **Ereignisextraktionseinstellungen** die Option **XML-Showplanereignisse separat speichern** aus.  
  
9. Geben Sie in das Dialogfeld **Speichern unter** den Namen der Datei ein, in die die **Showplan XML** -Ereignisse gespeichert werden sollen.  
  
10. Wählen Sie **Alle XML-Showplanbatches in einer einzelnen Datei** aus, um alle **Showplan XML**-Ereignisse in einer einzelnen XML-Datei zu speichern. Wählen Sie alternativ **Jeder XML-Showplanbatch in einer eigenen Datei** aus, um für jedes **Showplan XML**-Ereignis eine neue XML-Datei zu erstellen.  
  
11. Um die **Showplan XML**-Ereignisdatei in SQL Server Management Studio anzeigen zu lassen, zeigen Sie im Menü **Datei** auf **Öffnen**, und wählen Sie **Datei** aus. Navigieren Sie zu dem Verzeichnis, in dem Sie die **Showplan XML**-Ereignisdatei(en) gespeichert hatten, wählen Sie eine Datei aus, und öffnen Sie diese. **Showplan XML** -Ereignisdateien besitzen die Dateierweiterung .SQLPlan.  
  
## <a name="see-also"></a>Siehe auch  
 [Analysieren von Abfragen mit Showplan-Ergebnissen in SQL Server Profiler](../../tools/sql-server-profiler/analyze-queries-with-showplan-results-in-sql-server-profiler.md)  
  
  

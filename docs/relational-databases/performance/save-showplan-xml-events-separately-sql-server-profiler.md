---
title: Separates Speichern von Showplan XML-Ereignissen (SQL Server Profiler) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Showplan XML events
- saving Showplan XML events
- events [SQL Server], Showplan XML
ms.assetid: 33320a7a-36e8-401c-876d-5b82c49abd85
caps.latest.revision: 25
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e92884b770e55cbd1b34203d7979041ee3821159
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="save-showplan-xml-events-separately-sql-server-profiler"></a>Separates Speichern von Showplan XML-Ereignissen (SQL Server Profiler)
  In diesem Thema wird beschrieben, wie **Showplan XML** -Ereignisse, die in Ablaufverfolgungen erfasst sind, mithilfe von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]in separaten .SQLPlan-Dateien gespeichert werden können. Sie können die **Showplan XML** -Ereignisdateien in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]öffnen, sodass Sie den grafischen Ausführungsplan für die einzelnen Ereignisse betrachten können.  
  
### <a name="to-save-showplan-xml-events-separately"></a>So speichern Sie Showplan XML-Ereignisse separat  
  
1.  Klicken Sie im Menü **Datei** auf **Neue Ablaufverfolgung**, und stellen Sie dann eine Verbindung zu einer Instanz von SQL Server her.  
  
     Das Dialogfeld **Ablaufverfolgungseigenschaften**wird angezeigt.  
  
    > [!NOTE]  
    >  Bei der Auswahl von **Ablaufverfolgung sofort nach dem Herstellen der Verbindung starten**wird das Dialogfeld **Ablaufverfolgungseigenschaften**nicht angezeigt. Stattdessen beginnt die Ablaufverfolgung. Um diese Einstellung zu deaktivieren, klicken Sie im Menü **Extras**auf **Optionen**, und deaktivieren Sie das Kontrollkästchen **Ablaufverfolgung sofort nach dem Herstellen der Verbindung starten** .  
  
2.  Geben Sie im Dialogfeld **Ablaufverfolgungseigenschaften** im Feld **Ablaufverfolgungsname** einen Namen für die Ablaufverfolgung ein.  
  
3.  Wählen Sie in der Liste **Vorlage verwenden** eine Ablaufverfolgungsvorlage als Basis für die Ablaufverfolgung aus, oder wählen Sie **Leer** aus, wenn Sie keine Vorlage verwenden möchten.  
  
4.  Führen Sie eines der folgenden Verfahren aus:  
  
    -   Aktivieren Sie das Kontrollkästchen**In Datei speichern** , um die Ablaufverfolgung in einer Datei aufzuzeichnen. Geben Sie einen Wert für **Maximale Dateigröße festlegen**an. Optional aktivieren Sie die Kontrollkästchen **Dateirollover aktivieren** und **Ablaufverfolgungsdaten von Serverprozessen** .  
  
    -   Aktivieren Sie das Kontrollkästchen**In Tabelle speichern** , um die Ablaufverfolgung in einer Datenbanktabelle aufzuzeichnen. Klicken Sie optional auf **Maximale Zeilenzahl festlegen**, und geben Sie einen Wert an.  
  
5.  Aktivieren Sie optional das Kontrollkästchen **Beendigungszeit für Ablaufverfolgung aktivieren** , und geben Sie das Datum und die Uhrzeit zum Beenden der Ablaufverfolgung an.  
  
6.  Klicken Sie auf die Registerkarte **Ereignisauswahl**.  
  
7.  Geben Sie im Dialogfeld **Ereignisse**die Ereigniskategorie **Leistung**, und aktivieren Sie dann das Kontrollkästchen **Showplan XML**. Wenn die **Performance** -Ereigniskategorie nicht verfügbar ist, aktivieren Sie zum Anzeigen dieser Ereigniskategorie das Kontrollkästchen **Alle Ereignisse anzeigen** .  
  
     Das Dialogfeld **Ereignisextraktionseinstellungen**wird dem Dialogfeld **Ablaufverfolgungseigenschaften**hinzugefügt.  
  
8.  Klicken Sie im Menü **Ereignisextraktionseinstellungen**auf **XML-Showplanereignisse separat speichern**.  
  
9. Geben Sie in das Dialogfeld **Speichern unter** den Namen der Datei ein, in die die **Showplan XML** -Ereignisse gespeichert werden sollen.  
  
10. Klicken Sie auf **Alle XML-Showplanbatches in einer einzelnen Datei** , wenn alle **Showplan XML** -Ereignisse in einer einzigen XML-Datei gespeichert werden sollen, bzw. auf **Jeder XML-Showplanbatch in einer eigenen Datei**, um so je eine neue XML-Datei für die einzelnen **Showplan XML** -Ereignisse anlegen zu lassen.  
  
11. Um die **Showplan XML** -Ereignisdatei in SQL Server Management Studio anzeigen zu lassen, zeigen Sie im Menü **Datei** auf **Öffnen**, und klicken Sie auf **Datei**. Navigieren Sie zu dem Verzeichnis, in dem Sie die **Showplan XML** -Ereignisdatei(en) gespeichert hatten, wählen Sie eine Datei aus, und öffnen Sie diese. **Showplan XML** -Ereignisdateien besitzen die Dateierweiterung .SQLPlan.  
  
## <a name="see-also"></a>Siehe auch  
 [Analysieren von Abfragen mit SHOWPLAN-Ergebnissen in SQL Server Profiler](../../tools/sql-server-profiler/analyze-queries-with-showplan-results-in-sql-server-profiler.md)  
  
  

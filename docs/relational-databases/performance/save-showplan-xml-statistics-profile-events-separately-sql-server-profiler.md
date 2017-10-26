---
title: Separates Speichern eines Showplan XML Statistics Profile-Ereignisses (SQL Server Profiler) | Microsoft-Dokumentation
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
- Showplan XML events
- saving Showplan XML events
- events [SQL Server], Showplan XML
ms.assetid: df393f13-d538-4d94-8155-9c2fdf5f755d
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1f079c68f7f54569dee1a6d9f2e9fa61f1893426
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="save-showplan-xml-statistics-profile-events-separately-sql-server-profiler"></a>Separates Speichern eines Showplan XML Statistics Profile-Ereignisses (SQL Server Profiler)
  In diesem Thema wird beschrieben, wie Sie in Ablaufverfolgungen aufgezeichnete **Showplan XML Statistics Profile** -Ereignisse mithilfe von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]in separaten SQLPLAN-Dateien speichern. Sie können die **Showplan XML Statistics Profile** -Ereignisdateien in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]öffnen, um den grafischen Ausführungsplan für jedes Ereignis anzuzeigen.  
  
### <a name="to-save-showplan-xml-statistics-events-separately"></a>So speichern Sie Showplan XML Statistics-Ereignisse separat  
  
1.  Klicken Sie im Menü **Datei** auf **Neue Ablaufverfolgung**, und stellen Sie dann eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]her.  
  
     Das Dialogfeld **Ablaufverfolgungseigenschaften** wird angezeigt.  
  
    > [!NOTE]  
    >  Bei der Auswahl von **Ablaufverfolgung sofort nach dem Herstellen der Verbindung starten**wird das Dialogfeld **Ablaufverfolgungseigenschaften**nicht angezeigt. Stattdessen beginnt die Ablaufverfolgung. Um diese Einstellung zu deaktivieren, klicken Sie im Menü **Extras**auf **Optionen**, und deaktivieren Sie das Kontrollkästchen **Ablaufverfolgung sofort nach dem Herstellen der Verbindung starten** .  
  
2.  Geben Sie im Dialogfeld **Ablaufverfolgungseigenschaften** im Feld **Ablaufverfolgungsname** einen Namen für die Ablaufverfolgung ein.  
  
3.  Wählen Sie in der Liste **Vorlage verwenden** eine Ablaufverfolgungsvorlage für die Ablaufverfolgung aus, oder wählen Sie **Leer** aus, wenn Sie keine Vorlage verwenden möchten.  
  
4.  Führen Sie eines der folgenden Verfahren aus:  
  
    -   Klicken Sie auf**In Datei speichern**, um die Ablaufverfolgung in einer Datei zu erfassen. Geben Sie einen Wert für **Maximale Dateigröße festlegen**an.  
  
         Aktivieren Sie optional die Kontrollkästchen **Dateirollover aktivieren** und **Ablaufverfolgungsdaten von Serverprozessen**.  
  
    -   Klicken Sie auf**In Tabelle speichern** , um die Ablaufverfolgung in einer Datenbanktabelle zu erfassen.  
  
         Klicken Sie optional auf **Maximale Zeilenzahl festlegen**, und geben Sie einen Wert an.  
  
5.  Aktivieren Sie optional das Kontrollkästchen **Beendigungszeit für Ablaufverfolgung aktivieren** , um das Datum und die Uhrzeit zum Beenden der Ablaufverfolgung anzugeben.  
  
6.  Klicken Sie auf die Registerkarte **Ereignisauswahl**.  
  
7.  Erweitern Sie in der **Events**-Datenspalte die **Performance**-Ereigniskategorie, und aktivieren Sie dann das Kontrollkästchen **Showplan XML Statistics Profile**. Wenn die **Performance** -Ereigniskategorie nicht verfügbar ist, aktivieren Sie zum Anzeigen dieser Ereigniskategorie das Kontrollkästchen **Alle Ereignisse anzeigen** .  
  
     Das Dialogfeld **Ereignisextraktionseinstellungen**wird dem Dialogfeld **Ablaufverfolgungseigenschaften**hinzugefügt.  
  
8.  Klicken Sie im Menü **Ereignisextraktionseinstellungen**auf **XML-Showplanereignisse separat speichern**.  
  
9. Geben Sie im Dialogfeld **Speichern unter** den Dateinamen zum Speichern der **Showplan XML Statistics Profile** -Ereignisse ein.  
  
10. Klicken Sie auf **Alle XML-Showplanbatches in einer einzelnen Datei** , um alle **Showplan XML Statistics Profile** -Ereignisse in einer einzelnen XML-Datei zu speichern. Klicken Sie optional auf **Jeder XML-Showplanbatch in einer eigenen Datei**, um für jedes **Showplan XML Statistics Profile** -Ereignis eine neue XML-Datei zu erstellen.  
  
11. Zum Anzeigen der **Showplan XML Statistics Profile** -Ereignisdatei in SQL Server Management Studio zeigen Sie im Menü **Datei** auf **Öffnen**, und klicken Sie auf **Datei**. Navigieren Sie zu dem Verzeichnis, in Sie die **Showplan XML Statistics Profile** -Ereignisdatei(en) gespeichert haben, um eine Ereignisdatei auszuwählen und zu öffnen. **Showplan XML Statistics Profile** -Ereignisdateien haben eine SQLPlan-Dateinamenerweiterung.  
  
## <a name="see-also"></a>Siehe auch  
 [Analysieren von Abfragen mit SHOWPLAN-Ergebnissen in SQL Server Profiler](../../tools/sql-server-profiler/analyze-queries-with-showplan-results-in-sql-server-profiler.md)  
  
  


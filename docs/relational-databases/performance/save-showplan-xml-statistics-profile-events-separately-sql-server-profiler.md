---
title: Separates Speichern eines Showplan XML Statistics Profile-Ereignisses (SQL Server Profiler) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Showplan XML events
- saving Showplan XML events
- events [SQL Server], Showplan XML
ms.assetid: df393f13-d538-4d94-8155-9c2fdf5f755d
caps.latest.revision: "20"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c54c389d97e750b42d782314f01ec2cb5bedd352
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="save-showplan-xml-statistics-profile-events-separately-sql-server-profiler"></a>Separates Speichern eines Showplan XML Statistics Profile-Ereignisses (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema wird beschrieben, wie Sie in Ablaufverfolgungen aufgezeichnete **Showplan XML Statistics Profile**-Ereignisse mithilfe von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] in separaten SQLPLAN-Dateien speichern. Sie können die **Showplan XML Statistics Profile**-Ereignisdateien in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]öffnen, um den grafischen Ausführungsplan für jedes Ereignis anzuzeigen.  
  
## <a name="save-showplan-xml-statistics-profile-events-separately"></a>Separates Speichern der „Showplan XML Statistics“-Ereignisse  
  
1. Wählen Sie im Menü **Datei** die Option **Neue Ablaufverfolgung** aus, und stellen Sie dann eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] her.  
  
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
  
7. Erweitern Sie in der **Events**-Datenspalte die **Performance**-Ereigniskategorie, und aktivieren Sie dann das Kontrollkästchen **Showplan XML Statistics Profile**. Wenn die **Performance**-Ereigniskategorie nicht verfügbar ist, wählen Sie **Alle Ereignisse anzeigen** aus, um sie anzuzeigen.  
  
     Die Registerkarte **Ereignisextraktionseinstellungen** wird dem Dialogfeld **Ablaufverfolgungseigenschaften** hinzugefügt.  
  
8. Wählen Sie auf der Registerkarte **Ereignisextraktionseinstellungen** die Option **XML-Showplanereignisse separat speichern** aus.  
  
9. Geben Sie im Dialogfeld **Speichern unter** den Dateinamen zum Speichern der **Showplan XML Statistics Profile** -Ereignisse ein.  
  
10. Wählen Sie **Alle Batches in einer einzelnen Datei** aus, um alle **Showplan XML Statistics Profile**-Ereignisse in einer einzelnen XML-Datei zu speichern. Wählen Sie alternativ **Jeder XML-Showplanbatch in einer eigenen Datei** aus, um für jedes **Showplan XML Statistics Profile**-Ereignis eine neue XML-Datei zu erstellen.  
  
11. Zum Anzeigen der **Showplan XML Statistics Profile**-Ereignisdatei in SQL Server Management Studio zeigen Sie im Menü **Datei** auf **Öffnen** und wählen **Datei** aus. Navigieren Sie zu dem Verzeichnis, wo Sie die **Showplan XML Statistics Profile**-Ereignisdatei(en) gespeichert haben, um eine Ereignisdatei auszuwählen und zu öffnen. **Showplan XML Statistics Profile** -Ereignisdateien haben eine SQLPlan-Dateinamenerweiterung.  
  
## <a name="see-also"></a>Siehe auch  
 [Analysieren von Abfragen mit Showplan-Ergebnissen in SQL Server Profiler](../../tools/sql-server-profiler/analyze-queries-with-showplan-results-in-sql-server-profiler.md)  
  
  

---
title: Anzeigen von Optimierungsberichten | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-query-tuning
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- tuning reports [SQL Server]
ms.assetid: daee6143-269f-428b-8458-9a3e726d586c
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a395ca1faceb1465c1ce7dc8fc43215dae31c8be
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="lesson-1-3---viewing-tuning-reports"></a>Lektion 1 bis 3 - Optimierungsberichte anzeigen
In der vorigen Übung dieser Lektion haben Sie die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Skripts angezeigt, mit denen Datenbankobjekte in den Empfehlungen des Datenbankoptimierungsratgebers erstellt oder gelöscht werden, die als Ergebnis der Optimierungssitzung „MySession“ generiert wurden. Die Optimierungssitzung MySession wurde in [Optimieren einer Arbeitsauslastung](../../tools/dta/lesson-1-1-tuning-a-workload.md)angelegt.  
  
Es kann sehr nützlich sein, die Skripts anzuzeigen, die zum Implementieren der Optimierungsergebnisse verwendet werden können. Daneben bietet der Datenbankmodul-Optimierungsratgeber jedoch noch viele weitere nützliche Berichte, die Sie ebenfalls anzeigen können. Diese Berichte umfassen Informationen zu den vorhandenen physischen Entwurfsstrukturen in der zu optimierenden Datenbank sowie über die empfohlenen Strukturen. Zum Anzeigen der Optimierungsberichte klicken Sie auf die Registerkarte **Berichte** , wie in der folgenden Übung beschrieben. In dieser Übung werden die Optimierungssitzungen MySession und EvaluateMySession verwendet, die Sie in [Optimieren einer Arbeitsauslastung](../../tools/dta/lesson-1-1-tuning-a-workload.md) und in [Anzeigen von Empfehlungen für die Optimierung](../../tools/dta/lesson-1-2-viewing-tuning-recommendations.md)angelegt haben.  
  
### <a name="view-tuning-reports"></a>Anzeigen von Optimierungsberichten  
  
1.  Starten Sie den Datenbankoptimierungsratgeber. Weitere Informationen finden Sie unter [Starten des Datenbankoptimierungsratgebers](../../tools/dta/lesson-1-1-launching-database-engine-tuning-advisor.md). Stellen Sie sicher, dass Sie eine Verbindung mit derselben [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz herstellen, die Sie in den früheren Übungen dieser Lektion verwendet haben.  
  
    Doppelklicken Sie im Bereich **Sitzungsmonitor** auf **MySession** . Der Datenbankoptimierungsratgeber lädt die Sitzungsinformationen dieser Sitzung.  
  
2.  Klicken Sie auf die Registerkarte **Berichte** .  
  
3.  Im Bereich **Optimierungszusammenfassung** können Sie Informationen zu dieser Optimierungssitzung anzeigen. Verwenden Sie die Bildlaufleiste, um den gesamten Inhalt des Bereichs anzuzeigen. Beachten Sie die Felder **Prozentsatz für die erwartete Verbesserung** und **Von der Empfehlung verwendeter Speicherplatz (MB)**. Beim Festlegen der Optionen für die Optimierung kann der Platz eingeschränkt werden, der den Empfehlungen zur Verfügung steht. Wählen Sie auf der Registerkarte **Optimierungsoptionen** die Option **Erweiterte Optionen**aus. Aktivieren Sie **Max. Speicherplatz für Empfehlungen definieren (MB)** und geben Sie den maximal zulässigen Speicherplatz für eine empfohlene Konfiguration in Megabytes ein. Mit der Schaltfläche **Zurück** kehren Sie vom Browser der Hilfe zu diesem Tutorial zurück.  
  
4.  Klicken Sie im Bereich **Optimierungsberichte** in der Liste **Bericht auswählen** auf **Anweisungskostenbericht** . Wenn Sie für die Anzeige des Berichts mehr Platz brauchen, ziehen Sie den Rand des Bereichs **Sitzungsmonitor** nach links. Mit jeder [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung, die für eine Tabelle in Ihrer Datenbank ausgeführt wird, sind Leistungskosten verknüpft. Diese Leistungskosten können reduziert werden, indem für Spalten in einer Tabelle, auf die häufig zugegriffen wird, effektive Indizes erstellt werden. Dieser Bericht zeigt, wie hoch die geschätzte Verbesserung in Prozent ist, die bei einer Implementierung der Optimierungsempfehlungen erreicht werden kann, im Vergleich zu den ursprünglichen Kosten bei Ausführen der Anweisung in der Arbeitsauslastung. Beachten Sie, dass die Menge der im Bericht enthaltenen Informationen von der Länge und Komplexität der Arbeitsauslastung abhängt.  
  
5.  Klicken Sie mit der rechten Maustaste im Raster auf den Bereich **Anweisungskostenbericht** und anschließend auf **In Datei exportieren**. Speichern Sie den Bericht unter dem Namen **MyReport**. Dem Dateinamen wird automatisch die Erweiterung .xml angehängt. Sie können die Datei MyReport.xml in Ihrem bevorzugten XML-Editor oder in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] öffnen, um den Inhalt des Berichts anzuzeigen.  
  
6.  Kehren Sie zur Registerkarte **Berichte** des Datenbankoptimierungsratgebers zurück, und klicken Sie anschließend noch einmal mit der rechten Maustaste auf **Anweisungskostenbericht** . Überprüfen Sie die weiteren Optionen, die zur Verfügung stehen. Beachten Sie, dass Sie die Schriftart des Berichts, den Sie anzeigen, ändern können. Wenn Sie die Schriftart hier ändern, wird sie auch auf den anderen Seiten im Registerformat geändert.  
  
7.  Klicken Sie auf weitere Berichte in der Liste **Bericht auswählen** , um sich mit diesen vertraut zu machen.  
  
## <a name="summary"></a>Zusammenfassung  
Sie haben jetzt die Registerkarte **Berichte** der Benutzeroberfläche des Datenbankoptimierungsratgebers für die Optimierungssitzung MySession kennen gelernt. Die gleichen Schritte können Sie ausführen, um die Berichte zu prüfen, die für die Optimierungssitzung EvaluateMySession erstellt wurden. Doppelklicken Sie dazu im Bereich **Sitzungsmonitor** auf **EvaluateMySession** .  
  
## <a name="next-lesson"></a>Nächste Lektion  
[Lektion 3: Verwenden des Befehlszeilenprogramms dta](../../tools/dta/lesson-3-using-the-dta-command-prompt-utility.md)  
  
  
  


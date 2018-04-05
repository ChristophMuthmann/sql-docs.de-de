---
title: Anzeigen von Optimierungsempfehlungen | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: dta
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-query-tuning
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- Database Engine [SQL Server], tutorials
ms.assetid: e4e690c9-434f-4b01-b4de-0b905323ddd6
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 634534fb9fa7f97e61431a481ab847bd87e2806a
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="lesson-1-2---viewing-tuning-recommendations"></a>Lektion 1-2 - Anzeige von Optimierungsempfehlungen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Dieser Task verwendet die optimierungssitzung an, die Sie in erstellt [Optimieren einer Arbeitsauslastung](../../tools/dta/lesson-1-1-tuning-a-workload.md). Wenn Sie die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank mit dem Skript MyScript.sql [!INCLUDE[tsql](../../includes/tsql-md.md)] optimiert haben, werden die Ergebnisse des [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgebers auf der Registerkarte **Empfehlungen** angezeigt. In der folgenden Aufgabe erhalten Sie eine Einführung zur Registerkarte **Empfehlungen** auf der grafischen Benutzeroberfläche (graphical user interface, GUI) des [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgebers. Außerdem können Sie die Informationen prüfen, die als Ergebnisse der Optimierungssitzung zur Verfügung gestellt werden.  
  
### <a name="view-tuning-recommendations"></a>Optimierungsempfehlungen anzeigen  
  
1.  Starten Sie den [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgeber. Weitere Informationen finden Sie unter [Starten des Datenbankoptimierungsratgebers](../../tools/dta/lesson-1-1-launching-database-engine-tuning-advisor.md). Stellen Sie sicher, dass Sie eine Verbindung mit derselben [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz herstellen, die Sie in der Übung [Optimieren einer Arbeitsauslastung](../../tools/dta/lesson-1-1-tuning-a-workload.md)verwendet haben.  
  
2.  Doppelklicken Sie im Bereich **Sitzungsmonitor** auf **MySession** . [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Optimierungsratgeber lädt die Sitzungsinformationen aus Ihrer früheren optimierungssitzung und zeigt die **Empfehlungen** Registerkarte. Der [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgeber gibt jedoch keine **Partitionsempfehlungen** , da Sie alle Standardeinstellungen für die Optimierung übernommen haben und auf der Registerkarte **Optimierungsoptionen** die Option **Keine Partitionierung** ausgewählt wurde.  
  
3.  Verwenden Sie auf der Registerkarte **Empfehlungen** die Bildlaufleiste unten auf der Seite im Registerformat, um alle Spalten zu **Indexempfehlungen** anzuzeigen. Jede Zeile steht für ein Datenbankobjekt (Indizes oder indizierte Sichten), für das der [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgeber die Empfehlung abgibt, es zu löschen oder anzulegen. Führen Sie einen Bildlauf zur Spalte ganz rechts durch, und klicken Sie auf **Definition**. [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Optimierungsratgeber zeigt eine **SQL-Skriptvorschau** Fenster, in dem Sie anzeigen können, den [!INCLUDE[tsql](../../includes/tsql-md.md)] Skript, das erstellt oder löscht das Datenbankobjekt in dieser Zeile. Klicken Sie auf **Schließen** , um das Vorschaufenster zu schließen.  
  
    Wenn Sie Probleme haben, eine **Definition** zu finden, die einen Link enthält, klicken Sie am unteren Rand der Seite im Registerformat auf das Kontrollkästchen **Vorhandene Objekte anzeigen** , um es zu deaktivieren. Damit wird die Anzahl dargestellter Zeilen reduziert. Wenn Sie das Kontrollkästchen deaktivieren, zeigt der [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgeber nur die Objekte an, für die eine Empfehlung generiert wurde. Aktivieren Sie das Kontrollkästchen **Vorhandene Objekte anzeigen** , um alle Datenbankobjekte anzuzeigen, die derzeit in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank vorhanden sind. Zum Anzeigen aller Objekte verwenden Sie die Bildlaufleiste rechts auf der Seite im Registerformat.  
  
4.  Klicken Sie mit der rechten Maustaste auf das Raster im Bereich **Indexempfehlungen** . Im daraufhin angezeigten Kontextmenü können Sie Empfehlungen auswählen oder deren Auswahl aufheben. Außerdem können Sie die Schriftart des Rastertexts ändern.  
  
5.  Klicken Sie im Menü **Aktionen** auf **Empfehlungen speichern** , um alle Empfehlungen in einem [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skript zu speichern. Weisen Sie dem Skript den Namen **MySessionRecommendations.sql**zu.  
  
    Öffnen Sie das Skript MySessionRecommendations.sql im Abfrage-Editor von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , um es anzuzeigen. Sie könnten jetzt die Empfehlungen auf die Beispieldatenbank [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] anwenden, indem Sie das Skript im Abfrage-Editor ausführen, aber tun Sie das jetzt nicht. Schließen Sie das Skript im Abfrage-Editor, ohne es auszuführen.  
  
    Optional können Sie die Empfehlungen auch anwenden, indem Sie im Menü **Aktionen** des **-Optimierungsratgebers auf** Empfehlungen anwenden [!INCLUDE[ssDE](../../includes/ssde-md.md)] klicken. Wenden Sie jedoch die Empfehlungen an dieser Stelle in der Übung nicht an.  
  
6.  Wenn auf der Registerkarte **Empfehlungen** mehrere Empfehlungen vorhanden sind, deaktivieren Sie einige der Zeilen, in denen Datenbankobjekte im Raster **Indexempfehlungen** aufgelistet sind.  
  
7.  Klicken Sie im Menü **Aktionen** auf **Empfehlungen bewerten**. [!INCLUDE[ssDE](../../includes/ssde-md.md)] Der Optimierungsratgeber erstellt eine neue Optimierungssitzung, in der Sie eine Untergruppe der ursprünglichen Empfehlungen aus MySession auswerten können.  
  
8.  Geben Sie als Namen für die neue Sitzung im Feld **Sitzungsname** den Wert **EvaluateMySession**ein, und klicken Sie auf der Symbolleiste auf die Schaltfläche **Analyse starten** . Zum Anzeigen der Ergebnisse dieser neuen Optimierungssitzung können Sie die Schritte 2 und 3 wiederholen.  
  
## <a name="summary"></a>Zusammenfassung  
Sie haben den Inhalt der Registerkarte **Empfehlungen** für die Optimierungssitzung MySession angezeigt und eine Untergruppe der Empfehlungen in der neuen Optimierungssitzung EvaluateMySession ausgewertet.  
  
Das Auswerten einer Untergruppe von Optimierungsempfehlungen kann erforderlich sein, wenn Sie feststellen, dass Sie nach dem Ausführen einer Sitzung die Optimierungsoptionen noch ändern müssen. Beispiel: Sie legen im [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgeber in den Optimierungsoptionen für eine Sitzung fest, dass indizierte Sichten berücksichtigt werden sollen. Nachdem die Empfehlung erstellt wurde, beschließen Sie jedoch, indizierte Sichten nicht zu berücksichtigen. Sie können anschließend im Menü **Aktionen** den **-Optimierungsratgeber mithilfe der Option** Empfehlungen bewerten [!INCLUDE[ssDE](../../includes/ssde-md.md)] anweisen, die Sitzung neu zu bewerten, ohne dabei indizierte Sichten zu berücksichtigen. Wenn Sie die Option **Empfehlungen auswerten** verwenden, werden für die zweite Optimierungssitzung die vorher generierten Empfehlungen hypothetisch auf den aktuellen physischen Entwurf angewendet, um den physischen Entwurf für die zweite Optimierungssitzung zu erstellen.  
  
Auf der Registerkarte **Berichte** können Sie weitere Ergebnisse der Optimierung anzeigen. Darauf wird in der nächsten Aufgabe dieser Lektion näher eingegangen.  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in der Lektion  
[Anzeigen von Optimierungsberichten](../../tools/dta/lesson-1-3-viewing-tuning-reports.md)  
  
  
  

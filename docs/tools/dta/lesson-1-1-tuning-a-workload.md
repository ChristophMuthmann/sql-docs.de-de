---
title: Optimieren einer Arbeitsauslastung | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
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
- workloads [SQL Server], tuning
ms.assetid: 6229bf3f-1182-4bc6-8451-cedc37f4b62e
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 6acb93ddde56546e170b01c093dff843a2ea5968
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="lesson-1-1---tuning-a-workload"></a>Lektion 1: 1-Optimieren einer Arbeitsauslastung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Der Datenbankmodul-Optimierungsratgeber kann verwendet werden, finden Sie die besten physischen Datenbankentwurf für die abfrageleistung für die Datenbanken und Tabellen, die Sie für die Optimierung auswählen.  
  
In dieser Aufgabe wird die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Beispieldatenbank verwendet. Aus Sicherheitsgründen werden die Beispieldatenbanken standardmäßig nicht installiert. Informationen zur Installation der Beispieldatenbanken finden Sie unter [Installieren der SQL Server-Beispiele und -Beispieldatenbanken](http://sqlserversamples.codeplex.com).  
  
### <a name="tune-a-workload-transact-sql-script-file"></a>Optimieren der Arbeitsauslastung für eine Transact-SQL-Skriptdatei  
  
1.  Kopieren einer Beispiel-SELECT-Anweisung oder von Anweisungen von "A. Das Verwenden von SELECT, um Zeilen und Spalten" in [SELECT-Beispiele &#40;Transact-SQL&#41;](../../t-sql/queries/select-examples-transact-sql.md) abzurufen und die Anweisungen in den Abfrage-Editor von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] einzufügen. Speichern Sie die Datei unter dem Namen **MyScript.sql** in einem Verzeichnis, in dem Sie sie leicht wieder auffinden.  
  
2.  Starten Sie den Datenbankoptimierungsratgeber. Weitere Informationen finden Sie unter [Starten des Datenbankoptimierungsratgebers](../../tools/dta/lesson-1-1-launching-database-engine-tuning-advisor.md).  
  
3.  Geben Sie im rechten Bereich der GUI des Datenbankoptimierungsratgebers im Feld **Sitzungsname** den Namen **MySession**ein.  
  
4.  Wählen Sie unter **Arbeitsauslastung** die Option **Datei**aus, und klicken Sie auf die Schaltfläche **Suchen Sie nach einer Arbeitsauslastungsdatei** , um die in Schritt 1 gespeicherte Datei **MyScript.sql** zu suchen.  
  
5.  Wählen Sie [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] in der **Datenbank für Arbeitsauslastungsanalyse** aus, wählen Sie [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] im Raster **Zu optimierende Datenbanken und Tabellen auswählen** aus, und lassen Sie **Optimierungsprotokoll speichern** aktiviert. **Datenbank für Arbeitsauslastungsanalyse** gibt die erste Datenbank an, mit der der Datenbankoptimierungsratgeber beim Optimieren einer Arbeitsauslastung eine Verbindung herstellt. Nach dem Beginn der Optimierung stellt der Datenbankoptimierungsratgeber Verbindungen mit den Datenbanken her, die über die `USE DATABASE`-Anweisungen in der Arbeitsauslastung angegeben sind.  
  
6.  Klicken Sie auf die Registerkarte **Optimierungsoptionen** . In dieser Übung werden Sie keine Optimierungsoptionen festlegen. Aber nehmen Sie sich die Zeit, und überprüfen Sie die Standardoptimierungsoptionen. Drücken Sie F1, um die Hilfe zu dieser Seite im Registerformat anzuzeigen. Klicken Sie auf **Erweiterte Optionen** , um weitere Optimierungsoptionen anzuzeigen. Klicken Sie im Dialogfeld **Erweiterte Optimierungsoptionen** auf **Hilfe** , um weitere Informationen zu den angezeigten Optimierungsoptionen aufzurufen. Klicken Sie auf **Abbrechen** , um das Dialogfeld **Erweiterte Optimierungsoptionen** zu schließen und die Standardoptionen beizubehalten.  
  
7.  Klicken Sie auf der Symbolleiste auf die Schaltfläche **Analyse starten** . Während der Datenbankoptimierungsratgeber die Arbeitsauslastung analysiert, können Sie den Status auf der Registerkarte **Fortschritt** überwachen. Wenn das Optimieren abgeschlossen ist, wird die Registerkarte **Empfehlungen** angezeigt.  
  
    Wenn Sie einen Fehler zum Enddatum und zur Beendigungszeit für die Optimierung erhalten, aktivieren Sie das Kontrollkästchen **Beenden am** auf der Registerkarte **Optimierungsoptionen** . Überprüfen Sie, ob die in **Beenden am** für Datum und Uhrzeit angegebenen Werte größer sind als das aktuelle Datum und die aktuelle Uhrzeit, und ändern Sie die Werte nach Bedarf.  
  
8.  Speichern Sie die Empfehlungen nach Ende der Analyse als [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skript. Klicken Sie dazu im Menü **Aktionen** auf **Empfehlungen speichern** . Navigieren Sie im Dialogfeld **Speichern unter** zu dem Verzeichnis, in dem das Skript mit Empfehlungen gespeichert werden soll, und geben Sie als Dateinamen **MyRecommendations**an.  
  
## <a name="summary"></a>Zusammenfassung  
Sie haben die Arbeitsauslastung für eine einfache SELECT-Anweisung auf der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank optimiert. Der Datenbankoptimierungsratgeber kann auch Ablaufverfolgungsdateien von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] und Tabellen als zu optimierende Arbeitsauslastungen verwenden. In der nächsten Aufgabe wird gezeigt, wie Sie die Optimierungsempfehlungen, die Sie als Ergebnis in dieser Übung erhalten haben, anzeigen und interpretieren.  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in der Lektion  
[Anzeigen von Empfehlungen für die Optimierung](../../tools/dta/lesson-1-2-viewing-tuning-recommendations.md)  
  
  
  

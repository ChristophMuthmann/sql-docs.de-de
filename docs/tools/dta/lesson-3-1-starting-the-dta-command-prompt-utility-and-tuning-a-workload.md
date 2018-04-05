---
title: Starten des Befehlzeilenprogramms Dta und Optimieren einer Arbeitsauslastung | Microsoft Docs
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
ms.assetid: f34a5acf-1f3b-4484-a770-6470cb925ab0
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b4adf756444c22146108fead4f607c20c6108dc3
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="lesson-3-1---starting-the-dta-command-prompt-utility-and-tuning-a-workload"></a>Lektion 3-1: Starten des Befehlzeilenprogramms Dta und Optimieren einer Arbeitsauslastung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Dieser Task führt Sie durch Starten der **Dta** Hilfsprogramm dazugehörige Hilfe anzeigen, und klicken Sie dann zum Optimieren einer arbeitsauslastung von der Befehlszeile aus. Dabei wird die Arbeitsauslastung MyScript.sql verwendet, die Sie in der Übung zur grafischen Benutzeroberfläche des Datenbankoptimierungsratgebers [Optimieren einer Arbeitsauslastung](../../tools/dta/lesson-1-1-tuning-a-workload.md)angelegt haben.  
  
Im Lernprogramm wird die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Beispieldatenbank verwendet. Aus Sicherheitsgründen werden die Beispieldatenbanken nicht standardmäßig installiert. Informationen zur Installation der Beispieldatenbanken finden Sie unter [Installieren der SQL Server-Beispiele und -Beispieldatenbanken](http://sqlserversamples.codeplex.com).  
  
Im Folgenden werden folgende Schritte erläutert: Öffnen einer Eingabeaufforderung, Starten des Befehlszeilen-Hilfsprogramms **dta** , Anzeigen der Syntaxhilfe und Optimieren der einfachen Arbeitsauslastung MyScript.sql, die Sie in [Optimieren einer Arbeitsauslastung](../../tools/dta/lesson-1-1-tuning-a-workload.md)angelegt haben.  
  
### <a name="to-start-the-dta-command-prompt-utility-and-view-help"></a>So starten Sie das Befehlszeilen-Hilfsprogramms dta und zeigen die Hilfe an  
  
1.  Zeigen Sie im **Startmenü** auf **Alle Programme**, zeigen Sie auf **Zubehör**, und klicken Sie anschließend auf **Eingabeaufforderung**.  
  
2.  Geben Sie an der Eingabeaufforderung die folgende ein, und drücken Sie die EINGABETASTE:  
  
    ```  
    dta -? | more  
    ```  
  
    Der folgende Teil des Befehls ist optional: `| more` . Sie können mit seiner Hilfe jedoch die Syntaxhilfe des Hilfsprogramms besser durchblättern. Drücken Sie die EINGABETASTE, um im Hilfetext jeweils eine weitere Zeile anzuzeigen, oder drücken Sie die LEERTASTE, um auf die nächste Seite zu wechseln.  
  
### <a name="to-tune-a-simple-workload-by-using-the-dta-command-prompt-utility"></a>So optimieren Sie eine einfache Arbeitsauslastung mithilfe des Befehlszeilen-Hilfsprogramms dta  
  
1.  Navigieren Sie an der Eingabeaufforderung zu dem Verzeichnis, in dem Sie die Datei MyScript.sql gespeichert haben.  
  
2.  Geben Sie an der Eingabeaufforderung Folgendes ein. Drücken Sie danach die EINGABETASTE, um den Befehl auszuführen und die Optimierungssitzung zu starten (beachten Sie, dass das Hilfsprogramm beim Analysieren von Befehlen die Groß- und Kleinschreibung berücksichtigt):  
  
    ```  
    dta -S YourServerName\YourSQLServerInstanceName -E -D AdventureWorks2012 -if MyScript.sql -s MySession2 -of MySession2OutputScript.sql -ox MySession2Output.xml -fa IDX_IV -fp NONE -fk NONE  
    ```  
  
    Dabei gibt `-S` den Namen Ihres Servers und die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz an, in der die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank installiert ist. Die Einstellung `-E` gibt an, dass Sie eine vertrauenswürdige Verbindungsart mit der Instanz verwenden möchten. Dies ist der geeignete Verbindungstyp, wenn Sie eine Verbindung mit einem Windows-Domänenkonto herstellen. Die Einstellung `-D` gibt die Datenbank an, die Sie optimieren möchten, `-if` gibt die Arbeitsauslastungsdatei an, `-s` gibt den Sitzungsnamen an, `-of` gibt die Datei an, in die das Tool das Skript mit den [!INCLUDE[tsql](../../includes/tsql-md.md)] -Empfehlungen schreiben soll, und `-ox` gibt die Datei an, in die das Tool die Empfehlungen im XML-Format schreiben soll. Die letzten drei Schalter legen folgende Optimierungsoptionen fest: `-fa IDX_IV` gibt an, dass der Datenbankoptimierungsratgeber nur das Hinzufügen von Indizes (gruppiert und nicht gruppiert) und von indizierten Sichten berücksichtigen soll; `-fp NONE` gibt an, dass bei der Analyse keine Partitionsstrategie berücksichtigt werden soll; und `-fk NONE` gibt an, dass in der Datenbank vorhandene physische Entwurfsstrukturen nicht beibehalten werden müssen, wenn der Datenbankoptimierungsratgeber seine Empfehlungen abgibt.  
  
3.  Wenn der Datenbankoptimierungsratgeber mit dem Optimieren der Arbeitsauslastung fertig ist, zeigt er eine Meldung an, die besagt, dass die Optimierungssitzung erfolgreich abgeschlossen wurde. Sie können die Optimierungsergebnisse anzeigen. Verwenden Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] zum Öffnen der Dateien MySession2OutputScript.sql und MySession2Output.xml. Alternativ dazu können Sie auch die Optimierungssitzung MySession2 in der grafischen Benutzeroberfläche des Datenbankoptimierungsratgebers öffnen und die Empfehlungen und Berichte so anzeigen, wie in den Abschnitten [Anzeigen von Empfehlungen für die Optimierung](../../tools/dta/lesson-1-2-viewing-tuning-recommendations.md) und [Anzeigen von Optimierungsberichten](../../tools/dta/lesson-1-3-viewing-tuning-reports.md)erläutert.  
  
## <a name="summary"></a>Zusammenfassung  
Sie haben damit eine einfache Arbeitsauslastung von der Eingabeaufforderung aus mithilfe des Hilfsprogramms **dta** optimiert. Dieses Tool umfasst noch viele weitere Optimierungsoptionen. Weitere Informationen dazu finden Sie in der Hilfe des Tools (**dta -?**) und im Referenzthema [dta (Hilfsprogramm)](../../tools/dta/dta-utility.md) .  
  
## <a name="after-you-finish-this-tutorial"></a>Weiterführende Informationen nach Abschluss dieses Lernprogramms  
Wenn Sie die Lektionen in diesem Lernprogramm durchgearbeitet haben, finden Sie unter folgenden Themen weitere Informationen zum Datenbankoptimierungsratgeber:  
  
-   [Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md) enthält Beschreibungen zum Ausführen von Tasks mit diesem Tool.  
  
-   [dta Utility](../../tools/dta/dta-utility.md) enthält Referenzmaterial zum Eingabeaufforderungs-Hilfsprogramm und der optionalen XML-Datei, mit der Sie die Ausführung des Hilfsprogramms steuern können.  
  
Gehen Sie auf die Seite [Tutorial: Datenbankoptimierungsratgeber](../../tools/dta/tutorial-database-engine-tuning-advisor.md), um zum Anfang des Tutorials zurückzukehren.  
  
## <a name="see-also"></a>Siehe auch  
[Lernprogramme zum Datenbankmodul](../../relational-databases/database-engine-tutorials.md)  
  
  
  

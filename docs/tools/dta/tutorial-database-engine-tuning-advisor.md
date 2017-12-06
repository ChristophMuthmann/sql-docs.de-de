---
title: 'Lernprogramm: Datenbankoptimierungsratgeber | Microsoft Docs'
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: dta
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
helpviewer_keywords:
- Database Engine Tuning Advisor [SQL Server], tutorials
- tutorials [Database Engine Tuning Advisor]
ms.assetid: 3b54cbbe-d8c6-424d-92f1-aa58179f4da8
caps.latest.revision: "38"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 91ada122d3cdad5d3b40b1809c063b821c898bcb
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="tutorial-database-engine-tuning-advisor"></a>Lernprogramm: Datenbankoptimierungsratgeber
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Willkommen Sie beim Lernprogramm Datenbankmodul-Optimierungsratgeber. Der Datenbankoptimierungsratgeber prüft, wie Abfragen in den von Ihnen angegebenen Datenbanken verarbeitet werden. Er gibt dann eine Empfehlung ab, wie Sie die Verarbeitung von Abfragen verbessern können, indem Sie Datenbankstrukturen ändern, wie z. B. Indizes, indizierte Sichten und die Partitionierung.  
  
Der Datenbankoptimierungsratgeber bietet zwei Benutzeroberflächen: eine grafische Benutzeroberfläche (GUI) und das Befehlszeilenhilfsprogramm **dta** . Über die grafische Benutzeroberfläche können schnell die Ergebnisse von Optimierungssitzungen angezeigt werden. Das Hilfsprogramm **dta** ermöglicht die einfache Übernahme von Funktionen des Datenbankoptimierungsratgebers in Skripts für die automatische Optimierung. Darüber hinaus kann der Datenbankoptimierungsratgeber XML-Eingaben annehmen und bietet somit eine bessere Steuerung des Optimierungsprozesses.  
  
## <a name="what-you-will-learn"></a>Lernziele  
In diesem Lernprogramm erfahren Sie, wie Sie in der grafischen Benutzeroberfläche des Datenbankoptimierungsratgebers navigieren. Außerdem werden Sie einige einfache Aufgaben mithilfe der grafischen Benutzeroberfläche und mit dem Hilfsprogramm **dta** ausführen. Es enthält die folgenden Lektionen:  
  
[Lektion 1: Grundlagen zur Navigation im Datenbankoptimierungsratgeber](../../tools/dta/lesson-1-basic-navigation-in-database-engine-tuning-advisor.md)  
In dieser Lektion machen Sie sich mit der grafischen Benutzeroberfläche des neuen Datenbankoptimierungsratgebers vertraut und lernen, wie Sie die Anzeigeoptionen und das Layout festlegen.  
  
[Lektion 2: Verwenden des Datenbankoptimierungsratgebers](../../tools/dta/lesson-2-using-database-engine-tuning-advisor.md)  
In dieser Lektion erfahren Sie, wie Sie einfache Optimierungsaufgaben mit der grafischen Benutzeroberfläche des Datenbankoptimierungsratgebers ausführen.  
  
[Lektion 3: Verwenden des Befehlszeilenprogramms dta](../../tools/dta/lesson-3-using-the-dta-command-prompt-utility.md)  
In dieser Lektion lernen Sie, wie Sie das Befehlszeilenprogramm **dta** starten und wie Sie einige einfache Optimierungsbefehle ausführen.  
  
## <a name="requirements"></a>Anforderungen  
Dieses Lernprogramm richtet sich an Datenbankadministratoren, die noch nicht mit der grafischen Benutzeroberfläche des Datenbankoptimierungsratgebers oder mit dem Befehlszeilenhilfsprogramm **dta** vertraut sind, die jedoch mit Datenbankkonzepten und -strukturen vertraut sind, wie z.B. mit Indizes und indizierten Sichten.  
  
[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (bzw. eine höhere Version) muss mit der Beispieldatenbank [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] installiert werden. Aus Sicherheitsgründen werden die Beispieldatenbanken standardmäßig nicht installiert. Informationen zur Installation der Beispieldatenbanken finden Sie unter [Installieren der SQL Server-Beispiele und -Beispieldatenbanken](http://sqlserversamples.codeplex.com).  
  
## <a name="after-you-finish-this-tutorial"></a>Weiterführende Informationen nach Abschluss dieses Lernprogramms  
Wenn Sie die Lektionen in diesem Lernprogramm durchgearbeitet haben, finden Sie unter folgenden Themen weitere Informationen zum Datenbankoptimierungsratgeber:  
  
-   [Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md) enthält Beschreibungen zum Ausführen von Tasks mit diesem Tool.  
  
-   [dta Utility](../../tools/dta/dta-utility.md) enthält Referenzmaterial zum Eingabeaufforderungs-Hilfsprogramm und der optionalen XML-Datei, mit der Sie die Ausführung des Hilfsprogramms steuern können.  
  
## <a name="next-lesson"></a>Nächste Lektion  
[Lektion 1: Grundlagen zur Navigation im Datenbankoptimierungsratgeber](../../tools/dta/lesson-1-basic-navigation-in-database-engine-tuning-advisor.md)  
  
  
  

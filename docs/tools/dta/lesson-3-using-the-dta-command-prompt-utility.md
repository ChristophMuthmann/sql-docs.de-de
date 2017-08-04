---
title: 'Lektion 3: Verwenden des Befehlszeilenprogramms Dta | Microsoft Docs'
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
- Database Engine [SQL Server], tutorials
ms.assetid: 30f27f4d-8852-4b12-ba62-57f63e496f1d
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b33b5d2a64fc88cbd53d6c76fd73165ade697eac
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="lesson-3-using-the-dta-command-prompt-utility"></a>Lektion 3: Verwenden des Befehlszeilenprogramms dta
Mit dem Befehlszeilenprogramm **dta** wird die Funktionalität des Datenbankoptimierungsratgebers erweitert.  
  
Sie können mit Ihren bevorzugten XML-Tools Eingabedateien für das Befehlszeilenprogramm erstellen und dabei das XML-Schema des Datenbankoptimierungsratgebers verwenden. Dieses Schema wird zusammen mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert. Es befindet sich unter: C:\Programme (x86)\Microsoft SQL Server\110\Tools\Binn\schemas\sqlserver\2004\07\dta\dtaschema.xsd.  
  
Das XML-Schema des Datenbankoptimierungsratgebers ist auch online auf [dieser Microsoft-Website](http://go.microsoft.com/fwlink/?linkid=43100&clcid=0x409)verfügbar.  
  
Das XML-Schema des Datenbankoptimierungsratgebers ermöglicht mehr Flexibilität beim Festlegen von Optimierungsoptionen. So ermöglicht es z. B. die Durchführung einer "Was-wäre-wenn-Analyse". Für eine "Was-wäre-wenn-Analyse" wird für die Datenbank, die optimiert werden soll, eine Gruppe vorhandener sowie hypothetischer physischer Entwurfsstrukturen angegeben. Diese werden dann mit dem Datenbankoptimierungsratgeber analysiert, um herauszufinden, welche dieser hypothetischen Entwurfsstrukturen die Abfrageverarbeitung verbessert. Diese Art einer Analyse hat den Vorteil, dass die neue Konfiguration ausgewertet werden kann, ohne dass eine Implementierung erforderlich ist. Wenn die hypothetische physische Entwurfsstruktur nicht die gewünschten Leistungsverbesserungen erbringt, können Sie sie einfach ändern und erneut analysieren, bis die Konfiguration erreicht ist, mit der die gewünschten Ergebnisse erzielt werden.  
  
Außerdem können Sie mit dem XML-Schema des Datenbankoptimierungsratgebers und mit dem Befehlszeilenprogramm **dta** Funktionen des Datenbankoptimierungsratgebers in Skripts übernehmen und diese in anderen Datenbankentwicklungstools verwenden.  
  
Auf die Verwendung der XML-Eingabefunktionen des Datenbankoptimierungsratgebers wird in dieser Lektion nicht eingegangen.  
  
In dieser Lektion finden Sie eine Einführung in die Basissyntax des Befehlszeilenprogramms **dta** . Außerdem wird der Zugriff auf die Hilfe und das Optimieren der Arbeitsauslastung erläutert.  
  
Die Lektion enthält die folgenden Themen:  
  
-   Starten des Befehlzeilenprogramms **dta** und Optimieren einer Arbeitsauslastung  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in der Lektion  
[Starten des Befehlzeilenprogramms Dta und Optimieren einer Arbeitsauslastung](../../tools/dta/lesson-3-1-starting-the-dta-command-prompt-utility-and-tuning-a-workload.md)  
  
  
  


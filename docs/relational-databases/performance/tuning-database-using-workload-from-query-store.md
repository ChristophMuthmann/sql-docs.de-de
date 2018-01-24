---
title: Datenbankoptimierung mithilfe der Arbeitsauslastung aus dem Abfragespeicher | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Database Engine Tuning Advisor, Query Store
ms.assetid: 17107549-5073-4fa2-8ee7-5ed33b38821e
caps.latest.revision: "9"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8d43a90f7c4bebef8bb9753dd02b29b46a2f30b8
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="tuning-database-using-workload-from-query-store"></a>Datenbankoptimierung mithilfe der Arbeitsauslastung aus dem Abfragespeicher
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]


Die Funktion [Abfragespeicher](../../relational-databases/performance/how-query-store-collects-data.md) in SQL Server erfasst automatisch einen Verlauf der Abfragen, Pläne und Laufzeitstatistiken und speichert diese Informationen in der Datenbank. Der [Datenbankoptimierungsratgeber (Database Engine Tuning Advisor, DTA)](../../relational-databases/performance/database-engine-tuning-advisor.md) unterstützt eine neue Option, bei der man den Abfragespeicher verwenden kann, um automatisch eine entsprechende Arbeitsauslastung für die Optimierung auszuwählen. Viele Benutzer müssen dadurch nicht mehr explizit eine Arbeitsauslastung für die Optimierung erfassen. Diese Funktion ist nur verfügbar, wenn in der Datenbank die Abfragespeicherfunktion aktiviert ist. 
  
  Dieses Feature ist in SQL Server Management Studio, Version **16.4** oder höher verfügbar. 
  
<a name="how-to-tune-a-workload-from-query-store-in-database-engine-tuning-advisor-gui"></a>So optimieren Sie eine Arbeitsauslastung aus dem Abfragespeicher in der GUI des Datenbankoptimierungsratgebers
---
Wählen Sie über die DTA GUI das Optionsfeld **Abfragespeicher** im Bereich **Allgemein** aus, um diese Funktion zu aktivieren (siehe folgende Abbildung).
![DTA-Arbeitsauslastung aus Abfragespeicher](../../relational-databases/performance/media/dta-workload-from-query-store.gif)
 
<a name="how-to-tune-a-workload-from-query-store-in-dtaexe-command-line-utility"></a>So optimieren Sie eine Arbeitsauslastung aus dem Abfragespeicher im Befehlszeilenprogramm „dta.exe“
---
Wählen Sie aus der Befehlszeile („dta.exe“) die Option **-iq** aus, um die Arbeitsauslastung aus dem Abfragespeicher auszuwählen. 

Es stehen zwei zusätzliche Optionen über die Befehlszeile zur Verfügung, über die Sie das Verhalten von DTA bei der Auswahl der Arbeitsauslastung aus dem Abfragespeicher optimieren können. Folgende Optionen sind nicht über die GUI verfügbar:
  1. Anzahl der zu optimierenden Arbeitsauslastungsereignisse: Diese Option, die mithilfe des Befehlszeilenarguments **-n** angegeben wird, ermöglicht Benutzern die Kontrolle darüber, wie viele Ereignisse aus dem Abfragespeicher optimiert werden. Standardmäßig verwendet DTA einen Wert von 1000 für diese Option. Beachten Sie, dass DTA immer die aufwendigsten Ereignisse nach Gesamtdauer auswählt. 
  
  2. Zeitfenster der zu optimierenden Ereignisse: Nachdem der Abfragespeicher möglicherweise viele Abfragen enthält, die vor langer Zeit ausgeführt wurden, ermöglicht diese Option dem Benutzer das Angeben eines vergangenen Zeitfensters (in Stunden), wann eine Abfrage ausgeführt worden sein muss, damit sie von DTA für die Optimierung berücksichtigt wird. Diese Option wird mithilfe des Befehlszeilenarguments **-I** angegeben. 

Weitere Informationen finden Sie unter [dta Utility](../../tools/dta/dta-utility.md).

<a name="difference-between-using-workload-from-query-store-and-plan-cache"></a>Unterschied zwischen der Verwendung der Arbeitsauslastung aus dem Abfragespeicher und Plancache 
--- 
Der Unterschied zwischen den Optionen „Abfragespeicher“ und „Plancache“ liegt darin, dass ersterer einen langen Verlauf von Abfragen enthält, die in der Datenbank ausgeführt wurden und zwischen Serverneustarts beibehalten werden. Der Plancache enthält dagegen nur eine Teilmenge von kürzlich ausgeführten Abfragen, deren Pläne im Arbeitsspeicher zwischengespeichert werden. Wenn der Server neu gestartet wird, werden die Einträge im Plancache gelöscht.

<a name="see-also"></a>Weitere Informationen finden Sie unter 
--- 
[Datenbankoptimierungsratgeber](../../relational-databases/performance/database-engine-tuning-advisor.md)     
[Tutorial: Datenbankoptimierungsratgeber](Tutorial:%20Database%20Engine%20Tuning%20Advisor.md)     
[So werden Daten im Abfragespeicher gesammelt](../../relational-databases/performance/how-query-store-collects-data.md)     
[Abfragespeicher, bewährte Methoden](../../relational-databases/performance/best-practice-with-the-query-store.md)

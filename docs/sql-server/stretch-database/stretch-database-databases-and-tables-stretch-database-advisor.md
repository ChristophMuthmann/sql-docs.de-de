---
title: "Identifizieren von Datenbanken und Tabellen für Stretch Database mit Data Migration Assistant | Microsoft-Dokumentation"
ms.custom: 
ms.date: 10/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: stretch-database
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Stretch Database, identifying databases
- Stretch Database, identifying tables
- identifying databases for Stretch Database
- identifying tables for Stretch Database
ms.assetid: 81bd93d8-eef8-4572-88d7-5c37ab5ac2bf
caps.latest.revision: "29"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3fe01369c0dc9ab2f8556cafd932d6c624ed9554
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="identify-databases-and-tables-for-stretch-database-with-data-migration-assistant"></a>Identifizieren von Datenbanken und Tabellen für Stretch Database von Data Migration Assistant
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Laden Sie Microsoft Data Migration Assistant herunter, und führen Sie diesen aus, um Datenbanken und Tabellen, die für Stretch Database in Frage kommen, sowie mögliche Blockierungsprobleme zu ermitteln.
  
## <a name="get-data-migration-assistant"></a>Abrufen von Data Migration Assistant
 Laden Sie Data Migration Assistant [hier](https://www.microsoft.com/download/details.aspx?id=53595)herunter, und installieren Sie ihn. Dieses Tool ist in den SQL Server-Installationsmedien nicht enthalten.  
  
## <a name="run-data-migration-assistant"></a>Ausführen von Data Migration Assistant  
  
1.  Führen Sie Microsoft Data Migration Assistant aus.  

2.  Erstellen Sie ein neues Projekt des Typs **Assessment**, und benennen Sie es.

3.  Wählen Sie **SQL Server** sowohl als **Source server type** (Quellservertyp) als auch als **Target server type** (Zielservertyp) aus.

4.  Wählen Sie **Erstellen**aus. 

5. Klicken Sie auf der Seite **Optionen** (Schritt 1) auf **New features recommendation** (Empfehlungen neuer Funktionen). Deaktivieren Sie gegebenenfalls die Auswahl für **Kompatibilitätsprobleme**.

6.  Stellen Sie auf der Seite **Quellen auswählen** (Schritt 2) eine Verbindung zum Server her, wählen Sie eine Datenbank und anschließend **Hinzufügen** aus.

7.  Klicken Sie auf **Start Assessment** (Bewertung starten).

## <a name="review-the-results"></a>Auswerten der Ergebnisse  
  
1.  Wenn die Analyse abgeschlossen wurde, wählen Sie auf der Seite **Ergebnisse überprüfen** (Schritt 3) die Option **Featureempfehlungen** aus, und klicken Sie dann auf die Registerkarte **Speicher**.

2.  Sehen Sie sich die Empfehlungen zu Stretch Database an. Jede Empfehlung listet neben den möglichen Blockierungsproblemen die Tabellen auf, für die Stretch Database möglicherweise geeignet ist.

## <a name="historical-note"></a>Hinweis zum Verlauf
Der Stretch Database-Ratgeber war zuvor eine Komponente des SQL Server 2016-Upgrade Advisors. Zu diesem Zeitpunkt musste der Stretch Database-Advisor als separate Aktion ausgewählt und ausgeführt werden.

Mit der Veröffentlichung von Data Migration Assistant, das den Upgrade Advisor ersetzt und erweitert, werden die Funktionen des Stretch Database Advisor in dieses neue Tool integriert. Sie müssen keinerlei Optionen auswählen, um Empfehlungen im Zusammenhang mit Stretch Database zu erhalten. Wenn Sie in Data Migration Assistant eine Bewertung ausführen, werden die Ergebnisse in der Registerkarte **Speicher** der **Featureempfehlungen** angezeigt, die im Zusammenhang mit der Stretch Database stehen.
  
## <a name="next-step"></a>Nächster Schritt  
 Aktivieren Sie Stretch Database.  
  
-   Informationen zum aktivieren von Stretch Database für eine **Datenbank**finden Sie unter [Aktivieren von Stretch Database für eine Datenbank](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md).  
  
-   Informationen darüber, wie Sie Stretch Database auf einer anderen **Tabelle**aktivieren, wenn Stretch bereits auf der Datenbank aktiviert ist, finden Sie unter [Aktivieren von Stretch Database für eine Tabelle](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md). 
  
## <a name="see-also"></a>Siehe auch  
 [Einschränkungen für Stretch Database](../../sql-server/stretch-database/limitations-for-stretch-database.md)   
 [Aktivieren von Stretch Database für eine Datenbank](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [Aktivieren von Stretch-Datenbank für eine Tabelle](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
  

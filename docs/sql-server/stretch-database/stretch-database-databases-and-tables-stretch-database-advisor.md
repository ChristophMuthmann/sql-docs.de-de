---
title: "Datenbanken und Tabellen für Stretch-Datenbank – Ratgeber für Stretch-Datenbank | Microsoft-Dokumentation"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/14/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Stretch Database, identifying databases
- Stretch Database, identifying tables
- identifying databases for Stretch Database
- identifying tables for Stretch Database
ms.assetid: 81bd93d8-eef8-4572-88d7-5c37ab5ac2bf
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 603226ee369f6e557bae19e80211677f92fe7cd7
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="stretch-database-databases-and-tables---stretch-database-advisor"></a>Datenbanken und Tabellen für Stretch-Datenbank – Ratgeber für Stretch-Datenbank
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Zum Identifizieren von Datenbanken und Tabellen, die für Stretch-Datenbank in Frage kommen, laden Sie den Aktualisierungsratgeber für SQL Server 2016 herunter, und führen Sie den Ratgeber für Stretch-Datenbank aus. Der Ratgeber für Stretch-Datenbank ermittelt auch Blockierungsprobleme.  
  
## <a name="download-and-install-upgrade-advisor"></a>Herunterladen und Installieren von Upgrade Advisor  
 Sie können Upgrade Advisor [hier](https://www.microsoft.com/en-us/download/details.aspx?id=53595)herunterladen und installieren. Dieses Tool ist in den [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] -Installationsmedien nicht enthalten.  
  
## <a name="run-the-stretch-database-advisor"></a>Ausführen des Ratgebers für Stretch-Datenbank  
  
1.  Führen Sie den Upgrade Advisor aus.  
  
2.  Wählen Sie **Szenarien**und anschließend **RUN STRETCH DATABASE ADVISOR**(Ratgeber für Stretch-Datenbank ausführen) aus.  
  
3.  Klicken Sie auf dem Blatt für den **Ratgeber für Stretch-Datenbank ausführen** auf **SELECT DATABASES TO ANALYZE**(Datenbanken zum Analysieren auswählen).  
  
4.  Geben Sie auf dem Blatt **Datenbanken auswählen** den Servernamen und die Authentifizierungsinformationen ein, oder wählen Sie diese aus. Klicken Sie auf **Verbinden**.

5.  Eine Liste der Datenbanken auf dem ausgewählten Server wird angezeigt. Wählen Sie die zu analysierenden Datenbanken aus. Klicken Sie auf **Auswählen**.  
  
6.  Klicken Sie auf dem Blatt für den **Ratgeber für Stretch-Datenbank ausführen** auf **Ausführen**.  Die Analyse wird ausgeführt.  
  
## <a name="review-the-results"></a>Auswerten der Ergebnisse  
  
1.  Wählen Sie nach Abschluss der Analyse auf dem Blatt **Analysierte Datenbanken** eine der Datenbanken aus, die Sie analysiert haben, um das Blatt **Analyseergebnisse** anzuzeigen.  
  
     Das Blatt **Analyseergebnisse** listet empfohlene Tabellen in der ausgewählten Datenbank auf, die den Standardempfehlungskriterien entsprechen. 
  
2.  Wählen Sie auf dem Blatt **Analyseergebnisse** in der Liste der Tabellen eine der empfohlenen Tabellen aus, um das Blatt **Tabellenergebnisse** anzuzeigen.  
  
     Das Blatt **Tabellenergebnisse** listet die Blockierungsprobleme der ausgewählten Tabelle auf, sofern entsprechende Probleme vorliegen. Informationen über die vom Ratgeber für Stretch-Datenbank erkannten Blockierungsprobleme finden Sie unter [Einschränkungen (Stretch-Datenbank)](../../sql-server/stretch-database/limitations-for-stretch-database.md).  
  
3.  Wählen Sie auf dem Blatt **Tabellenergebnisse** eines der Blockierungsprobleme aus, um weitere Informationen zum ausgewählten Problem anzuzeigen und Schritte zur Behebung vorzuschlagen. Implementieren Sie die vorgeschlagenen Schritte zur Vermeidung, wenn Sie die ausgewählte Tabelle für Stretch-Datenbank konfigurieren möchten.  
  
## <a name="next-step"></a>Nächster Schritt  
 Aktivieren Sie Stretch-Datenbank.  
  
-   Informationen zum aktivieren von Stretch-Datenbank für eine **Datenbank**finden Sie unter [Aktivieren von Stretch-Datenbank für eine Datenbank](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md).  
  
-   Informationen darüber, wie Sie Stretch-Datenbank auf einer anderen **Tabelle**aktivieren, wenn Stretch bereits auf der Datenbank aktiviert ist, finden Sie unter [Aktivieren von Stretch-Datenbank für eine Tabelle](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md). 
  
## <a name="see-also"></a>Siehe auch  
 [Einschränkungen (Stretch-Datenbank)](../../sql-server/stretch-database/limitations-for-stretch-database.md)   
 [Aktivieren von Stretch-Datenbank für eine Datenbank](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [Aktivieren von Stretch-Datenbank für eine Tabelle](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
  


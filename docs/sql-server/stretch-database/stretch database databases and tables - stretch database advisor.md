---
title: "Identifizieren von Datenbanken und Tabellen f&#252;r Stretch-Datenbank durch Ausf&#252;hren des Ratgebers f&#252;r Stretch-Datenbank | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.service: "sql-server-stretch-database"
ms.suite: ""
ms.technology: 
  - "dbe-stretch"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Stretch-Datenbank, Identifizieren von Datenbanken"
  - "Stretch-Datenbank, Identifizieren von Tabellen"
  - "Identifizieren von Datenbanken für Stretch-Datenbank"
  - "Identifizieren von Tabellen für Stretch-Datenbank"
ms.assetid: 81bd93d8-eef8-4572-88d7-5c37ab5ac2bf
caps.latest.revision: 29
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
---
# Identifizieren von Datenbanken und Tabellen f&#252;r Stretch-Datenbank durch Ausf&#252;hren des Ratgebers f&#252;r Stretch-Datenbank
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Zum Identifizieren von Datenbanken und Tabellen, die für Stretch-Datenbank in Frage kommen, laden Sie den Aktualisierungsratgeber für SQL Server 2016 herunter, und führen Sie den Ratgeber für Stretch-Datenbank aus. Der Ratgeber für Stretch-Datenbank ermittelt auch Blockierungsprobleme.  
  
## Herunterladen und Installieren von Upgrade Advisor  
 Sie können Upgrade Advisor [hier](http://go.microsoft.com/fwlink/?LinkID=613421) herunterladen und installieren. Dieses Tool ist in den [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]-Installationsmedien nicht enthalten.  
  
## Ausführen des Ratgebers für Stretch-Datenbank  
  
1.  Führen Sie den Upgrade Advisor aus.  
  
2.  Wählen Sie **Szenarien** und anschließend **RUN STRETCH DATABASE ADVISOR** (Ratgeber für Stretch-Datenbank ausführen) aus.  
  
3.  Klicken Sie auf dem Blatt für den **Ratgeber für Stretch-Datenbank ausführen** auf **SELECT DATABASES TO ANALYZE** (Datenbanken zum Analysieren auswählen).  
  
4.  Geben Sie auf dem Blatt **Datenbanken auswählen** den Servernamen und die Authentifizierungsinformationen ein, oder wählen Sie diese aus. Klicken Sie auf **Verbinden**.

5.  Eine Liste der Datenbanken auf dem ausgewählten Server wird angezeigt. Wählen Sie die zu analysierenden Datenbanken aus. Klicken Sie auf **Auswählen**.  
  
6.  Klicken Sie auf dem Blatt für den **Ratgeber für Stretch-Datenbank ausführen** auf **Ausführen**.  Die Analyse wird ausgeführt.  
  
## Auswerten der Ergebnisse  
  
1.  Wählen Sie nach Abschluss der Analyse auf dem Blatt **Analysierte Datenbanken** eine der Datenbanken aus, die Sie analysiert haben, um das Blatt **Analyseergebnisse** anzuzeigen.  
  
     Das Blatt **Analyseergebnisse** listet empfohlene Tabellen in der ausgewählten Datenbank auf, die den Standardempfehlungskriterien entsprechen. 
  
2.  Wählen Sie auf dem Blatt **Analyseergebnisse** in der Liste der Tabellen eine der empfohlenen Tabellen aus, um das Blatt **Tabellenergebnisse** anzuzeigen.  
  
     Das Blatt **Tabellenergebnisse** listet die Blockierungsprobleme der ausgewählten Tabelle auf, sofern entsprechende Probleme vorliegen. Informationen über die vom Ratgeber für Stretch-Datenbank erkannten Blockierungsprobleme finden Sie unter [Einschränkungen (Stretch-Datenbank)](../../sql-server/stretch-database/limitations-for-stretch-database.md).  
  
3.  Wählen Sie auf dem Blatt **Tabellenergebnisse** eines der Blockierungsprobleme aus, um weitere Informationen zum ausgewählten Problem anzuzeigen und Schritte zur Behebung vorzuschlagen. Implementieren Sie die vorgeschlagenen Schritte zur Vermeidung, wenn Sie die ausgewählte Tabelle für Stretch-Datenbank konfigurieren möchten.  
  
## Nächster Schritt  
 Aktivieren Sie Stretch-Datenbank.  
  
-   Informationen zum aktivieren von Stretch-Datenbank für eine **Datenbank** finden Sie unter [Aktivieren von Stretch-Datenbank für eine Datenbank](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md).  
  
-   Informationen darüber, wie Sie Stretch-Datenbank auf einer anderen **Tabelle** aktivieren, wenn Stretch bereits auf der Datenbank aktiviert ist, finden Sie unter [Aktivieren von Stretch-Datenbank für eine Tabelle](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md).  
  
## Siehe auch  
 [Einschränkungen (Stretch-Datenbank)](../../sql-server/stretch-database/limitations-for-stretch-database.md)   
 [Aktivieren von Stretch-Datenbank für eine Datenbank](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [Aktivieren von Stretch-Datenbank für eine Tabelle](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
  
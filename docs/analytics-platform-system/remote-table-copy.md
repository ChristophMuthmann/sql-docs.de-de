---
title: Kopieren der Remotetabelle - Parallel Data Warehouse | Microsoft Docs
description: Remotetabelle Kopie in Analytics Platform System Parallel Data Warehouse verwenden.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5ed517a471368e4192ad7393a92274424d37f975
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="remote-table-copy"></a>Remotetabelle kopieren
Beschreibt, wie die Remotetabelle Copy-Funktion verwenden, um Tabellen aus SQL Server PDW-Datenbanken auf entfernte (nicht-Appliance) – SMP – SQL Server-Datenbanken zu kopieren. Verwenden Sie für SQL Server PDW Remotetabelle Kopie auf Hub- und Spoke-Szenarien ermöglicht.  
  
## <a name="BasicsPDE"></a>Verstehen der Remotetabelle Kopie für SQLServer PDW  
Remotetabelle Kopie ist ein Feature von SQL Server PDW, die Hub- und Spoke-Szenarien ermöglicht, die Ergebnisse einer SQL SELECT-Anweisung auf eine Tabelle in einer SMP-Datenbank kopieren. Die Remotetabelle Kopie wird initiiert, mit der [CREATE REMOTE TABLE AS SELECT](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md) Anweisung.  
  
## <a name="BasicsPrerequisites"></a>Anforderungen für die Verwendung von Remote-Tabelle kopieren  
Sie können die Remotetabelle Copy zum Kopieren von Tabellen aus SQL Server PDW mit einer SQL Server-Datenbank verwenden, wenn diese Bedingungen erfüllt sind:  
  
-   Die Zieldatenbank muss eine Instanz von Microsoft® SQL Server®, die auf einem System Microsoft Windows® ausgeführt wird, die mit der SQL Server PDW Appliance verbinden, jedoch befindet sich nicht auf einem Server innerhalb der Anwendung. SQL-Remoteserver kann in der SQL Server-PDW mit dem InfiniBand-Netzwerk oder über das Ethernet-Netzwerk verbunden werden.  
  
-   Der zu kopierenden Daten muss mit einer einzelnen gültigen SQL Server PDW auswählbare [wählen](../t-sql/queries/select-transact-sql.md) Anweisung.  
  
-   Der Zielserver muss Server sein, der nicht zur Appliance gehört. Daten können nicht direkt von einem Gerät kopiert werden, in eine andere mithilfe der Anweisungen in diesem Thema.  
  
-   Der Zielserver muss für alle Knoten auf die Appliance Infiniband-Netzwerk zugegriffen werden kann.  
  
## <a name="ConfigureRemote"></a>Konfigurieren Sie die Remotetabelle kopieren  
Um Remotetabelle Kopie zu verwenden, müssen Sie kaufen und Konfigurieren eines Windows-Servers konfigurieren von SQL Server auf dem WindowsServer und Konfigurieren von SQL Server PDW. Verwenden Sie die folgenden Links, um diese drei Konfigurationsschritte ausführen.  
  
1.  [Konfigurieren Sie eine externe Windows-System zum Empfangen der Remotetabelle Kopien mit InfiniBand](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md)  
  
2.  [Konfigurieren Sie eine externe SMP-SQL-Server für den Empfang von Kopien der Remotetabelle](configure-an-external-smp-sql-server-to-receive-remote-table-copies.md)  
  
3.  [Konfigurieren von SQLServer PDW für Kopien der Remotetabelle](configure-sql-server-pdw-for-remote-table-copies.md)  
  
## <a name="PerformRemote"></a>Führen Sie eine Kopie der Remotetabelle  
Um eine Kopie der Remotetabelle auszuführen, verwenden die [CREATE REMOTE TABLE AS SELECT](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md) SQL-Anweisung. Beispiele sind in der CREATE REMOTE TABLE Thema enthalten.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  

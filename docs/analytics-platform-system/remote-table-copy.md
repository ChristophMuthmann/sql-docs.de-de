---
title: Remotetabelle kopieren (SQLServer PDW)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e00d948f-fede-4d41-a45d-67134770ce37
caps.latest.revision: "23"
ms.openlocfilehash: 3de6700957b48c5022c73c3d521bf6f6ed090553
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="remote-table-copy"></a>Remotetabelle kopieren
Beschreibt, wie die Remotetabelle Copy-Funktion verwenden, um Tabellen aus SQL Server PDW-Datenbanken auf entfernte (nicht-Appliance) – SMP – SQL Server-Datenbanken zu kopieren. Verwenden Sie für SQL Server PDW Remotetabelle Kopie auf Hub- und Spoke-Szenarien ermöglicht.  
  
## <a name="BasicsPDE"></a>Verstehen der Remotetabelle Kopie für SQLServer PDW  
Remotetabelle Kopie ist ein Feature von SQL Server PDW, die Hub- und Spoke-Szenarien ermöglicht, die Ergebnisse einer SQL SELECT-Anweisung auf eine Tabelle in einer SMP-Datenbank kopieren. Die Remotetabelle Kopie wird initiiert, mit der [CREATE REMOTE TABLE AS SELECT](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md) Anweisung.  
  
## <a name="BasicsPrerequisites"></a>Anforderungen für die Verwendung von Remote-Tabelle kopieren  
Sie können die Remotetabelle Copy zum Kopieren von Tabellen aus SQL Server PDW mit einer SQL Server-Datenbank verwenden, wenn diese Bedingungen erfüllt sind:  
  
-   Die Zieldatenbank muss eine Instanz von Microsoft® SQL Server®, die auf einem System Microsoft Windows® ausgeführt wird, die mit der SQL Server PDW Appliance verbinden, jedoch befindet sich nicht auf einem Server innerhalb der Anwendung. SQL-Remoteserver kann in der SQL Server-PDW mit dem InfiniBand-Netzwerk oder über das Ethernet-Netzwerk verbunden werden.  
  
-   Der zu kopierenden Daten muss mit einer einzelnen gültigen SQL Server PDW auswählbare [wählen](../t-sql/queries/select-transact-sql.md) Anweisung.  
  
-   Der Zielserver muss ein nicht-Appliance-Server sein. Daten können nicht direkt von einem Gerät kopiert werden, in eine andere mithilfe der Anweisungen in diesem Thema.  
  
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
  

---
title: "Ändern des Datenbank-Kompatibilitätsmodus und Verwenden des Abfragespeichers | Microsoft-Dokumentation"
ms.custom: 
ms.date: 07/21/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- query plans [SQL Server], migrating
- upgrading SQL Server, migrating query plans
- plan guides [SQL Server], migrating query plans
ms.assetid: 7e02a137-6867-4f6a-a45a-2b02674f7e65
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6fa6e9e16be729fba7334b26b130c8e22525e479
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="change-the-database-compatibility-mode-and-use-the-query-store"></a>Ändern des Datenbank-Kompatibilitätsmodus und Verwenden des Abfragespeichers
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] werden einige Änderungen erst wirksam, nachdem der [Datenbank-Kompatibilitätsgrad](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md) geändert wurde. Dies hat verschiedene Gründe:  
  
- Da das Upgraden einen unidirektionalen Vorgang darstellt (ein Downgrade des Dateiformats ist nicht möglich), ist es sinnvoll, das Aktivieren neuer Funktionen als separaten Datenbankvorgang durchzuführen. Es ist möglich, eine Einstellung auf einen früheren Datenbank-Kompatibilitätsgrad zurückzusetzen.  Das neue Modell reduziert die Anzahl von Vorgängen, die während einer Ausfallzeit durchgeführt werden müssen.  
  
- Änderungen am Abfrageprozessor können komplexe Auswirkungen haben. Obwohl eine „positive“ Änderung am System für die meisten Workloads sehr gut sein kann, könnte sie an anderer Stelle für eine wichtige Abfrage eine unzulässige Regression verursachen. Durch die Trennung dieser Logik vom Upgradevorgang können Features, wie z. B. der Abfragespeicher, Planauswahlregressionen auf Produktionsservern schnell abschwächen oder sogar komplett vermeiden.  
  
> [!IMPORTANT]  
> War der Kompatibilitätsgrad einer Benutzerdatenbank vor dem Upgrade 100 oder höher, wird er nach dem Upgrade beibehalten. War der Kompatibilitätsgrad einer Benutzerdatenbank vor dem Upgrade 90, wird er auf 100 gesetzt, was dem niedrigsten unterstützten Kompatibilitätsgrad in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] entspricht. Der Kompatibilitätsgrad der Datenbanken „tempdb“, „model“, „msdb“ und „Resource“ wird nach dem Upgrade auf den aktuellen Kompatibilitätsgrad festgelegt.
> Die „master“-Systemdatenbank behält den Kompatibilitätsgrad von vor dem Upgrade bei. 
  
Der Upgradevorgang zum Aktivieren neuer Abfrageprozessorfunktionen steht im Zusammenhang mit dem Wartungsmodell des Produkts nach der Einführung.  Einige dieser Fixes werden unter dem [Ablaufverfolgungsflag 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md#4199) zur Verfügung gestellt.  Kunden, die Fixes benötigen, können diese abonnieren, ohne unerwartete Regressionen für andere Kunden zu verursachen. Das Wartungsmodell für Abfrageprozessor-Hotfixes nach der Einführung ist [hier](http://support.microsoft.com/kb/974006)dokumentiert. Ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bedeutet das Verschieben in einen neuen Kompatibilitätsgrad, dass das Ablaufverfolgungsflag 4199 nicht mehr benötigt wird, da diese Problembehebungen (Fixes) nun standardmäßig im aktuellsten Kompatibilitätsgrad aktiviert sind. Im Rahmen des Upgradevorgangs ist es daher wichtig, sich zu vergewissern, dass 4199 nicht aktiviert ist, sobald der Upgradevorgang abgeschlossen ist.  

> [!NOTE]
> Das Ablaufverfolgungsflag 4199 ist jedoch weiterhin erforderlich, um alle neuen Abfrageprozessor-Problembehebungen zu aktivieren, die nach RTM freigegeben wurden (sofern zutreffend).
  
Der empfohlene Workflow für eine Aktualisierung des Abfrageprozessors auf die neueste Version des Codes ist in den „Verwendungsszenarien für den Abfragespeicher“ unter [Aufrechterhalten einer stabilen Leistung während des Upgrades auf das neuere SQL Server](../../relational-databases/performance/query-store-usage-scenarios.md#CEUpgrade) dokumentiert (siehe weiter unten).  
  
![Abfrage-Store-Nutzung-5](../../relational-databases/performance/media/query-store-usage-5.png "query-store-usage-5") 
 
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Anzeigen oder Ändern des Kompatibilitätsgrads einer Datenbank](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)  
 [Verwendungsszenarios für den Abfragespeicher](../../relational-databases/performance/query-store-usage-scenarios.md) 
  

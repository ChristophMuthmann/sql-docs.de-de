---
title: Verwalten des Transaktionsumfangs | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 82900342-bc80-445f-98a4-468a303aae1e
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c36592d2460dca27a172be763ef2cd289b6571f8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="managing-transaction-size"></a>Verwalten des Transaktionsumfangs
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Wenn Sie mit Transaktionen arbeiten, ist es wichtig, die Transaktionen so kurz wie möglich zu halten. Der Standardmodus Auto-Commit, aktivieren oder deaktivieren, indem Sie mit der [SetAutoCommit](../../connect/jdbc/reference/setautocommit-method-sqlserverconnection.md) -Methode, führt ein commit für jede Aktion. Dies ist der Modus, mit dem die meisten Entwickler am bequemsten arbeiten können.  
  
 Wenn Sie manuelle Transaktionen verwenden, stellen Sie sicher, dass im Code so schnell wie möglich ein Commit für die Transaktion ausgeführt wird. Durch das Offenhalten einer Transaktion wird blockiert, dass andere Benutzer auf die Daten zugreifen können. Es ist beispielsweise ein gutes Programmierverfahren, einen rollback-Aufruf im catch-Block und einen commit-Aufruf im finally-Block einzufügen. Dies ist jedoch vom Entwurf der Anwendung abhängig.  
  
 Wenn der Umfang der Transaktionen klein gehalten wird, führt dies zu einer besseren Parallelität. Wenn Sie beispielsweise eine manuelle Transaktion beginnen und 10.000 Zeilen in einer Tabelle mit 20.000 Zeilen ändern, ist die Hälfte der Tabelle für alle anderen Benutzer blockiert, auch wenn sie die Daten nur lesen. Durch das Reduzieren der Änderungen auf 2.000 Zeilen bleiben 90 Prozent der Tabelle verfügbar.  
  
 Stellen Sie außerdem sicher, dass Sie die Timeouteinstellung für Sperren verwenden, wenn die Anwendung Probleme mit Sperren erwartet und hierfür Timeouts benötigt. Sie erreichen dies, indem die [SetLockTimeout](../../connect/jdbc/reference/setlocktimeout-method-sqlserverdatasource.md) Methode. Der Standardwert für das Sperrtimeout ist -1. Dies bedeutet, dass beim Warten auf die Sperre unendlich lang blockiert wird. Sie können das Sperrtimeout auf 30 Sekunden festlegen. So tritt bei der gesperrten Verbindung nach 30 Sekunden ein Timeout auf, wenn eine Blockierung durch eine andere Verbindung vorliegt.  
  
## <a name="see-also"></a>Siehe auch  
 [Verbessern von Leistung und Zuverlässigkeit mit dem JDBC-Treiber](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  

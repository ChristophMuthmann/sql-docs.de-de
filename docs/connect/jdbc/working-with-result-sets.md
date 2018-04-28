---
title: Arbeiten mit Resultsets | Microsoft Docs
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
ms.topic: article
ms.assetid: 4fc4b1c6-3075-4ad7-9244-865d9ede7ae6
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 815a8f481141fac0d2c834cdd3a663fa2609b3b4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="working-with-result-sets"></a>Arbeiten mit Resultsets
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Beim Arbeiten mit den Daten in einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank, eine Methode zum Bearbeiten der Daten ist die Verwendung ein Resultsets. Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] unterstützt die Verwendung von Resultsets legt, über fest die [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt. Mithilfe des SQLServerResultSet-Objekts, können Sie von einer SQL-Anweisung oder gespeicherten Prozedur zurückgegebenen Daten abrufen, aktualisieren Sie die Daten nach Bedarf und dann persistent gespeichert, dass die Daten in der Datenbank zurück.  
  
 Darüber hinaus bietet das SQLServerResultSet-Objekt Methoden zum Navigieren durch die Datenzeilen, Abrufen oder Festlegen der darin enthaltenen Daten und die Sensitivität gegenüber Änderungen in der zugrunde liegenden Datenbank einzurichten.  
  
> [!NOTE]  
>  Weitere Informationen zur Verwaltung von Resultsets, einschließlich deren Sensitivität gegenüber Änderungen, finden Sie unter [Verwalten von Resultsets mit dem JDBC-Treiber](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md).  
  
 Die Themen in diesem Abschnitt beschreiben verschiedene Möglichkeiten, die Sie einem Resultset verwenden können, die in enthaltenen Daten bearbeiten einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[Abrufen von Resultsetdaten – Beispiel](../../connect/jdbc/retrieving-result-set-data-sample.md)|Beschreibt, wie ein Resultset zum Abrufen von Daten aus einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank, und zeigen Sie es.|  
|[Ändern von Resultsetdaten – Beispiel](../../connect/jdbc/modifying-result-set-data-sample.md)|Beschreibt die Verwendung eines Resultsets zum Einfügen, abrufen und Ändern von Daten in einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank.|  
|[Zwischenspeichern von Resultsetdaten – Beispiel](../../connect/jdbc/caching-result-set-data-sample.md)|Beschreibt, wie ein Resultset zum Abrufen großer Datenmengen von einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank, und um zu steuern, wie die Daten auf dem Client zwischengespeichert werden.|  
  
## <a name="see-also"></a>Siehe auch  
 [Beispiele für JDBC-Treiberanwendungen](../../connect/jdbc/sample-jdbc-driver-applications.md)  
  
  

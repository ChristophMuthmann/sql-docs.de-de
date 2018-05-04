---
title: Herstellen einer Verbindung und zum Abrufen von Daten | Microsoft Docs
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
ms.assetid: ce43cc20-46a3-42ff-a3fb-75ad1ed10e08
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cd98a0b7954f5b67bedbaa09833b72d8f5914921
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="connecting-and-retrieving-data"></a>Verbinden und Abrufen von Daten
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Bei der Arbeit mit der [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], es gibt zwei primäre Methoden zum Herstellen einer Verbindungs mit einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank. Eine Verbindungseigenschaften in der Verbindungs-URL festzulegen, und rufen Sie anschließend die GetConnection-Methode der zurückzugebenden DriverManager-Klasse ist eine [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) Objekt.  
  
> [!NOTE]  
>  Eine Liste der vom JDBC-Treiber unterstützten Verbindungseigenschaften finden Sie [Festlegen der Verbindungseigenschaften](../../connect/jdbc/setting-the-connection-properties.md).  
  
 Die zweite Methode werden die Verbindungseigenschaften mit den festlegungsmethoden des der [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) -Klasse, und dem anschließenden Aufrufen der [GetConnection](../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md) Methode, um ein SQLServerConnection zurückzugeben. -Objekt.  
  
 Die Themen in diesem Abschnitt beschreiben die verschiedenen Möglichkeiten, in dem Sie können eine Verbindung mit, einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank, und sie zeigen auch verschiedene Techniken zum Abrufen von Daten.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[Verbindungs-URL – Beispiel](../../connect/jdbc/connection-url-sample.md)|Beschreibt, wie eine Verbindungs-URL für die Verbindung [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] und verwenden Sie eine SQL-Anweisung zum Abrufen von Daten.|  
|[Beispiel für Datenquellen](../../connect/jdbc/data-source-sample.md)|Beschreibt die Verwendung einer Datenquelle, um eine Verbindung zu SQL Server herzustellen und Daten anschließend mit einer gespeicherten Prozedur abzurufen.|  
  
## <a name="see-also"></a>Siehe auch  
 [Beispiele für JDBC-Treiberanwendungen](../../connect/jdbc/sample-jdbc-driver-applications.md)  
  
  

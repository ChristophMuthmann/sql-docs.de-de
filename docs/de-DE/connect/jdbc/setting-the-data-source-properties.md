---
title: Festlegen der Data Datenquelleneigenschaften | Microsoft Docs
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
ms.assetid: f3363d05-07fc-4bf8-ae5e-2a7a968808ad
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 707cd603132e84b0e6712ac18fad0ebfbb6b2bec
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="setting-the-data-source-properties"></a>Festlegen der Datenquelleneigenschaften
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Datenquellen bilden den bevorzugten Mechanismus, mit dem in einer Umgebung der Java-Plattform, Enterprise Edition (Java EE) JDBC-Verbindungen erstellt werden. Datenquellen ermöglichen Verbindungen, Poolverbindungen und verteilte Verbindungen, ohne die Verbindungseigenschaften fest im Java-Code codieren zu müssen. Alle [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] Datenquellen festlegen oder den Wert einer beliebigen Eigenschaft abrufen, indem Sie mit den entsprechenden Abruf-Abrufmethoden, bzw. können.  
  
 Java EE-Produkte wie Anwendungsserver und Servlet-/JSP-Engines lassen normalerweise die Konfiguration von Datenquellen für den Datenbankzugriff zu. Jede Eigenschaft aufgeführt, die der [Festlegen der Verbindungseigenschaften](../../connect/jdbc/setting-the-connection-properties.md) Thema kann angegeben werden, immer, wenn die Konfiguration können Sie eine Eigenschaft als Eigenschaft geben Sie = Wert-Paar.  
  
 Weitere Informationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Datenquellen finden Sie unter der [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) Klasse. Ein Beispiel dafür, wie die SQLServerDataSource-Klasse verwendet wird, zum Herstellen einer Verbindung mit einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] finden Sie unter [-Datenquellenbeispiel](../../connect/jdbc/data-source-sample.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Verbinden von SQL Server mit dem JDBC-Treiber](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  

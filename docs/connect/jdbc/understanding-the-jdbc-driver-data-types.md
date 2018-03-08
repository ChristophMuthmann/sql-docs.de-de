---
title: Grundlegendes zu den Datentypen des JDBC-Treiber | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7802328d-4d23-4775-9573-4169b127d258
caps.latest.revision: "27"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 1c9599a6e71ee0fbf171ba9c8619cafac8332cc5
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="understanding-the-jdbc-driver-data-types"></a>Grundlegendes zu den Datentypen in JDBC Driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]unterstützt die Verwendung von JDBC grundlegenden und erweiterten Datentypen in einer Java-Anwendung, verwendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] als Datenbank.  
  
 Der JDBC-Typsystem vermittelt die Konvertierung zwischen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Datentypen und Java-Typen und Objekte. Die JDBC-Typen beruhen auf den SQL-92- und SQL-99-Typen. Der JDBC-Treiber befolgt die JDBC-Spezifikation und stellt eine optimale Balance zwischen Vorhersehbarkeit und Flexibilität bereit.  
  
 Die Themen in diesem Abschnitt beschreiben die Verwendung der grundlegenden und erweiterten Datentypen sowie das Konvertieren der Datentypen in andere Datentypen.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[Verwenden von Standarddatentypen](../../connect/jdbc/using-basic-data-types.md)|Beschreibt die grundlegenden JDBC-Datentypen. Umfasst Beispiele zum Arbeiten mit den Datentypen mithilfe von Resultsets, parametrisierten Abfragen und gespeicherten Prozeduren.|  
|[Konfigurieren der Art und Weise, wie java.sql.Time-Werte an den Server gesendet werden](../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)|Beschreibt die Generierung von Datumsangaben durch den JDBC-Treiber.|  
|[Verwenden von erweiterten Datentypen](../../connect/jdbc/using-advanced-data-types.md)|Beschreibt die erweiterten JDBC-Datentypen.|  
|[Grundlegendes zu den Unterschieden von Datentypen](../../connect/jdbc/understanding-data-type-differences.md)|Beschreibt Unterschiede zwischen den verschiedenen Datentypen des JDBC-Treibers.|  
|[Grundlegendes zu Datentypkonvertierungen](../../connect/jdbc/understanding-data-type-conversions.md)|Beschreibt, wie die Datentypkonvertierung bei der Verwendung von Methoden zum Festlegen und Abrufen behandelt wird.|  
|[Unterstützung für nationale Zeichensätze](../../connect/jdbc/national-character-set-support.md)|Beschreibt die Unterstützung der Typen für nationale Zeichensätze.|  
|[Unterstützen von XML-Daten](../../connect/jdbc/supporting-xml-data.md)|Beschreibt die SQLXML-Schnittstelle. Außerdem wird beschrieben, wie zum Lesen und Schreiben von XML-Daten in bzw. aus einer relationalen Datenbank mit der **SQLXML** Java-Datentyp.|  
|[Wrapper und Schnittstellen](../../connect/jdbc/wrappers-and-interfaces.md)|Behandelt die Schnittstellen, die über die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] -spezifischen Methoden und Konstanten, mit denen einen Anwendungsserver einen Proxy der Klasse erstellen können außerdem unterstützungen für die java.sql.Wrapper-Schnittstelle.|  
  
## <a name="see-also"></a>Siehe auch  
 [Overview of the JDBC Driver (Übersicht über den JDBC-Treiber)](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  

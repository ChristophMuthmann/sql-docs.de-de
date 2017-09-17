---
title: "Unterstützung von XML-Daten | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 32b7217e-1f0c-473d-9a45-176daa81584e
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5f561c72cda30a9f62e202cbd612725d02b7f408
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="supporting-xml-data"></a>Unterstützen von XML-Daten
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Stellt eine **Xml** -Datentyp, der ermöglicht Ihnen das Speichern von XML-Dokumenten und-Fragmenten in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank. Die **Xml** -Datentyp ist ein integrierter Datentyp in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], und einige auf ähnliche Weise wie andere integrierten Typen wie **Int** und **Varchar**. Wie andere integrierten Typen können Sie die **Xml** -Datentyp als: Geben Sie einen Variablentyp, Parametertyp, einen Funktionsrückgabetyp oder einer Spalte beim Erstellen einer Tabelle oder in [!INCLUDE[tsql](../../includes/tsql_md.md)] Funktionen CAST und CONVERT. In der JDBC-Treiber die **Xml** -Datentyp kann als Zeichenfolge, Byte-Array, Datenstrom, CLOB-, BLOB- oder SQLXML-Objekt zugeordnet werden. Die Standardzuordnung ist als Zeichenfolge.  
  
 Der JDBC-Treiber bietet Unterstützung für die JDBC 4.0-API, in der die SQLXML-Schnittstelle eingeführt wird. Die SQLXML-Schnittstelle definiert Methoden für die Interaktion mit und die Bearbeitung von XML-Daten. Die **SQLXML** ist ein JDBC 4.0-Datentyp und ordnet es die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **Xml** -Datentyp. Um den SQLXML-Datentyp in der Anwendung verwenden zu können, müssen Sie daher den Klassenpfad so festlegen, dass die Datei „sqljdbc4.jar“ enthalten ist. Wenn die Anwendung beim Zugriff auf das SQLXML-Objekt und seine Methoden versucht, „sqljdbc3.jar“ zu verwenden, wird eine Ausnahme ausgelöst.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]die XML-Daten wird immer überprüft, bevor sie in der Datenbankspalte gespeichert werden. Anwendungen können **SQLXML** -Datentyp, da der JDBC-Treiber eine Zuordnung der **Xml** Datentyp automatisch. Die **SQLXML** Support ist in "sqljdbc4.jar" verfügbar. Finden Sie unter [Systemanforderungen für JDBC Driver](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md) für die Liste der vom unterstützten JRE-Versionen der [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].  
  
 Die Themen in diesem Abschnitt beschreiben die SQLXML-Schnittstelle und die Programmierung der **SQLXML** -Datentyp mit den JDBC-API-Methoden.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[SQLXML-Schnittstelle](../../connect/jdbc/sqlxml-interface.md)|Beschreibt die SQLXML-Schnittstelle und ihre Methoden.|  
|[Programmieren mit SQLXML](../../connect/jdbc/programming-with-sqlxml.md)|Beschreibt, wie die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] API-Methoden zum Speichern und Abrufen von XML-Daten in bzw. aus einer relationalen Datenbank mit der **SQLXML** Java-Datentyp. Außerdem sind Informationen über die Typen von SQLXML-Objekten und eine Liste wichtiger Richtlinien und Einschränkungen für die Verwendung von SQLXML-Objekten enthalten.|  
  
## <a name="see-also"></a>Siehe auch  
 [Grundlegendes zu den Datentypen des JDBC-Treiber](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  

---
title: Verwenden von Parametermetadaten | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
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
ms.assetid: db2c1957-91c6-4989-a07b-9f8be6d2033a
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1a8d71bb60e5efa5289a03c9ca8ab59dc183e91f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="using-parameter-metadata"></a>Verwenden von Parametermetadaten
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Abfrage eine [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) oder ein [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) Objekt zu den Parametern, die sie enthalten, die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] implementiert die [ SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md) Klasse. Diese Klasse enthält eine Vielzahl von Feldern und Methoden, die Informationen in der Form eines einzelnen Werts zurückgeben.  
  
 Um ein SQLServerParameterMetaData-Objekt zu erstellen, können Sie die [GetParameterMetaData](../../connect/jdbc/reference/getparametermetadata-method-sqlserverpreparedstatement.md) der Sqlserverpreparedstatement- und SQLServerCallableStatement-Klasse.  
  
 Im folgenden Beispiel wird eine offene Verbindung mit dem [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] -Beispieldatenbank an die Funktion übergeben, die GetParameterMetaData-Methode der SQLServerCallableStatement-Klasse wird verwendet, um ein SQLServerParameterMetaData-Objekt, und klicken Sie dann verschiedenen zurückgeben Methoden, die von der SQLServerParameterMetaData-Objekt dienen zum Anzeigen von Informationen zu Typ und Modus der Parameter, die in der gespeicherten Prozedur HumanResources.uspUpdateEmployeeHireInfo enthalten sind.  
  
 [!code[JDBC#UsingParamMetaData1](../../connect/jdbc/codesnippet/Java/using-parameter-metadata_1.java)]  
    
> [!NOTE]  
Es gibt einige Einschränkungen bei die SQLServerParameterMetaData-Klasse mit vorbereiteten Anweisungen verwendet. 
**Mit Microsoft JDBC Driver 6.0 (oder höher) für SQL Server**: bei Verwendung von SQL Server 2008 oder 2008 R2 unterstützt der JDBC-Treiber SELECT, DELETE, INSERT und UPDATE-Anweisungen, solange diese Anweisungen enthält keine Unterabfragen.  

Abfragen ZUSAMMENFÜHREN werden auch nicht für die SQLServerParameterMetaData-Klasse unterstützt, bei Verwendung von SQL Server 2008 oder 2008 R2. Bei SQL Server 2012 und höheren werden Parametermetadaten in komplexen Abfragen unterstützt.  

Abrufen von Parametermetadaten für verschlüsselte Spalten werden nicht unterstützt. **Mit Microsoft JDBC Driver 4.1 und 4.2 für SQL Server**: der JDBC-Treiber unterstützt SELECT, DELETE, INSERT und UPDATE-Anweisungen aus, solange diese Anweisungen enthält keine Unterabfragen. Abfragen ZUSAMMENFÜHREN, werden auch nicht für die SQLServerParameterMetaData-Klasse unterstützt.  
  
  

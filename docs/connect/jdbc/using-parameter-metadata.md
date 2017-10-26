---
title: Verwenden von Parametermetadaten | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: db2c1957-91c6-4989-a07b-9f8be6d2033a
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d50af4d0d22d6042230fed2ee6b989fb7c53408d
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-parameter-metadata"></a>Verwenden von Parametermetadaten
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Abfrage eine [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) oder ein [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) Objekt zu den Parametern, die sie enthalten, die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] implementiert die [ SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md) Klasse. Diese Klasse enthält eine Vielzahl von Feldern und Methoden, die Informationen in der Form eines einzelnen Werts zurückgeben.  
  
 Um ein SQLServerParameterMetaData-Objekt zu erstellen, können Sie die [GetParameterMetaData](../../connect/jdbc/reference/getparametermetadata-method-sqlserverpreparedstatement.md) der Sqlserverpreparedstatement- und SQLServerCallableStatement-Klasse.  
  
 Im folgenden Beispiel wird eine offene Verbindung mit dem [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] -Beispieldatenbank an die Funktion übergeben, die GetParameterMetaData-Methode der SQLServerCallableStatement-Klasse wird verwendet, um ein SQLServerParameterMetaData-Objekt, und klicken Sie dann verschiedenen zurückgeben Methoden, die von der SQLServerParameterMetaData-Objekt dienen zum Anzeigen von Informationen zu Typ und Modus der Parameter, die in der gespeicherten Prozedur HumanResources.uspUpdateEmployeeHireInfo enthalten sind.  
  
 [!code[JDBC#UsingParamMetaData1](../../connect/jdbc/codesnippet/Java/using-parameter-metadata_1.java)]  
    
> [!NOTE]  
Es gibt einige Einschränkungen bei die SQLServerParameterMetaData-Klasse mit vorbereiteten Anweisungen verwendet. 
**Mit Microsoft JDBC Driver 6.0 (oder höher) für SQL Server**: bei Verwendung von SQL Server 2008 oder 2008 R2 unterstützt der JDBC-Treiber SELECT, DELETE, INSERT und UPDATE-Anweisungen, solange diese Anweisungen enthält keine Unterabfragen. Abfragen ZUSAMMENFÜHREN werden auch nicht für die SQLServerParameterMetaData-Klasse unterstützt, bei Verwendung von SQL Server 2008 oder 2008 R2. Bei SQL Server 2012 und höheren werden Parametermetadaten in komplexen Abfragen unterstützt. Abrufen von Parametermetadaten für verschlüsselte Spalten werden nicht unterstützt. **Mit Microsoft JDBC Driver 4.0, 4.1 und 4.2 für SQL Server**: der JDBC-Treiber unterstützt SELECT, DELETE, INSERT und UPDATE-Anweisungen aus, solange diese Anweisungen enthält keine Unterabfragen. Abfragen ZUSAMMENFÜHREN, werden auch nicht für die SQLServerParameterMetaData-Klasse unterstützt.  

## <a name="see-also"></a>Siehe auch  
 [Verarbeiten von Metadaten mit dem JDBC-Treiber](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)  
  
  


---
title: Abrufen der Treiberversion | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5e241d72-16da-4ada-ac67-e6308394108f
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b7578539a178e76796018d2da307381318414cb0
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2018
---
# <a name="getting-the-driver-version"></a>Abrufen der Treiberversion
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Die installierte Version von [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] finden Sie auf folgende Weise:  
  
-   Rufen Sie die [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) Methoden [GetDriverMajorVersion](../../connect/jdbc/reference/getdrivermajorversion-method-sqlserverdatabasemetadata.md), [GetDriverMinorVersion](../../connect/jdbc/reference/getdriverminorversion-method-sqlserverdatabasemetadata.md), oder [GetDriverVersion](../../connect/jdbc/reference/getdriverversion-method-sqlserverdatabasemetadata.md).  
  
-   Die Version wird in der Datei readme.txt für das Produkt angezeigt.  
  
 Darüber hinaus kann der JDBC-Treibername von zurückgegeben werden die [GetDriverName](../../connect/jdbc/reference/getdrivername-method-sqlserverdatabasemetadata.md) Methodenaufruf in der SQLServerDatabaseMetaData-Klasse. Es gibt z. B. "Microsoft JDBC Driver 6.4 für SQL Server" zurück.  
  
 Im folgenden finden ein Beispiel der Ausgabe von Aufrufen an die Methode der SQLServerDatabaseMetaData-Klasse:  
  
 `getDriverName = Microsoft JDBC Driver 6.4 for SQL Server`  
  
 `getDriverMajorVersion = 6`  
  
 `getDriverMinorVersion = 4`  
  
 `getDriverVersion = 6.4.` *xxx.x*  
  
 Dabei ist "xxx.x" die abschließende Versionsnummer.  
  
## <a name="see-also"></a>Siehe auch  
 [Diagnostizieren von Problemen mit dem JDBC-Treiber](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  

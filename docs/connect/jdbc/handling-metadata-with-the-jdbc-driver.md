---
title: Verarbeiten von Metadaten mit dem JDBC-Treiber | Microsoft Docs
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
ms.assetid: 5cfb35d4-ddcd-40a2-8091-f29cddc32552
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 63d691c8bef93ad734a7596532ba567708128a2d
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="handling-metadata-with-the-jdbc-driver"></a>Verarbeiten von Metadaten mit dem JDBC-Treiber
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] dienen zum Verarbeiten von Metadaten in einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank in einer Vielzahl von Möglichkeiten. Mit dem JDBC-Treiber können Metadaten zur Datenbank, zu einem Resultset oder zu Parametern abgerufen werden.  
  
 Der JDBC-Treiber umfasst drei Klassen zum Abrufen von Metadaten aus einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank:  
  
-   [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md), der verwendet wird, die Informationen zur Datenbank zurückzugeben, die derzeit verbunden ist.  
  
-   [SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md), der verwendet wird, die Informationen über das Resultset zurückgegeben.  
  
-   [SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md), der verwendet wird, die Informationen über die Parameter vorbereiteter und aufrufbarer Anweisungen zurück.  
  
 Die Themen in diesem Abschnitt werden erläutert, wie Sie die drei Metadatenklassen können zum Verarbeiten von Metadaten in einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank.  
  
> [!NOTE]  
>  Die in diesem Abschnitt behandelten Metadatenmethoden wirken sich im Allgemeinen erheblich auf die Leistung der Anwendung aus, sodass deren Verwendung sorgfältig abgewägt werden muss.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[Verwenden von Datenbankmetadaten](../../connect/jdbc/using-database-metadata.md)|Beschreibt das Abrufen von Metadateninformationen über die zurzeit verbundene Datenbank.|  
|[Verwenden von Resultsetmetadaten](../../connect/jdbc/using-result-set-metadata.md)|Beschreibt das Abrufen von Metadateninformationen über das aktuelle Resultset.|  
|[Verwenden von Parametermetadaten](../../connect/jdbc/using-parameter-metadata.md)|Beschreibt das Abrufen von Metadateninformationen über die Parameter vorbereiteter und aufrufbarer Anweisungen.|  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über die JDBC-Treiber](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  


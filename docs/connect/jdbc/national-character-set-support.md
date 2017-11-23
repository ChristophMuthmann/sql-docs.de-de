---
title: "Unterstützung für nationale Zeichensätze | Microsoft Docs"
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
ms.assetid: 4fceacfd-df4f-40cd-b7a2-5e5e58a5979f
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9be09b40e72a19a498913bf824e73b52db6596a2
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="national-character-set-support"></a>Unterstützung für nationale Zeichensätze
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Der JDBC-Treiber bietet Unterstützung für die JDBC 4.0-API, die neue API-Methoden für die Konvertierung nationaler Zeichensätze enthält. Diese Unterstützung beinhaltet neue Setter, Getter und Updater-Methoden für **NCHAR**, **NVARCHAR**, **LONGNVARCHAR**, und **NCLOB** JDBC-Typen.  
  
 In der folgenden Liste sind die Methoden zum Abrufen, Festlegen und Aktualisieren für die Unterstützung der Konvertierung nationaler Zeichensätze aufgeführt:  
  
-   [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md): [SetNString](../../connect/jdbc/reference/setnstring-method-int-java-lang-string.md), [SetNCharacterStream](../../connect/jdbc/reference/setncharacterstream-method-sqlserverpreparedstatement.md), [SetNClob](../../connect/jdbc/reference/setnclob-method-sqlserverpreparedstatement.md).  
  
-   [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md): [GetNClob](../../connect/jdbc/reference/getnclob-method-sqlservercallablestatement.md), [GetNString](../../connect/jdbc/reference/getnstring-method-sqlservercallablestatement.md), [GetNCharacterStream](../../connect/jdbc/reference/getncharacterstream-method-sqlservercallablestatement.md), [SetNString](../../connect/jdbc/reference/setnstring-method-sqlservercallablestatement.md), [SetNCharacterStream](../../connect/jdbc/reference/setncharacterstream-method-sqlservercallablestatement.md), [SetNClob](../../connect/jdbc/reference/setnclob-method-sqlservercallablestatement.md).  
  
-   [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md): [GetNClob](../../connect/jdbc/reference/getnclob-method-sqlserverresultset.md), [GetNString](../../connect/jdbc/reference/getnstring-method-sqlserverresultset.md), [GetNCharacterStream](../../connect/jdbc/reference/getncharacterstream-method-sqlserverresultset.md), [UpdateNClob](../../connect/jdbc/reference/updatenclob-method-sqlserverresultset.md), [UpdateNString](../../connect/jdbc/reference/updatenstring-method-sqlserverresultset.md), [UpdateNCharacterStream](../../connect/jdbc/reference/updatencharacterstream-method-sqlserverresultset.md).  
  
> [!NOTE]  
>  Um diese Methoden in einer Anwendung verwenden zu können, müssen Sie den Klassenpfad so festlegen, dass die Datei „sqljdbc4.jar“ enthalten ist.  
  
 Damit String-Parameter im Unicode-Format an den Server gesendet werden, sollten die Anwendungen entweder die neuen JDBC 4.0-Methoden für nationale Zeichensätze verwenden. oder legen Sie die **SendStringParametersAsUnicode** Verbindungseigenschaft auf "**" true "**" Wenn Sie die Methoden für nicht nationale Zeichensätze verwenden. Es wird empfohlen, nach Möglichkeit die neuen JDBC 4.0-Methoden für nationale Zeichensätze zu verwenden. Weitere Informationen zu den **SendStringParametersAsUnicode** Verbindungseigenschaft finden Sie unter [Festlegen der Verbindungseigenschaften](../../connect/jdbc/setting-the-connection-properties.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Grundlegendes zu den Datentypen in JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  

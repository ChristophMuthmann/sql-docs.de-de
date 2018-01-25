---
title: Zuordnen eines Anweisungshandles | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-queries
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQLSetStmtAttr function
- statements [ODBC], statement handles
- ODBC applications, executing queries
- SQLGetStmtAttr function
- SQL Server Native Client ODBC driver, statements
- allocating statement handles
- ODBC applications, statements
- statement handles [ODBC]
- SQLAllocHandle function
ms.assetid: 9ee207f3-2667-45f5-87ca-e6efa1fd7a5c
caps.latest.revision: "30"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bc701ff4419fdb60f2b954333aa2af7ec9845521
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="allocating-a-statement-handle"></a>Zuordnen eines Anweisungshandles
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Bevor eine Anwendung eine Anweisung ausführen kann, muss sie ein Anweisungshandle zuordnen. Dies geschieht durch Aufrufen von **SQLAllocHandle** mit der *HandleType* -Parameter auf SQL_HANDLE_STMT festgelegt und *InputHandle* auf ein Verbindungshandle zeigt.  
  
 Anweisungsattribute sind Eigenschaften des Anweisungshandles. Beispielanweisungsattribute können die Verwendung von Lesezeichen und den mit dem Resultset der Anweisung zu verwendenden Cursor beinhalten. Anweisungsattribute werden mit festgelegt [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md), und ihre aktuellen Einstellungen werden abgerufen, indem [SQLGetStmtAttr](../../relational-databases/native-client-odbc-api/sqlgetstmtattr.md). Es ist nicht erforderlich, dass eine Anwendung Anweisungsattribute festlegt; alle Anweisungsattribute haben Standardwerte und einige sind treiberspezifisch.  
  
 Gehen Sie bei der Verwendung mehrere ODBC-Anweisungs- und -Verbindungsoptionen vorsichtig vor. Aufrufen von [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) mit *fOption* auf SQL_ATTR_LOGIN_TIMEOUT Steuerelemente den Zeitraum festlegen, die eine Anwendung ein Verbindungsversuch mit Timeout beim Warten auf das Herstellen einer Verbindung (0 wartet Gibt eine unbegrenzte Wartezeit). Für Sites mit langen Reaktionszeiten kann hierfür ein hoher Wert festgelegt werden, um sicherzustellen, dass zum Herstellen von Verbindungen ausreichend Zeit eingeräumt wird. Jedoch sollte das Intervall stets so niedrig sein, dass der Benutzer nach einer angemessenen Zeitspanne benachrichtig wird, wenn der Treiber keine Verbindung herstellen kann.  
  
 Aufrufen von **SQLSetStmtAttr** mit *fOption* auf SQL_ATTR_QUERY_TIMEOUT festgelegt ist, legt ein abfragetimeoutintervall zum Schutz der Server und der Benutzer von langwierigen Abfragen.  
  
 Aufrufen von **SQLSetStmtAttr** mit *fOption* auf SQL_ATTR_MAX_LENGTH festgelegt ist, schränkt die Menge der **Text** und **Image** Daten, die ein einzelne Anweisung abrufen kann. Aufrufen von **SQLSetStmtAttr** mit *fOption* auf SQL_ATTR_MAX_ROWS festgelegt beschränkt außerdem ein Rowset mit dem ersten  *n*  Zeilen ist, die alle für die Anwendung benötigt. Beachten Sie, dass das Festlegen von SQL_ATTR_MAX_ROWS bewirkt, dass der Treiber eine SET ROWCOUNT-Anweisung an den Server ausgibt. Dies wirkt sich auf alle [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anweisungen, z. B. Trigger und Updates.  
  
 Gehen Sie beim Festlegen dieser Optionen vorsichtig vor. Im Idealfall sollten alle Anweisungshandle eines Verbindungshandles die gleichen Einstellungen für SQL_ATTR_MAX_LENGTH und SQL_ATTR_MAX_ROWS aufweisen. Wenn der Treiber von einem Anweisungshandle zu einem anderen mit abweichenden Werten für diese Optionen wechselt, muss der Treiber die entsprechenden SET TEXTSIZE- und SET ROWCOUNT-Anweisungen generieren, um die Einstellungen zu ändern. Der Treiber kann diese Anweisungen nicht dem gleichen Batch zuordnen, in dem sich auch die SQL-Anweisung des Benutzers befindet, da die SQL-Anweisung des Benutzers eine Anweisung enthalten kann, die die erste Anweisung in einem Batch darstellen muss. Der Treiber muss die Anweisungen SET TEXTSIZE und SET ROWCOUNT in einem separaten Batch senden, der automatisch einen zusätzlichen Roundtrip zum Server generiert.  
  
## <a name="see-also"></a>Siehe auch  
 [Ausführen von Abfragen &#40; ODBC &#41;](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  

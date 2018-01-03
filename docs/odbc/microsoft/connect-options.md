---
title: "Optionen für die verbindungsherstellung | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connection options [ODBC]
- ODBC driver for Oracle [ODBC], connection options
- custom connection options [ODBC]
ms.assetid: abfdc133-cb33-435f-a467-fbe15444f687
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8ae5a9e91e76608b46daf7f0bf5f532f30141cff
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="connect-options"></a>Optionen für die verbindungsherstellung
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden. Verwenden Sie stattdessen den ODBC-Treiber von Oracle bereitgestellt.  
  
 Diese Optionen ermöglichen die Anpassung der Verbindung mit der Datenbank innerhalb einer Anwendung.  
  
|Verbindungsoption|Hinweise|  
|--------------------|-----------|  
|SQL_AUTOCOMMIT|Bei Auswahl von SQL_AUTOCOMMIT_OFF festlegen, die Anwendung muss explizit einen commit oder Rollback Transaktionen mit [SQLTransact](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md).|  
|SQL_ODBC_CURSORS|Dieses Verbindungsattribut wird in der Treiber-Manager implementiert.|  
|SQL_OPT_TRACE|Dieses Verbindungsattribut wird in der Treiber-Manager implementiert.|  
|SQL_OPT_TRACEFILE|Dieses Verbindungsattribut wird in der Treiber-Manager implementiert.|  
|SQL_TRANSLATE_DLL|Gibt Fehler zurück: "Treiber nicht unterstützt."|  
|SQL_TRANSLATE_OPTION|Ein 32-Bit-Wert mit der Übersetzung-DLL übergeben.|  
|SQL_TXN_ISOLATION|Der Treiber kann nur SQL_TXN_READ_COMMITTED.<br /><br /> Die folgenden vParams werden nicht unterstützt:<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE FESTGELEGT SIND|  
|SQL_ATTR_ENLIST_IN_DTC|Dieses Verbindungsattribut ODBC 3.0 ermöglicht Ihnen die Verwendung der ODBC-Treiber für Oracle in verteilten Transaktionen von Microsoft Component Services (oder MTS, bei Verwendung von Windows NT) koordiniert. Es stellt den Schnittstellenzeiger *pITransaction* für die Transaktion als die *vParam* Argument.|  
|SQL_ATTR_CONNECTION_DEAD|Diese schreibgeschützte ODBC 3.5-Verbindungsattribut können Sie bestimmen, ob die Verbindung mit dem Oracle-Server fehlgeschlagen ist. Nur abgerufen werden. kann nicht festgelegt.|

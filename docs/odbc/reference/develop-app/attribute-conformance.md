---
title: "-Attribut Konformität | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
- conformance levels [ODBC], attribute
- attribute conformance levels [ODBC]
ms.assetid: 34fea100-10f9-46d5-bc50-3aa867b70f24
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9d615371a5bcf305158cb5f29c22a087110f95ac
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="attribute-conformance"></a>Attribut-Konformität
In der folgenden Tabelle gibt an, dem Konformitätsgrad jedes Attributs ODBC-Umgebung, in denen dies gut definiert ist.  
  
|Funktion|Konformitätsgrad|  
|--------------|-----------------------|  
|SQL_ATTR_CONNECTION_POOLING|--[1]|  
|SQL_ATTR_CP_MATCH|--[1]|  
|SQL_ATTR_ODBC_VER|Core|  
|SQL_ATTR_OUTPUT_NTS|--[1]|  
  
 [1]. Dies ist ein optionales Feature und als solche ist nicht Teil der Übereinstimmungsebenen.  
  
 In der folgenden Tabelle gibt an, dem Konformitätsgrad jede ODBC-Verbindungsattribut, in denen dies gut definiert ist.  
  
|Funktion|Konformitätsgrad|  
|--------------|-----------------------|  
|SQL_ATTR_ACCESS_MODE|Core|  
|SQL_ATTR_ASYNC_ENABLE|Ebene 1/Level 2 [1]|  
|SQL_ATTR_AUTO_IPD|Ebene 2|  
|SQL_ATTR_AUTOCOMMIT|Ebene 1|  
|SQL_ATTR_CONNECTION_DEAD|Ebene 1|  
|SQL_ATTR_CONNECTION_TIMEOUT|Ebene 2|  
|SQL_ATTR_CURRENT_CATALOG|Ebene 2|  
|SQL_ATTR_LOGIN_TIMEOUT|Ebene 2|  
|SQL_ATTR_ODBC_CURSORS|Core|  
|SQL_ATTR_PACKET_SIZE|Ebene 2|  
|SQL_ATTR_QUIET_MODE|Core|  
|SQL_ATTR_TRACE|Core|  
|SQL_ATTR_TRACEFILE|Core|  
|SQL_ATTR_TRANSLATE_LIB|Core|  
|SQL_ATTR_TRANSLATE_OPTION|Core|  
|SQL_ATTR_TXN_ISOLATION|Ebene 1/Level 2 [2]|  
  
 [1]-Anwendungen, die Verbindungsebene Asynchronie (erforderlich für Ebene 1) unterstützen müssen unterstützen Festlegen dieses Attributs auf SQL_TRUE durch Aufrufen von **SQLSetConnectAttr**; das Attribut nicht auf einen anderen Wert als den Standardwert festgelegt sein muss Wert über **SQLSetStmtAttr**. Anwendungen, die auf Anweisungsebene Asynchronie (erforderlich für Ebene 2) unterstützen müssen durch Festlegen dieses Attributs auf SQL_TRUE, die mit einer Funktion unterstützen.  
  
 [2] für Ebene-1-Schnittstelle-Konformität der Treiber muss einen Wert neben der treiberdefinierten Standardwert unterstützen (durch Aufrufen von verfügbar **SQLGetInfo** mit der Option SQL_DEFAULT_TXN_ISOLATION). Für Ebene-2-Schnittstelle Konformität muss der Treiber sql_txn_serializable festgelegt sind ebenfalls unterstützen.  
  
 In der folgenden Tabelle gibt an, dem Konformitätsgrad des jede ODBC-Anweisungsattribut, in denen dies gut definiert ist.  
  
|Funktion|Konformitätsgrad|  
|--------------|-----------------------|  
|SQL_ATTR_APP_PARAM_DESC|Core|  
|SQL_ATTR_APP_ROW_DESC|Core|  
|SQL_ATTR_ASYNC_ENABLE|Ebene 1/Level 2 [1]|  
|SQL_ATTR_CONCURRENCY|Ebene 1/Level 2 [2]|  
|SQL_ATTR_CURSOR_SCROLLABLE|Ebene 1|  
|SQL_ATTR_CURSOR_SENSITIVITY|Ebene 2|  
|SQL_ATTR_CURSOR_TYPE|Core-Ebene 2 [3]|  
|SQL_ATTR_ENABLE_AUTO_IPD|Ebene 2|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|Ebene 2|  
|SQL_ATTR_IMP_PARAM_DESC|Core|  
|SQL_ATTR_IMP_ROW_DESC|Core|  
|SQL_ATTR_KEYSET_SIZE|Ebene 2|  
|SQL_ATTR_MAX_LENGTH|Ebene 1|  
|SQL_ATTR_MAX_ROWS|Ebene 1|  
|SQL_ATTR_METADATA_ID|Core|  
|SQL_ATTR_NOSCAN|Core|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|Core|  
|SQL_ATTR_PARAM_BIND_TYPE|Core|  
|SQL_ATTR_PARAM_OPERATION_PTR|Core|  
|SQL_ATTR_PARAM_STATUS_PTR|Core|  
|SQL_ATTR_PARAMS_PROCESSED_PTR|Core|  
|SQL_ATTR_PARAMSET_SIZE|Core|  
|SQL_ATTR_QUERY_TIMEOUT|Ebene 2|  
|SQL_ATTR_RETRIEVE_DATA|Ebene 1|  
|SQL_ATTR_ROW_ARRAY_SIZE|Core|  
|SQL_ATTR_ROW_BIND_OFFSET_PTR|Core|  
|SQL_ATTR_ROW_BIND_TYPE|Core|  
|SQL_ATTR_ROW_NUMBER|Ebene 1|  
|SQL_ATTR_ROW_OPERATION_PTR|Ebene 1|  
|SQL_ATTR_ROW_STATUS_PTR|Core|  
|SQL_ATTR_ROWS_FETCHED_PTR FEST|Core|  
|SQL_ATTR_SIMULATE_CURSOR|Ebene 2|  
|SQL_ATTR_USE_BOOKMARKS|Ebene 2|  
  
 [1]-Anwendungen, die Verbindungsebene Asynchronie (erforderlich für Ebene 1) unterstützen müssen unterstützen Festlegen dieses Attributs auf SQL_TRUE durch Aufrufen von **SQLSetConnectAttr**; das Attribut nicht auf einen anderen Wert als den Standardwert festgelegt sein muss Wert über **SQLSetStmtAttr**. Anwendungen, die auf Anweisungsebene Asynchronie (erforderlich für Ebene 2) unterstützen müssen durch Festlegen dieses Attributs auf SQL_TRUE, die mit einer Funktion unterstützen.  
  
 [2] für Ebene-2-Schnittstelle Konformität muss der Treiber SQL_CONCUR_READ_ONLY und mindestens ein anderer Wert unterstützen.  
  
 [3] für Ebene 1 Schnittstelle Konformität muss der Treiber SQL_CURSOR_FORWARD_ONLY und mindestens ein anderer Wert unterstützen. Für Ebene-2-Schnittstelle Konformität muss der Treiber alle Werte, die in diesem Dokument definierte unterstützen.

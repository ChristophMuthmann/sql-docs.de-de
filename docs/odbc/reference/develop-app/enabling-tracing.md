---
title: Aktivieren der Ablaufverfolgung | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: tracing options [ODBC], enabling
ms.assetid: 48e318bd-2487-4708-a698-ea01f36a45e9
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 569c5b42c57bca4eff30225f5dcc1ff1176fe00e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="enabling-tracing"></a>Aktivieren der Ablaufverfolgung
Ablaufverfolgung kann in der folgenden drei Arten aktiviert werden:  
  
-   Legen Sie die **Ablaufverfolgung** und **TraceFile** Schlüsselwörter im Registrierungseintrag Odbc.ini. Dies aktiviert oder deaktiviert die Ablaufverfolgung, wenn **SQLAllocHandle** mit einem *HandleType* SQL_HANDLE_ENV aufgerufen wird. Diese Optionen werden in der Registerkarte "Ablaufverfolgung" im Dialogfeld ODBC-Datenquellen-Administrator angezeigt wird, während Data Source-Setup festgelegt. Weitere Informationen finden Sie unter [Registrierungseinträge für Datenquellen](../../../odbc/reference/install/registry-entries-for-data-sources.md).  
  
-   Rufen Sie **SQLSetConnectAttr** SQL_ATTR_TRACE-Verbindungsattribut auf SQL_OPT_TRACE_ON festgelegt. Dies aktiviert oder deaktiviert die Ablaufverfolgung für die Dauer der Verbindung. Weitere Informationen finden Sie unter der [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) funktionsbeschreibung.  
  
-   Verwendung **ODBCSharedTraceFlag** zu aktivieren oder deaktivieren Sie die Protokollierung dynamisch. (Weitere Informationen finden Sie im nächste Thema [dynamische Tracing](../../../odbc/reference/develop-app/dynamic-tracing.md).)

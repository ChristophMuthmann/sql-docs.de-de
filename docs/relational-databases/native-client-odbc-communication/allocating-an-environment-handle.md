---
title: Zuordnen eines Umgebungshandles | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-communication
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, environment handles
- ODBC applications, connections
- handles [SQL Server Native Client]
- environment handles [SQLNCLI]
ms.assetid: 15c1b428-ea6d-4672-894c-f0e289e2da3f
caps.latest.revision: "29"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1f7f5442bc8cb3a6e5443d25e196b0e4567bba3c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="allocating-an-environment-handle"></a>Zuordnen eines Umgebungshandles
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Bevor eine Anwendung eine ODBC-Funktion aufrufen kann, muss sie die ODBC-Umgebung initialisieren und ein Umgebungshandle zuordnen. Dies ist das globale Kontexthandle und der Platzhalter für die anderen Handles in ODBC. Dazu rufen **SQLAllocHandle** mit der *HandleType* Parametersatz auf SQL_HANDLE_ENV und *InputHandle* auf SQL_NULL_HANDLE festgelegt wird.  
  
 Nachdem das Umgebungshandle zugewiesen wurde, muss die Anwendung Umgebungsattribute festlegen, um anzugeben, welche Version der ODBC-Funktionsaufrufe verwendet wird. Die ODBC 3. verwenden zu können. *x* -Funktionen aufrufen [SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md) mit der *Attribut* Parametersatz auf SQL_ATTR_ODBC_VERSION und *ValuePtr* SQL_OV_ festgelegt ODBC3.  
  
## <a name="see-also"></a>Siehe auch  
 [Bei der Kommunikation mit SQLServer &#40; ODBC &#41;](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  

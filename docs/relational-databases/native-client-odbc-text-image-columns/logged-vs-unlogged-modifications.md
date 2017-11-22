---
title: "Protokollierte im Vergleich zu Nicht protokollierte Änderungen | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-text-image-columns
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], image
- data types [ODBC], text
- logged vs. nonlogged modifications [SQL Server Native Client]
- columns [ODBC]
- ODBC data types, image columns
- nonlogged vs. logged modifications
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: 20aa5b27-4a2c-46e7-8356-beb0eebf4b7e
caps.latest.revision: "29"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2a429671be26d53fe9354e4ab986cb10ac35d35b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="logged-vs-unlogged-modifications"></a>Protokollierte im Vergleich zu Nicht protokollierte Änderungen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Kann eine Anwendung anfordern, die die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber nicht protokolliert **Text**, **Ntext**, und **Image** Änderungen. Diese Option sollte jedoch mit Vorsicht eingesetzt werden. Sollte nur für solche Situationen verwendet werden, in denen die **Text**, **Ntext**, oder **Image** Daten ist nicht wichtig und Datenbesitzer möchte die Möglichkeit zum Wiederherstellen von Daten für Kompromisse sind höhere Leistung.  
  
 Die Protokollierung von **Text**, **Ntext**, und **Image** Änderungen wird gesteuert durch Aufrufen von [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) mit der  *Attribut* Parametersatz auf SQL_SOPT_SS_ TEXTPTR_LOGGING und *ValuePtr* legen Sie entweder auf SQL_TL_ON oder auf sql_tl_off festgelegt wird.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten von Text und Imagespalten](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
  

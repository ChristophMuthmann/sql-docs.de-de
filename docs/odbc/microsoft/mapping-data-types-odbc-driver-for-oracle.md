---
title: "Zuordnen von Datentypen (ODBC-Treiber für Oracle) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mapping data types [ODBC]
- data types [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], data types
ms.assetid: a5d9ce12-19da-4943-8493-e3d56fa08348
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b6384f81f03a20e46a1d2a6434063caf32577554
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="mapping-data-types-odbc-driver-for-oracle"></a>Zuordnen von Datentypen (ODBC-Treiber für Oracle)
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Verwenden Sie stattdessen den ODBC-Treiber von Oracle bereitgestellt.  
  
 Der Oracle-Server unterstützt einen Satz von Datentypen. Der ODBC-Treiber für Oracle wird diese Datentypen in ihre entsprechenden ODBC SQL-Datentypen zugeordnet. Die folgende Tabelle enthält die Oracle 7.3 Server-Datentypen und die entsprechenden ODBC SQL-Datentypen.  
  
 Der ODBC-Treiber für Oracle unterstützt Oracle 7.3 und einige 8-Datentypen. Weitere Informationen zu unterstützten 8-Datentypen finden Sie unter [Supported Data Types](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md).  
  
|Oracle Server-Datentyp|ODBC-SQL-Datentyp|  
|-----------------------------|------------------------|  
|CHAR|SQL_CHAR|  
|DATE|SQL_TIMESTAMP|  
|GLEITKOMMAZAHL|SQL_DOUBLE|  
|INTEGER|SQL_DECIMAL|  
|LONG|SQL_LONGVARCHAR|  
|LONG RAW|SQL_LONGVARBINARY|  
|NUMBER|SQL_DECIMAL|  
|RAW|SQL_VARBINARY|  
|VARCHAR2|SQL_VARCHAR|  
  
> [!NOTE]  
>  Weitere Informationen zu die zulässige Größe der Spalte VARCHAR, finden Sie unter [VARCHAR Spaltengröße](../../odbc/microsoft/varchar-column-size-odbc-driver-for-oracle.md) in diesem Handbuch.


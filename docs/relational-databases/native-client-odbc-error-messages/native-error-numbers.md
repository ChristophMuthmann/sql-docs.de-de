---
title: Systemeigene Fehlernummern | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-error-messages
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- ODBC error handling, native error numbers
- SQL Server Native Client ODBC driver, errors
- native error numbers [SQL Server Native Client]
- messages [ODBC], native error numbers
- errors [ODBC], native error numbers
ms.assetid: 77cbc826-f47f-4803-8e7a-223d6df069b1
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 49fbc1ffedf678170bf08306220a7389cf1ed3f4
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="native-error-numbers"></a>Systemeigene Fehlernummern
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Für Fehler, die in der Datenquelle auftreten (zurückgegebenes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]), wird die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber gibt die systemeigene Fehlernummer an, indem sie zurückgegeben [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Für Fehler, die vom Treiber erkannt die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber gibt eine systemeigene Fehlernummer 0 zurück. Weitere Informationen zu einer Liste mit systemeigenen Fehlernummern finden Sie unter der Fehlerspalte der **Sysmessages** -Systemtabelle in der **master** in Datenbank [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Informationen über die Statusfehlercodes finden Sie unter [SQLSTATE &#40; ODBC-Fehlercodes &#41;](../../relational-databases/native-client-odbc-error-messages/sqlstate-odbc-error-codes.md). Bei Fehlern, die von der Netzwerkbibliothek zurückgegeben werden, stammt die systemeigene Fehlernummer von der zugrunde liegenden Netzwerksoftware.  
  
## <a name="see-also"></a>Siehe auch  
 [Behandlung von Fehlern und Meldungen](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  

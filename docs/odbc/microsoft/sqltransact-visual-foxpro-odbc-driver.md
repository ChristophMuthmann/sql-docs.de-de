---
title: SQLTransact (Visual FoxPro-ODBC-Treiber) | Microsoft Docs
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
helpviewer_keywords: SQLTransact function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 92cf86c0-f7a8-44d7-b59f-a1342677440b
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ff927598bd1c5458d296a4b19786c4c78b98785f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqltransact-visual-foxpro-odbc-driver"></a>SQLTransact (Visual FoxPro-ODBC-Treiber)
> [!NOTE]  
>  Dieses Thema enthält Visual FoxPro-ODBC-Treiber-spezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Unterstützung: vollständige  
  
 : ODBC-API Core Konformitätsgrad  
  
 Fordert einen Commit oder Rollback-Vorgang für alle aktiven Vorgänge auf alle Anweisungshandles (*Befehls beschäftigt*s) eine Verbindung oder für alle Verbindungen, die das Umgebungshandle zugeordnet zugeordneten *Henv*. **SQLTransact** funktioniert nur bei Datenquellen, [Datenbanken](../../odbc/microsoft/visual-foxpro-terminology.md).  
  
 Die Transaktion bleibt aktiv, wenn ein Commit im manuellen Modus fehlschlägt, Sie können auswählen, um ein Rollback der Transaktion, oder wiederholen den Commitvorgang. Wenn ein Commitvorgang im Transaktionsmodus für automatische fehlschlägt, wird die Transaktion automatisch zurückgesetzt; die Transaktion darf nicht inaktiv sein.  
  
 Weitere Informationen finden Sie unter [SQLTransact](../../odbc/reference/syntax/sqltransact-function.md) in der *ODBC Programmer's Reference*.

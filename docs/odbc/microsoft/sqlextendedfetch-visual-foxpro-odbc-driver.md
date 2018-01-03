---
title: SQLExtendedFetch (Visual FoxPro-ODBC-Treiber) | Microsoft Docs
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
helpviewer_keywords: SQLExtendedFetch function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b28af112-fb47-4143-b11e-3b743b2ae1b8
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f4788047cb62f8bb6c8e0f3f09ae865c3e8fca21
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqlextendedfetch-visual-foxpro-odbc-driver"></a>SQLExtendedFetch (Visual FoxPro-ODBC-Treiber)
> [!NOTE]  
>  Dieses Thema enthält Visual FoxPro-ODBC-Treiber-spezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Unterstützung: vollständige  
  
 ODBC-API-Konformität: Ebene 2  
  
 Ähnlich wie [SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md) jedoch mehrere Zeilen mit einem Array für jede Spalte zurückgegeben. Das Resultset ist Forward bildlauffähige und rückwärts bildlauffähige, wenn der Cursor definiert ist, werden statische, nicht Vorwärtscursor vorgenommen werden kann.  
  
 Standardmäßig gibt der Visual FoxPro-ODBC-Treiber nicht in einer Tabelle FoxPro als gelöscht markierte Zeilen zurück. Zeilen zum Löschen markiert, aber noch nicht aus einer Tabelle entfernt wurden, sind nicht in der resultsetcursor enthalten. Sie können dieses Verhalten ändern, indem Sie mit der [SET DELETED](../../odbc/microsoft/set-deleted-command.md) Befehl.  
  
 Weitere Informationen finden Sie unter [SQLExtendedFetch](../../odbc/reference/syntax/sqlextendedfetch-function.md) in der *ODBC Programmer's Reference*.

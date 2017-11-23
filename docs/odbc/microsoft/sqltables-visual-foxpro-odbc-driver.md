---
title: SQLTables (Visual FoxPro-ODBC-Treiber) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLTables function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 69e2a038-5def-423f-91aa-8756e069dd2a
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0414d6d4bc61cc114d4bce83220e2f20c25def40
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="sqltables-visual-foxpro-odbc-driver"></a>SQLTables (Visual FoxPro-ODBC-Treiber)
> [!NOTE]  
>  Dieses Thema enthält Visual FoxPro-ODBC-Treiber-spezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Unterstützung: vollständige  
  
 ODBC-API-Konformität: Ebene 1  
  
 Gibt die Liste der Tabellennamen angegeben durch den Parameter in der **SQLTables** Anweisung. Wenn kein Parameter angegeben wird, gibt die Namen der Tabellen in der aktuellen Datenquelle gespeichert. Der Treiber gibt zurück, die Informationen als ein Resultset.  
  
 Enumeration Typs ruft werden einen Ergebnis Set-Eintrag für remote-Ansichten oder lokalen parametrisierte Sichten nicht empfangen. Allerdings einen Aufruf von **SQLTables** durch eine eindeutige Tabelle wird eine Übereinstimmung mit einer solchen Ansicht von namenspezifizierer ermittelt, ob mit diesem Namen vorhanden; Dadurch wird die API verwendet werden, um Namenskonflikte vor der Erstellung einer neuen Tabelle überprüfen.  
  
> [!NOTE]  
>  Der Visual FoxPro-ODBC-Treiber unterscheidet zwischen [-Datenbanktabellen](../../odbc/microsoft/visual-foxpro-terminology.md) und [frei Tabellen](../../odbc/microsoft/visual-foxpro-terminology.md), selbst wenn beide Typen von Tabellen im selben Verzeichnis auf Ihrem System gespeichert werden. Wenn Ihre Datenquelle freie Tabellen in einem Verzeichnis befindet, wird der Visual FoxPro-ODBC-Treiber nicht Katalog oder Zurückgeben der Namen von Tabellen, die einer Datenbank zugeordnet sind.  
  
 Weitere Informationen finden Sie unter [SQLTables](../../odbc/reference/syntax/sqltables-function.md) in der *ODBC Programmer's Reference*.

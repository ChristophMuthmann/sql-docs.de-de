---
title: SQLDriverConnect (Visual FoxPro-ODBC-Treiber) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLDriverConnect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 10492c8f-3a18-4971-9db8-879e878083b9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f463f7c1c71ef120c7fb5446e3edd1f77c791137
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqldriverconnect-visual-foxpro-odbc-driver"></a>SQLDriverConnect (Visual FoxPro-ODBC-Treiber)
> [!NOTE]  
>  Dieses Thema enthält Visual FoxPro-ODBC-Treiber-spezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Unterstützung: vollständige  
  
 ODBC-API-Konformität: Ebene 1  
  
 Eine Verbindung mit einer vorhandenen Datenquelle, die kann entweder ein [Datenbank](../../odbc/microsoft/visual-foxpro-terminology.md) oder in einem Verzeichnis [frei Tabellen](../../odbc/microsoft/visual-foxpro-terminology.md). Die ODBC-Attribut Schlüsselwörter UID und PWD werden ignoriert. In der folgenden Tabelle sind die zusätzlichen unterstützten Attributspeicher Schlüsselwörter aufgeführt.  
  
|ODBC-Attribut-Schlüsselwort|Attributwert|  
|----------------------------|---------------------|  
|DSN||  
|UID|Von der Visual FoxPro-ODBC-Treiber ignoriert, nicht jedoch einen Fehler.|  
|PWD|Von der Visual FoxPro-ODBC-Treiber ignoriert, nicht jedoch einen Fehler.|  
|Treiber|Name und Speicherort der Visual FoxPro-ODBC-Treiber; implementiert die vom Treiber-Manager.|  
  
|Visual FoxPro-ODBC-Treiber-Attribut-Schlüsselwort|Attributwert|  
|-------------------------------------------------|---------------------|  
|BackgroundFetch|"Yes" oder "No"|  
|Sortieren|"Computer" oder andere Sortierreihenfolge. Eine Liste der unterstützten Sortierreihenfolge Sequenzen, finden Sie unter [festgelegt COLLATE](../../odbc/microsoft/set-collate-command.md).|  
|Description||  
|Exclusive|"Yes" oder "No"|  
|SourceDB|Einen vollständig qualifizierten Pfad auf ein Verzeichnis mit NULL oder mehr [frei Tabellen](../../odbc/microsoft/visual-foxpro-terminology.md), oder der absolute Pfad und Dateiname für eine [Datenbank](../../odbc/microsoft/visual-foxpro-terminology.md).|  
|SourceType|"Datenbank" oder "DBF"|  
|Version||  
  
 Wenn der Name der Datenquelle nicht angegeben ist, wird der Treiber-Manager fordert den Benutzer Informationen zu erhalten (entsprechend der Einstellung von der *fDriverCompletion* Argument) und dann fortgesetzt wird. Wenn Sie weitere Informationen erforderlich ist, zeigt der Visual FoxPro-ODBC-Treiber das Dialogfeld "Prompt".  
  
 Weitere Informationen finden Sie unter [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md) in der *ODBC Programmer's Reference*.

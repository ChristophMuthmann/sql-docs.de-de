---
title: SQLDriverConnect (Excel-Treiber) | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], Excel Driver
ms.assetid: 285cb1ea-f461-4596-97f2-fc57af05dede
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 05274f9efa557d7d0b47b6dce0e06160c3ab5c29
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqldriverconnect-excel-driver"></a>SQLDriverConnect (Excel-Treiber)
> [!NOTE]  
>  Dieses Thema enthält die Excel-Treiber-spezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLDriverConnect** können Sie einem Treiberpaket zu verbinden, ohne das Erstellen einer Datenquelle (DSN).  
  
 Die folgenden Schlüsselwörter werden in der Verbindungszeichenfolge für alle Treiber unterstützt: **DSN**, **DBQ**, und **FIL**.  
  
 In der folgenden Tabelle sind die minimalen Schlüsselwörter, die für die Verbindung mit jeder Treiber und enthält ein Beispiel für die Schlüsselwort-Wert-Paaren, die mit verwendet **SQLDriverConnect**. Eine vollständige Liste der DRIVERID Werte finden Sie unter [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).  
  
> [!NOTE]  
>  Wenn DBQ oder Wert für die Microsoft Excel 3.0 oder 4.0 Treiber nicht angegeben ist, werden die Treiber in das aktuelle Verzeichnis verbunden.  
  
|Treiber|Schlüsselwörter, die erforderlich sind|Beispiele|  
|------------|-----------------------|--------------|  
|Microsoft Excel 3.0 oder 4.0|DriverID-Treiber|Driver = {Microsoft Excel-Treiber (*.xls)}; DBQ = "c:\Temp"; DriverID = 278|  
|Microsoft Excel 5.0/7.0|Treiber, DriverID, DBQ|Driver = {Microsoft Excel-Treiber (*.xls)}; DBQ=c:\temp\sample.xls; DriverID = 22|  
|Microsoft Excel 97 und höher|Treiber, DriverID, DBQ|Driver = {Microsoft Excel-Treiber (*.xls)}; DBQ=c:\temp\sample.xls; DriverID = 790|

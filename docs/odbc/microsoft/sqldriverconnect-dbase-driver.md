---
title: SQLDriverConnect (dBASE-Treiber) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- DBase driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], dBASE Driver
ms.assetid: c837aa31-068e-4fa3-bc00-aae09bec21de
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 35f26a0e81c27bf773145410b9f0ab8bbbb2c5a3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqldriverconnect-dbase-driver"></a>SQLDriverConnect (dBASE-Treiber)
> [!NOTE]  
>  Dieses Thema enthält dBASE treiberspezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLDriverConnect** können Sie einem Treiberpaket zu verbinden, ohne das Erstellen einer Datenquelle (DSN).  
  
 Die folgenden Schlüsselwörter werden in der Verbindungszeichenfolge für alle Treiber unterstützt: **DSN**, **DBQ**, und **FIL**.  
  
 Wenn Paradox-Treiber, verwendet wird nachdem eine kennwortgeschützte Datei von einem Benutzer geöffnet wurde, sind andere Benutzer nicht zulässig, um die gleiche Datei zu öffnen.  
  
 In der folgenden Tabelle sind die minimalen Schlüsselwörter, die für die Verbindung mit jeder Treiber und enthält ein Beispiel für die Schlüsselwort-Wert-Paaren, die mit verwendet **SQLDriverConnect**. Eine vollständige Liste der DRIVERID Werte finden Sie unter [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).  
  
> [!NOTE]  
>  Wenn DBQ oder Wert für die dBASEdriver nicht angegeben ist, werden die Treiber in das aktuelle Verzeichnis verbunden.  
  
|Treiber|Schlüsselwörter, die erforderlich sind|Beispiele|  
|------------|-----------------------|--------------|  
|DBASE|DriverID-Treiber|Driver = {Microsoft dBASE-Treiber (*.DBF)}; DBQ = "c:\Temp"; DriverID = 277|

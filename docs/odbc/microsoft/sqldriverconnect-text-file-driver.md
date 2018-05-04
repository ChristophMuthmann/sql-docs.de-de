---
title: SQLDriverConnect (Text-Datei-Treiber) | Microsoft Docs
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
- SQLDriverConnect function [ODBC], Text File Driver
- text file driver [ODBC], SQLDriverConnect
ms.assetid: d7769021-bd18-4d8e-96e0-e184a82d6ca3
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 491f2a8d6e7ab372703cf51f309325807337335a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqldriverconnect-text-file-driver"></a>SQLDriverConnect (Text-Datei-Treiber)
> [!NOTE]  
>  Dieses Thema enthält die Textdatei treiberspezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLDriverConnect** können Sie einem Treiberpaket zu verbinden, ohne das Erstellen einer Datenquelle (DSN).  
  
 Die folgenden Schlüsselwörter werden in der Verbindungszeichenfolge für alle Treiber unterstützt: **DSN**, **DBQ**, und **FIL**.  
  
 In der folgenden Tabelle sind die minimalen Schlüsselwörter, die für die Verbindung mit jeder Treiber und enthält ein Beispiel für die Schlüsselwort-Wert-Paaren, die mit verwendet **SQLDriverConnect**. Eine vollständige Liste der DRIVERID Werte finden Sie unter [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).  
  
> [!NOTE]  
>  Wenn DBQ oder Wert für den Text-Treiber nicht angegeben ist, werden die Treiber in das aktuelle Verzeichnis verbunden.  
  
|Treiber|Schlüsselwörter, die erforderlich sind|Beispiele|  
|------------|-----------------------|--------------|  
|Text|Treiber|Driver = {Microsoft-Texttreiber (*.txt;\*. Volumes, CSV)}; Wert = "c:\Temp"|

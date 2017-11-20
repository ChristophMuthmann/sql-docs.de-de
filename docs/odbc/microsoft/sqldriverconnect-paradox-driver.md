---
title: SQLDriverConnect (Paradox-Treiber) | Microsoft Docs
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
- SQLDriverConnect function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLDriverConnect
ms.assetid: c2ba486e-5e01-4e67-adb1-68511f5f0206
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f9265657327f71e41c124707ab66c8ad621bda55
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqldriverconnect-paradox-driver"></a>SQLDriverConnect (Paradox-Treiber)
> [!NOTE]  
>  Dieses Thema enthält Paradox treiberspezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLDriverConnect** können Sie einem Treiberpaket zu verbinden, ohne das Erstellen einer Datenquelle (DSN).  
  
 Die folgenden Schlüsselwörter werden in der Verbindungszeichenfolge für alle Treiber unterstützt: **DSN**, **DBQ**, und **FIL**.  
  
 Die **PWD** -Schlüsselwort wird ebenfalls unterstützt. Das PWD-Schlüsselwort sollte die Sonderzeichen nicht enthalten (Siehe SQL_SPECIAL_CHARACTERS in **SQLGetInfo** Werte zurückgegeben).  
  
 Nachdem eine kennwortgeschützte Datei von einem Benutzer geöffnet wurde, sind andere Benutzer nicht zulässig, auf die gleiche Datei zu öffnen.  
  
 In der folgenden Tabelle sind die minimalen Schlüsselwörter, die für die Verbindung mit jeder Treiber und enthält ein Beispiel für die Schlüsselwort-Wert-Paaren, die mit verwendet **SQLDriverConnect**. Eine vollständige Liste der DRIVERID Werte finden Sie unter [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).  
  
> [!NOTE]  
>  Wenn DBQ oder Wert für den Treiber Paradox nicht angegeben ist, werden die Treiber in das aktuelle Verzeichnis verbunden.  
  
|Treiber|Schlüsselwörter, die erforderlich sind|Beispiel|  
|------------|-----------------------|-------------|  
|Paradox|DriverID-Treiber|Driver = {Microsoft Paradox-Treiber (*.DB)}; DBQ = "c:\Temp"; DriverID = 26|


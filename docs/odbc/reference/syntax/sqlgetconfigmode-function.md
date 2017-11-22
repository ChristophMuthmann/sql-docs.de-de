---
title: SQLGetConfigMode Funktion | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLGetConfigMode
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLGetConfigMode
helpviewer_keywords: SQLGetConfigMode function [ODBC]
ms.assetid: b96ab3b8-08d5-4fea-9ffe-e03043efbf2d
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 82f01e7b93cc5114193dcc550476dafc63cd09a3
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="sqlgetconfigmode-function"></a>SQLGetConfigMode-Funktion
**Konformität**  
 Version eingeführt: ODBC 3.0  
  
 **Zusammenfassung**  
 **SQLGetConfigMode** Ruft den Konfigurationsmodus, der angibt, in dem der Odbc.ini Eintrag auflisten DSN-Werte in die Systeminformationen ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BOOL SQLGetConfigMode(  
     UWORD *   pwConfigMode);  
```  
  
## <a name="arguments"></a>Argumente  
 *pwConfigMode*  
 [Ausgabe] Zeiger auf den Puffer, der Konfigurationsmodus enthält. (Siehe "Kommentare".) Der Wert in  *\*PwConfigMode* sind möglich:  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>Rückgabewert  
 Die Funktion gibt "true" zurück, wenn erfolgreich, "false" ist dabei ein Fehler aufgetreten.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLGetConfigMode** gibt "false", ein zugehöriges  *\*PfErrorCode* Wert abgerufen werden kann, durch den Aufruf **SQLInstallerError**. Die folgende Tabelle enthält die  *\*PfErrorCode* Werte, die von zurückgegeben werden können **SQLInstallerError** und jeweils im Kontext dieser Funktion erläutert.  
  
|*\*pfErrorCode*|Fehler|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_OUT_OF_MEM|Nicht genügend Arbeitsspeicher.|Das Installationsprogramm konnte die Funktion aufgrund unzureichenden Arbeitsspeichers nicht ausgeführt werden.|  
  
## <a name="comments"></a>Kommentare  
 Diese Funktion wird verwendet, um zu bestimmen, in dem der Odbc.ini Eintrag auflisten DSN-Werte in die Systeminformationen ist. Wenn  *\*PwConfigMode* ODBC_USER_DSN, der DSN ist eine Benutzer-DSN und die Funktion liest aus dem Eintrag der Odbc.ini in HKEY_CURRENT_USER. Ist er ODBC_SYSTEM_DSN, der DSN ist eine System-DSN, und die Funktion liest aus dem Eintrag der Odbc.ini in HKEY_LOCAL_MACHINE. HKEY_CURRENT_USER wird versucht, wenn es sich um ODBC_BOTH_DSN handelt, und falls dies fehlschlägt, wird HKEY_LOCAL_MACHINE verwendet.  
  
 Standardmäßig **SQLGetConfigMode** ODBC_BOTH_DSN zurückgibt. Wenn ein Benutzer-DSN oder einer System-DSN durch einen Aufruf von erstellt **SQLConfigDataSource**, setzt die Funktion der Konfigurationsmodus ODBC_USER_DSN oder ODBC_SYSTEM_DSN, um Benutzer und System-DSNs, die beim Ändern von einem DSN zu unterscheiden. Vor der Rückgabe, **SQLConfigDataSource** setzt die Konfigurationsmodus auf ODBC_BOTH_DSN zurück.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Durch Festlegen des Konfigurationsmodus|[SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|

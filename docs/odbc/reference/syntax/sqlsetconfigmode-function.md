---
title: SQLSetConfigMode Funktion | Microsoft Docs
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
apiname: SQLSetConfigMode
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLSetConfigMode
helpviewer_keywords: SQLSetConfigMode function [ODBC]
ms.assetid: 09eb88ea-b6f6-4eca-b19d-0951cebc6c0a
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 96ffac2d3329aa9e9b69be122dfd7becc37acd57
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="sqlsetconfigmode-function"></a>SQLSetConfigMode-Funktion
**Konformität**  
 Version eingeführt: ODBC 3.0  
  
 **Zusammenfassung**  
 **SQLSetConfigMode** legt den Konfigurationsmodus, der angibt, in dem der Odbc.ini Eintrag auflisten DSN-Werte in die Systeminformationen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BOOL SQLSetConfigMode(  
     UWORD     wConfigMode);  
```  
  
## <a name="arguments"></a>Argumente  
 *wConfigMode*  
 [Eingabe] Der Installer-Konfigurationsmodus (siehe "Kommentare"). Der Wert in *wConfigMode* sind möglich:  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>Rückgabewert  
 Die Funktion gibt "true" zurück, wenn erfolgreich, "false" ist dabei ein Fehler aufgetreten.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLSetConfigMode** gibt "false", ein zugehöriges  *\*PfErrorCode* Wert abgerufen werden kann, durch den Aufruf **SQLInstallerError**. Die folgende Tabelle enthält die  *\*PfErrorCode* Werte, die von zurückgegeben werden können **SQLInstallerError** und jeweils im Kontext dieser Funktion erläutert.  
  
|*\*pfErrorCode*|Fehler|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|Ungültiger Parameter-Sequenz|Die *wConfigMode* Argument keine ODBC_USER_DSN, ODBC_SYSTEM_DSN oder ODBC_BOTH_DSN enthalten.|  
  
## <a name="comments"></a>Kommentare  
 Diese Funktion wird verwendet, um festgelegt, wobei der Odbc.ini Eintrag auflisten DSN-Werte in die Systeminformationen. Wenn *wConfigMode* ODBC_USER_DSN, der DSN ist eine Benutzer-DSN und die Funktion liest aus dem Eintrag der Odbc.ini in HKEY_CURRENT_USER. Ist er ODBC_SYSTEM_DSN, der DSN ist eine System-DSN, und die Funktion liest aus dem Eintrag der Odbc.ini in HKEY_LOCAL_MACHINE. Ist er ODBC_BOTH_DSN, wird das von HKEY_CURRENT_USER versucht, und falls dies fehlschlägt, klicken Sie dann HKEY_LOCAL_MACHINE dient.  
  
 Diese Funktion hat keinen Einfluss auf **SQLCreateDataSource** und **SQLDriverConnect**. Der Konfigurationsmodus muss festgelegt werden, wenn ein Treiber durch den Aufruf aus der Registrierung liest **SQLGetPrivateProfileString** oder schreibt Sie in der Registrierung durch den Aufruf **SQLWritePrivateProfileString**. Aufrufe von **SQLGetPrivateProfileString** und **SQLWritePrivateProfileString** verwenden, der Konfigurationsmodus wissen, welcher Teil der Registrierung, das verarbeitet werden.  
  
> [!CAUTION]  
>  **SQLSetConfigMode** sollte aufgerufen werden, nur bei Bedarf; Wenn der Modus nicht ordnungsgemäß festgelegt ist, die ODBC-Installationsprogramm fehlschlagen, ordnungsgemäß funktioniert.  
  
 **SQLSetConfigMode** macht eine direkte registrierungsänderung des Konfigurationsmodus. Dies ist, abgesehen von den Prozess der Änderung der Konfigurationsmodus durch einen Aufruf von **SQLConfigDataSource**. Ein Aufruf von **SQLConfigDataSource** legt den Konfigurationsmodus, Benutzer und System-DSNs, bei einen DSN ändern zu unterscheiden. Vor der Rückgabe, **SQLConfigDataSource** setzt die Konfigurationsmodus auf BOTHDSN zurück.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Erstellen einer Datenquelle|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|  
|Herstellen einer Verbindung mit einer Datenquelle mit einer Zeichenfolge oder ein Dialogfeld Verbindungsdialogfeld|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Abrufen von Konfigurationsmodus|[SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|

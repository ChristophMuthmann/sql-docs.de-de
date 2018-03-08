---
title: SQLRemoveDSNFromIni Funktion | Microsoft Docs
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
apiname: SQLRemoveDSNFromIni
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLRemoveDSNFromIni
helpviewer_keywords: SQLRemoveDSNFromIni function [ODBC]
ms.assetid: bb2e8273-7b61-4113-bfc8-f7ccc607c811
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6d53af3854ff74a075033a787820ee868e76e667
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqlremovedsnfromini-function"></a>SQLRemoveDSNFromIni-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0  
  
 **Zusammenfassung**  
 **SQLRemoveDSNFromIni** entfernt eine Datenquelle aus der Systeminformationen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BOOL SQLRemoveDSNFromIni(  
     LPCSTR   lpszDSN);  
```  
  
## <a name="arguments"></a>Argumente  
 *lpszDSN*  
 [Eingabe] Der Name der Datenquelle zu entfernen.  
  
## <a name="returns"></a>Rückgabewert  
 Die Funktion gibt "true" zurück, wenn die Datenquelle entfernt oder die Datenquelle nicht in die Datei Odbc.ini wurde. Es gibt FALSE zurück, wenn sie nicht innerhalb der Datenquelle zu entfernen.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLRemoveDSNFromIni** gibt "false", ein zugehöriges  *\*PfErrorCode* Wert abgerufen werden kann, durch den Aufruf **SQLInstallerError**. Die folgende Tabelle enthält die  *\*PfErrorCode* Werte, die von zurückgegeben werden können **SQLInstallerError** und jeweils im Kontext dieser Funktion erläutert.  
  
|*\*pfErrorCode*|Fehler|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Allgemeine Installer-Fehler|Fehler für die kein bestimmtes Installationsfehler aufgetreten.|  
|ODBC_ERROR_INVALID_DSN|Ungültige DSN|Die *LpszDSN* Argument war ungültig.|  
|ODBC_ERROR_REQUEST_FAILED|Fehler bei der Anforderung|Das Installationsprogramm konnte die DSN-Informationen nicht aus der Registrierung entfernt werden.|  
|ODBC_ERROR_OUT_OF_MEM|Nicht genügend Arbeitsspeicher.|Das Installationsprogramm konnte die Funktion aufgrund unzureichenden Arbeitsspeichers nicht ausgeführt werden.|  
  
## <a name="comments"></a>Kommentare  
 **SQLRemoveDSNFromIni** der Name der Datenquelle aus dem Abschnitt [ODBC-Datenquellen] Informationen entfernt. Zusätzlich wird Abschnitt Spezifikation-Datenquelle aus der Systeminformationen entfernt.  
  
 Diese Funktion sollte nur von Setup Treiberbibliothek aufgerufen werden.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Hinzufügen, ändern oder Entfernen einer Datenquelle|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|Hinzufügen, ändern oder Entfernen einer Datenquelle|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Entfernen die Standarddatenquelle|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|Die Systeminformationen hinzugefügt einen Datenquellennamen|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|

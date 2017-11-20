---
title: SQLWriteDSNToIni Funktion | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLWriteDSNToIni
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLWriteDSNToIni
helpviewer_keywords:
- SQLWriteDSNToIni [ODBC]
ms.assetid: dc7018b2-18d4-4657-96d0-086479a47474
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 230accf6ae34f7b6bbced597e6e8bf2991bc8544
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlwritedsntoini-function"></a>SQLWriteDSNToIni-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0  
  
 **Zusammenfassung**  
 **SQLWriteDSNToIni** die Systeminformationen eine Datenquelle hinzugefügt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BOOL SQLWriteDSNToIni(  
     LPCSTR   lpszDSN,  
     LPCSTR   lpszDriver);  
```  
  
## <a name="arguments"></a>Argumente  
 *lpszDSN*  
 [Eingabe] Der Name der Datenquelle hinzufügen.  
  
 *lpszDriver*  
 [Eingabe] Beschreibung (normalerweise der Name des zugehörigen DBMS) anstelle des Namens des physischen Treiber präsentiert.  
  
## <a name="returns"></a>Rückgabewert  
 Die Funktion gibt "true" zurück, wenn erfolgreich, "false" ist dabei ein Fehler aufgetreten.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLWriteDSNToIni** gibt "false", ein zugehöriges  *\*PfErrorCode* Wert abgerufen werden kann, durch den Aufruf **SQLInstallerError**. Die folgende Tabelle enthält die  *\*PfErrorCode* Werte, die von zurückgegeben werden können **SQLInstallerError** und jeweils im Kontext dieser Funktion erläutert.  
  
|*\*pfErrorCode*|Fehler|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Allgemeine Installer-Fehler|Fehler für die kein bestimmtes Installationsfehler aufgetreten.|  
|ODBC_ERROR_INVALID_DSN|Ungültige DSN|Die *LpszDSN* Argument enthalten sind, eine Zeichenfolge, die für eine DSN ungültig war.|  
|ODBC_ERROR_INVALID_NAME|Ungültiger Name für Treiber oder das Konvertierungsprogramm|Die *LpszDriver* Argument war ungültig.|  
|ODBC_ERROR_REQUEST_FAILED|Fehler bei der Anforderung|Der Installer konnte nicht in der Registrierung einen DSN erstellen.|  
|ODBC_ERROR_OUT_OF_MEM|Nicht genügend Arbeitsspeicher.|Das Installationsprogramm konnte die Funktion aufgrund unzureichenden Arbeitsspeichers nicht ausgeführt werden.|  
  
## <a name="comments"></a>Kommentare  
 **SQLWriteDSNToIni** im Abschnitt [ODBC-Datenquellen], Informationen mit die Datenquelle hinzugefügt. Anschließend erstellt einen Abschnitt Spezifikation für die Datenquelle und fügt Sie ein einzelnes Schlüsselwort (**Treiber**) mit dem Namen der Treiber-DLL als Wert. Wenn Quelle Spezifikation Datenabschnitt bereits vorhanden ist, **SQLWriteDSNToIni** alten Abschnitts vor dem Erstellen des neuen Servers entfernt.  
  
 Der Aufrufer dieser Funktion muss alle treiberspezifischen Schlüsselwörter und Werte Quelle Spezifikation Datenabschnitt der Systeminformationen hinzufügen.  
  
 Wenn der Name der Datenquelle in der Standardeinstellung wird **SQLWriteDSNToIni** erstellt außerdem die Spezifikation den Standardabschnitt-Treiber in die Systeminformationen.  
  
 Diese Funktion sollte nur von einem Setup-DLL aufgerufen werden.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Hinzufügen, ändern oder Entfernen einer Datenquelle|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)(in der Setup-DLL)|  
|Hinzufügen, ändern oder Entfernen einer Datenquelle|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Entfernen einen Datenquellennamen aus der Systeminformationen|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|


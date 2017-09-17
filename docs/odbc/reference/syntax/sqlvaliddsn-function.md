---
title: SQLValidDSN Funktion | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLValidDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLValidDSN
helpviewer_keywords:
- SQLValidDSN [ODBC]
ms.assetid: 930d1d89-337a-4429-85a2-84ee10555ac9
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 473670a87ede935267c91537f301589b94666acf
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlvaliddsn-function"></a>SQLValidDSN-Funktion
**Konformität**  
 Version eingeführt: ODBC 2.0  
  
 **Zusammenfassung**  
 **SQLValidDSN** die Länge und die Gültigkeit der Namen der Datenquelle überprüft, bevor der Name der Systeminformationen hinzugefügt wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BOOL SQLValidDSN(  
     LPCSTR    lpszDSN);  
```  
  
## <a name="arguments"></a>Argumente  
 *lpszDSN*  
 [Eingabe] Datenquellenname überprüft werden soll.  
  
## <a name="returns"></a>Rückgabewert  
 Die Funktion gibt "true" zurück, wenn der Name der Datenquelle gültig ist. Wenn der Datenquellenname ungültig ist oder Fehler beim Aufrufen der Funktion zurückgegeben "false".  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLValidDSN** gibt "false", ein zugehöriges * \*PfErrorCode* Wert abgerufen werden kann, durch den Aufruf **SQLInstallerError**. Ein * \*PfErrorCode* wird zurückgegeben, nur wenn der Funktionsaufruf fehlgeschlagen ist, nicht wenn "false" zurückgegeben wurde, da der Datenquellenname ungültig ist. Die folgende Tabelle enthält die * \*PfErrorCode* Werte, die von zurückgegeben werden können **SQLInstallerError** und jeweils im Kontext dieser Funktion erläutert.  
  
|*\*pfErrorCode*|Fehler|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Allgemeine Installer-Fehler|Fehler für die kein bestimmtes Installationsfehler aufgetreten.|  
|ODBC_ERROR_OUT_OF_MEM|Nicht genügend Arbeitsspeicher.|Das Installationsprogramm konnte die Funktion aufgrund unzureichenden Arbeitsspeichers nicht ausgeführt werden.|  
  
## <a name="comments"></a>Kommentare  
 **SQLValidDSN** wird aufgerufen, indem Sie eines Treibers [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) So prüfen die Länge der Namen der Datenquelle und die Gültigkeit der einzelnen Zeichen im Namen Datenquelle. Er überprüft, ob die Länge des Namens SQL_MAX_DSN_LENGTH, größer ist, wie in Sqlext.h definiert. (Die Länge der Namen der Datenquelle wird auch durch überprüft [SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md).) **SQLValidDSN** überprüft, ob eine der folgenden ungültigen Zeichen im Namen Datenquelle enthalten sind:  
  
 [ ] { } ( ) , ; ? * = ! @ \  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Hinzufügen, ändern oder Entfernen einer Datenquelle|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) (in der Setup-DLL)|  
|Hinzufügen, ändern oder Entfernen einer Datenquelle|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Schreiben einen Datenquellennamen ein, in die Systeminformationen|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|

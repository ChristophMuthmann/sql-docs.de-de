---
title: ConfigTranslator Funktion | Microsoft Docs
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
- ConfigTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- ConfigTranslator
helpviewer_keywords:
- ConfigTranslator [ODBC]
ms.assetid: 7c22f07e-36de-425b-aa67-e32a84afae92
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f9de00042d81ac74bbda54be2060a331cf1ac3ad
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="configtranslator-function"></a>ConfigTranslator-Funktion
**Konformität**  
 Version eingeführt: ODBC 2.0  
  
 **Zusammenfassung**  
 **ConfigTranslator** eine Standardoption für die Übersetzung für ein Konvertierungsprogramm zurückgegeben. Sie können in das Konvertierungsprogramm DLL oder eine separate Installation DLL sein.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BOOL ConfigTranslator(  
     HWND     hwndParent,  
     DWORD *  pvOption);  
```  
  
## <a name="arguments"></a>Argumente  
 *hwndParent*  
 [Eingabe] Handle des übergeordneten Fensters. Die Funktion wird keine Dialogfelder angezeigt, wenn das Handle null ist.  
  
 *pvOption*  
 [Ausgabe] Eine für 32-Bit-Übersetzungsoption.  
  
## <a name="returns"></a>Rückgabewert  
 Die Funktion gibt "true" zurück, wenn erfolgreich, "false" ist dabei ein Fehler aufgetreten.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **ConfigTranslator** gibt "false", ein zugehöriges * \*PfErrorCode* Wert wird in den Puffer der Installer-Fehler durch einen Aufruf von gebucht **SQLPostInstallerError**und abgerufen werden können, durch den Aufruf **SQLInstallerError**. Die folgende Tabelle enthält die * \*PfErrorCode* Werte, die von zurückgegeben werden können **SQLInstallerError** und jeweils im Kontext dieser Funktion erläutert.  
  
|*\*pfErrorCode*|Fehler|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|Ungültige Fensterhandle|Die *HwndParent* Argument war ungültig oder NULL.|  
|ODBC_ERROR_DRIVER_SPECIFIC|Treiber-Konvertierer spezifische Fehler|Ein treiberspezifischen Fehler für die kein definierten ODBC-Installer-Fehler vorliegt. Die *SzError* Argument in einem Aufruf der **SQLPostInstallerError** Funktion sollte die treiberspezifische Fehlermeldung enthalten.|  
|ODBC_ERROR_INVALID_OPTION|Ungültige Translation-option|Die *PvOption* Argument enthalten einen ungültigen Wert.|  
  
## <a name="comments"></a>Kommentare  
 Wenn das Konvertierungsprogramm nur eine einzelne Translation-Option unterstützt **ConfigTranslator** gibt "true" zurück und setzt *PvOption* der 32-Bit-Option. Andernfalls wird die Standardoption für die Übersetzung verwendet bestimmt. **ConfigTranslator** kann ein Dialogfeld, mit denen ein Benutzer eine Standardoption für die Übersetzung wählt, anzeigen.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Abrufen einer Übersetzungsoption|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Ein Konvertierungsprogramm auswählen|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|Festlegen einer Übersetzungsoption|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|


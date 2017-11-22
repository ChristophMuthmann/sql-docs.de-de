---
title: SQLGetTranslator Funktion | Microsoft Docs
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
apiname: SQLGetTranslator
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLGetTranslator
helpviewer_keywords: SQLGetTranslator function [ODBC]
ms.assetid: 33879db3-5ef9-4585-9be5-69376157e017
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5d8b0f18e683facc1316fd5a58ac1a2983acea63
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="sqlgettranslator-function"></a>SQLGetTranslator-Funktion
**Konformität**  
 Version eingeführt: ODBC 2.0  
  
 **Zusammenfassung**  
 **SQLGetTranslator** zeigt ein Dialogfeld, in dem ein Benutzer ein Konvertierungsprogramm auswählen kann.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BOOL SQLGetTranslator(  
     HWND      hwndParent,  
     LPSTR     lpszName,  
     WORD      cbNameMax,  
     WORD *    pcbNameOut,  
     LPSTR     lpszPath,  
     WORD      cbPathMax,  
     WORD *    pcbPathOut,  
     DWORD *   pvOption);  
```  
  
## <a name="arguments"></a>Argumente  
 *hwndParent*  
 [Eingabe] Handle des übergeordneten Fensters.  
  
 *Wert*  
 [Eingabe/Ausgabe] Der Name des konvertierers aus der Systeminformationen.  
  
 *cbNameMax*  
 [Eingabe] Maximale Länge von der *Wert* Puffer.  
  
 *pcbNameOut*  
 [Eingabe/Ausgabe] Gesamtanzahl der Bytes (ausgenommen die Null-Terminierung Byte) übergeben oder in ausgegeben *Wert*. Die Anzahl der zurückzugebenden verfügbaren Bytes ist größer als oder gleich *CbNameMax*, den Konvertierer Namen im *Wert* auf abgeschnitten *CbNameMax* minus der NULL-Abschlusszeichen. Die *PcbNameOut* -Argument ein null-Zeiger sein.  
  
 *lpszPath*  
 [Ausgabe] Vollständiger Pfad der Konvertierungs-DLL.  
  
 *cbPathMax*  
 [Eingabe] Maximale Länge von der *LpszPath* Puffer.  
  
 *pcbPathOut*  
 [Ausgabe] Gesamte Anzahl der Bytes, die (mit Ausnahme der Null-Terminierung Byte) im zurückgegebenen *LpszPath*. Die Anzahl der zurückzugebenden verfügbaren Bytes ist größer als oder gleich *CbPathMax*, in der Übersetzung DLL-Pfad *LpszPath* auf abgeschnitten *CbPathMax* minus der NULL-Abschlusszeichen. Die *PcbPathOut* -Argument ein null-Zeiger sein.  
  
 *pvOption*  
 [Ausgabe] Übersetzung von 32-Bit-Option.  
  
## <a name="returns"></a>Rückgabewert  
 Die Funktion gibt "true" zurück, wenn er erfolgreich ausgeführt wird, "false" ist, wenn ein Fehler auftritt oder wenn der Benutzer das Dialogfeld abbricht.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLGetTranslator** gibt "false", ein zugehöriges  *\*PfErrorCode* Wert abgerufen werden kann, durch den Aufruf **SQLInstallerError**. Die folgende Tabelle enthält die  *\*PfErrorCode* Werte, die von zurückgegeben werden können **SQLInstallerError** und jeweils im Kontext dieser Funktion erläutert.  
  
|*\*pfErrorCode*|Fehler|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Allgemeine Installer-Fehler|Fehler für die kein bestimmtes Installationsfehler aufgetreten.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Ungültige Pufferlänge.|Die *CbNameMax* oder *CbPathMax* Argument war kleiner oder gleich 0.|  
|ODBC_ERROR_INVALID_HWND|Ungültige Fensterhandle|Die *HwndParent* Argument war ungültig oder NULL.|  
|ODBC_ERROR_INVALID_NAME|Ungültiger Name für Treiber oder das Konvertierungsprogramm|Die *Wert* Argument war ungültig. Es konnte nicht in der Registrierung gefunden werden.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Die Treiber oder das Konvertierungsprogramm Setup-Bibliothek konnte nicht geladen werden.|Die Konvertierer-Bibliothek konnte nicht geladen werden.|  
|ODBC_ERROR_INVALID_OPTION|Ungültige Transaktionsoption|Die *PvOption* Argument enthalten einen ungültigen Wert.|  
|ODBC_ERROR_OUT_OF_MEM|Nicht genügend Arbeitsspeicher.|Das Installationsprogramm konnte die Funktion aufgrund unzureichenden Arbeitsspeichers nicht ausgeführt werden.|  
  
## <a name="comments"></a>Kommentare  
 Wenn *HwndParent* null ist oder wenn *Wert*, *LpszPath*, oder *PvOption* ist ein null-Zeiger **SQLGetTranslator** gibt "false" zurück. Andernfalls zeigt die Liste der installierten Übersetzer im folgenden Dialogfeld an.  
  
 ![Select Konvertierer (Dialogfeld)](../../../odbc/reference/syntax/media/ch23j.gif "CH23J")  
  
 Wenn *Wert* enthält den Namen eines gültigen Konvertierer es aktiviert ist. Andernfalls \<Nein Konvertierer > ausgewählt ist.  
  
 Wenn der Benutzer entscheidet \<Nein Konvertierer >, den Inhalt der *Wert*, *LpszPath*, und *PvOption* sind nicht berührt. **SQLGetTranslator** legt *PcbNameOut* und *PcbPathOut* 0 und gibt "true".  
  
 Wenn der Benutzer ein Konvertierungsprogramm **SQLGetTranslator** Aufrufe **ConfigTranslator** im Setup-DLL für das Konvertierungsprogramm. Wenn **ConfigTranslator** gibt "false" **SQLGetTranslator** gibt zurück, um das Dialogfeld. Wenn **ConfigTranslator** gibt "true", **SQLGetTranslator** gibt "true", zusammen mit der Option ausgewählten Konvertierer, Name, Path und Übersetzung zurück.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Konfigurieren ein Konvertierungsprogramm|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|Abrufen einer Übersetzung-Attribut|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Wenn eine Übersetzung-Attribut|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|

---
title: SQLDataSourceToDriver Funktion | Microsoft Docs
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
apiname: SQLDataSourceToDriver
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLDataSourceToDriver
helpviewer_keywords: SQLDataSourceToDriver function [ODBC]
ms.assetid: 0d87fcac-30a0-4303-ad8f-a5b53f4b428d
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4d09d649bc53a08ff7389413882bb338d9713ffc
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqldatasourcetodriver-function"></a>SQLDataSourceToDriver-Funktion
**SQLDataSourceToDriver** Supportstranslations für ODBC-Treiber. Diese Funktion wird nicht von ODBC-fähigen Anwendungen aufgerufen wird. Anwendungen fordern Übersetzung über **SQLSetConnectAttr**. Die zugeordneten Treibers Untersuchen der *Verbindungshandle* im angegebenen **SQLSetConnectAttr** Ruft die angegebene DLL zum Ausführen von Übersetzungen für alle Daten, die aus der Datenquelle für den Treiber. Eine Standard-Konvertierungs-DLL kann in der ODBC-Initialisierungsdatei angegeben werden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BOOL SQLDataSourceToDriver(  
     UDWORD     fOption,  
     SWORD      fSqlType,  
     PTR        rgbValueIn,  
     SDWORD     cbValueIn,  
     PTR        rgbValueOut,  
     SDWORD     cbValueOutMax,  
     SDWORD *   pcbValueOut,  
     UCHAR *    szErrorMsg,  
     SWORD      cbErrorMsgMax,  
     SWORD *    pcbErrorMsg);  
```  
  
## <a name="arguments"></a>Argumente  
 *fOption*  
 [Eingabe] Der Optionswert.  
  
 *fSqlType*  
 [Eingabe] Der SQL-Datentyp. Dieses Argument weist den Treiber wie konvertiert *RgbValueIn* in eine Form, die von der Anwendung zulässig. Eine Liste der gültigen SQL-Datentypen, finden Sie unter der [SQL-Datentypen](../../../odbc/reference/appendixes/sql-data-types.md) Abschnitt im Anhang D:-Datentypen.  
  
 *rgbValueIn*  
 [Eingabe] Der Wert zu übersetzen.  
  
 *cbValueIn*  
 [Eingabe] Länge des *RgbValueIn*.  
  
 *rgbValueOut*  
 [Ausgabe] Ergebnis der Übersetzung.  
  
> [!NOTE]  
>  Konvertierungs-DLL beendet nicht Null-Wert.  
  
 *cbValueOutMax*  
 [Eingabe] Länge des *RgbValueOut*.  
  
 *pcbValueOut*  
 [Ausgabe] Die Gesamtanzahl der Bytes (ausgenommen die Null-Terminierung Byte) zur Rückgabe in *RgbValueOut*.  
  
 Für Zeichen- oder Binärdaten darstellen, ist dies größer als oder gleich *CbValueOutMax*, die Daten in *RgbValueOut* auf abgeschnitten *CbValueOutMax* Bytes.  
  
 Für alle anderen Datentypen den Wert der *CbValueOutMax* wird ignoriert, und die Übersetzung DLL setzt voraus, dass die Größe des *RgbValueOut* ist die Größe der Standard-C-Datentyp des SQL-Datentyps mit angegeben*fSqlType*.  
  
 Die *PcbValueOut* -Argument ein null-Zeiger sein.  
  
 *von SQLDiagRec()*  
 [Ausgabe] Zeiger auf Speicher für eine Fehlermeldung angezeigt. Dies ist eine leere Zeichenfolge, es sei denn, die Übersetzung ist fehlgeschlagen.  
  
 *cbErrorMsgMax*  
 [Eingabe] Länge des *von SQLDiagRec()*.  
  
 *pcbErrorMsg*  
 [Ausgabe] Zeiger auf die Gesamtanzahl der Bytes (ausgenommen die Null-Terminierung Byte) zur Rückgabe in *von SQLDiagRec()*. Ist dies größer als oder gleich *CbErrorMsg*, die Daten in *von SQLDiagRec()* auf abgeschnitten *CbErrorMsgMax* minus der Null-Abschlusszeichen. Die *PcbErrorMsg* -Argument ein null-Zeiger sein.  
  
## <a name="returns"></a>Rückgabewert  
 "True", wenn die Verschiebung erfolgreich "false" war, wenn die Übersetzung fehlgeschlagen ist.  
  
## <a name="comments"></a>Kommentare  
 Der Treiber ruft **SQLDataSourceToDriver** übersetzen Alldata (Resultsetdaten, Tabellennamen, Spaltennamen, Zeilenanzahl, Fehlermeldungen usw.) Datenquelle Übergabe von Daten an den Treiber. Die Übersetzung DLL möglicherweise einige Daten, je nach Typ der Daten und den Zweck des Konvertierungs-DLL nicht übersetzt; eine DLL, die Zeichendaten aus einer Codeseite in eine andere übersetzt ignoriert beispielsweise alle numerische und die binäre Daten.  
  
 Der Wert der *fOption* festgelegt ist, auf den Wert der *vParam* angegeben, indem **SQLSetConnectAttr** mit dem SQL_ATTR_TRANSLATE_OPTION-Attribut. Es ist eine 32-Bit-Wert, der für eine angegebene Übersetzung DLL eine besondere Bedeutung hat. Es kann z. B. angeben, dass ein bestimmter Zeichen Übersetzung festgelegt.  
  
 Wenn für der gleiche Puffer angegeben ist *RgbValueIn* und *RgbValueOut*, die Umwandlung von Daten in den Puffer in Ort ausgeführt werden.  
  
 Obwohl *CbValueIn*, *CbValueOutMax*, und *PcbValueOut* sind vom Typ SDWORD, **SQLDataSourceToDriver** nicht notwendigerweise unterstützen Sie große Zeiger.  
  
 Wenn **SQLDataSourceToDriver** gibt "false", Abschneiden von Daten möglicherweise während der Übersetzung aufgetreten sind. Wenn *PcbValueOut* (die Anzahl der Bytes in den Ausgabepuffer des zurückzugebenden verfügbar) ist größer als *CbValueOutMax* (die Länge des Ausgabepuffers), und klicken Sie dann die abgeschnittenen Daten. Der Treiber muss bestimmen, ob das Abschneiden akzeptabel. Wenn nicht abgeschnitten die **SQLDataSourceToDriver** "false" aufgrund eines anderen Fehlers zurückgegeben. In beiden Fällen wird eine entsprechende Fehlermeldung zurückgegeben, *von SQLDiagRec()*.  
  
 Weitere Informationen zum Übersetzen von Daten finden Sie unter [Übersetzung DLLs](../../../odbc/reference/develop-app/translation-dlls.md).  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Übersetzen von Daten an die Datenquelle gesendet werden|[SQLDriverToDataSource](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|  
|Die Einstellung der Verbindungsattribut zurückgeben|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Ein Verbindungsattribut festlegen|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|

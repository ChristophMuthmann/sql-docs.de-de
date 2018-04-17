---
title: SQLDriverToDataSource Funktion | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLDriverToDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDriverToDataSource
helpviewer_keywords:
- SQLDriverToDataSource function [ODBC]
ms.assetid: 0de28eb5-8aa9-43e4-a87f-7dbcafe800dc
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f1dcb53a08e3e20457a3ad616cd7b3d45fec2962
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqldrivertodatasource-function"></a>SQLDriverToDataSource-Funktion
**SQLDriverToDataSource** Übersetzungen für ODBC-Treiber unterstützt. Diese Funktion wird nicht von ODBC-fähigen Anwendungen aufgerufen wird. Anwendungen fordern Übersetzung über **SQLSetConnectAttr**. Die zugeordneten Treibers Untersuchen der *Verbindungshandle* im angegebenen **SQLSetConnectAttr** Ruft die angegebene DLL um Übersetzungen für alle Daten, die aus dem Treiber mit der Datenquelle auszuführen. Eine Standard-Konvertierungs-DLL kann in der ODBC-Initialisierungsdatei angegeben werden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BOOL SQLDriverToDataSource(  
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
 [Eingabe] Der ODBC-SQL-Datentyp. Dieses Argument weist den Treiber wie konvertiert *RgbValueIn* in eine Form, die von der Datenquelle akzeptabel. Eine Liste der gültigen SQL-Datentypen, finden Sie unter [SQL-Datentypen](../../../odbc/reference/appendixes/sql-data-types.md).  
  
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
 Der Treiber ruft **SQLDriverToDataSource** übersetzen Sie alle Daten (SQL-Anweisungen, Parameter usw.) aus dem Treiber an die Datenquelle übergeben. Die Übersetzung DLL möglicherweise einige Daten, je nach Typ der Daten und den Zweck des Konvertierungs-DLL nicht übersetzt. Eine DLL, die Zeichendaten aus einer Codeseite in eine andere übersetzt ignoriert beispielsweise alle numerische und die binäre Daten.  
  
 Der Wert der *fOption* festgelegt ist, auf den Wert der *vParam* angegeben, indem **SQLSetConnectAttr** mit dem SQL_ATTR_TRANSLATE_OPTION-Attribut. Es ist eine 32-Bit-Wert, der für eine angegebene Übersetzung DLL eine besondere Bedeutung hat. Es kann z. B. angeben, dass ein bestimmter Zeichen Übersetzung festgelegt.  
  
 Wenn für der gleiche Puffer angegeben ist *RgbValueIn* und *RgbValueOut*, die Umwandlung von Daten in den Puffer in Ort ausgeführt werden.  
  
 Obwohl *CbValueIn*, *CbValueOutMax*, und *PcbValueOut* sind vom Typ SDWORD, **SQLDriverToDataSource** nicht notwendigerweise unterstützen Sie große Zeiger.  
  
 Wenn **SQLDriverToDataSource** gibt "false", Abschneiden von Daten möglicherweise während der Übersetzung aufgetreten sind. Wenn *PcbValueOut* (die Anzahl der Bytes in den Ausgabepuffer des zurückzugebenden verfügbar) ist größer als *CbValueOutMax* (die Länge des Ausgabepuffers), und klicken Sie dann die abgeschnittenen Daten. Der Treiber muss bestimmen, und zwar unabhängig davon, ob das Abschneiden akzeptabel war. Wenn nicht abgeschnitten die **SQLDriverToDataSource** "false" aufgrund eines anderen Fehlers zurückgegeben. In beiden Fällen wird eine entsprechende Fehlermeldung zurückgegeben, *von SQLDiagRec()*.  
  
 Weitere Informationen zum Übersetzen von Daten finden Sie unter [Übersetzung DLLs](../../../odbc/reference/develop-app/translation-dlls.md).  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Übersetzen von Daten zurückgegeben aus der Datenquelle|[SQLDataSourceToDriver](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|  
|Die Einstellung der Verbindungsattribut zurückgeben|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Ein Verbindungsattribut festlegen|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|

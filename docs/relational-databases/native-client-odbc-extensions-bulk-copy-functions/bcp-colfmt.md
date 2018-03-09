---
title: Bcp_colfmt | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- bcp_colfmt
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_colfmt function
ms.assetid: 5c3b6299-80c7-4e84-8e69-4ff33009548e
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c19dd268f958bc35f6e41fd6a6283ca23beb60e9
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/24/2018
---
# <a name="bcpcolfmt"></a>bcp_colfmt
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Gibt das Quell- oder Zielformat der Daten in einer Benutzerdatei an. Bei Verwendung als Quellformat **Bcp_colfmt** gibt das Format einer vorhandenen Datendatei verwendet, die als Quelle der Daten in einem Massenkopiervorgang in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tabelle. Bei Verwendung als Zielformat wird die Datendatei wird erstellt mithilfe der angegebenen mit Spaltenformate **Bcp_colfmt**.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
RETCODE bcp_colfmt (  
        HDBC hdbc,  
        INT idxUserDataCol,  
        BYTE eUserDataType,  
        INT cbIndicator,  
        DBINT cbUserData,  
        LPCBYTE pUserDataTerm,  
        INT cbUserDataTerm,  
        INT idxServerCol);  
```  
  
## <a name="arguments"></a>Argumente  
 *HDBC*  
 Das für den Massenkopiervorgang aktivierte ODBC-Verbindungshandle.  
  
 *idxUserDataCol*  
 Die Ordnungsnummer der Spalte in der Benutzerdatendatei, für die das Format angegeben wird. Die erste Spalte ist 1.  
  
 *eUserDataType*  
 Der Datentyp dieser Spalte in der Benutzerdatei. Falls abweichend vom Datentyp der entsprechenden Spalte in der Datenbanktabelle (*IdxServerColumn*), das Massenkopieren konvertiert die Daten Wenn möglich.  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]führte die Unterstützung für SQLXML und SQLUDT Datentyptoken in der *eUserDataType* Parameter.  
  
 Die *eUserDataType* Parameter aufgelistet, indem die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datentyptoken in sqlncli.h, nicht die ODBC C-datentypenumeratoren. Sie können beispielsweise mithilfe des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-spezifischen SQLCHARACTER-Typs eine Zeichenfolge vom ODBC-Typ SQL_C_CHAR angeben.  
  
 Um die Standarddatendarstellung für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datentyp anzugeben, legen Sie diesen Parameter auf 0 fest.  
  
 Für einen Massenkopiervorgang aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in eine Datei, wenn *eUserDataType* SQLDECIMAL oder sqlnumeric festgelegt ist:  
  
-   Wenn die Quellspalte nicht **decimal** oder **numerischen**, die standardmäßige Genauigkeit und Dezimalstellenanzahl verwendet werden.  
  
-   Wenn die Quellspalte **decimal** oder **numerischen**, die Genauigkeit und Dezimalstellen der Quellspalte verwendet werden.  
  
 *cbIndicator*  
 Die Länge eines Längen-/NULL-Indikators innerhalb der Spaltendaten in Byte. Gültige Indikatorlängenwerte sind 0 (wenn kein Indikator verwendet wird), 1, 2, 4 oder 8.  
  
 Legen Sie diesen Parameter auf SQL_VARLEN_DATA fest, um die Verwendung eines standardmäßigen Massenkopierindikators anzugeben.  
  
 Indikatoren werden im Speicher direkt vor allen anderen Daten angezeigt. In der Datendatei werden sie direkt vor den Daten, auf die sie sich beziehen, angezeigt.  
  
 Wird mehr als eine Methode zur Angabe der Länge der Datendateispalte verwendet (z. B. ein Indikator und eine maximale Spaltenlänge oder ein Indikator und eine Abschlusszeichensequenz), wird beim Massenkopieren die Methode ausgewählt, die zu der kleineren zu kopierenden Datenmenge führt.  
  
 Datendateien, die durch Massenkopieren generiert wurden, wobei das Datenformat nicht durch Benutzereingriff angepasst wird, enthalten Indikatoren, wenn die Spaltendaten eine unterschiedliche Länge haben oder die Spalte NULL als Wert akzeptieren kann.  
  
 *cbUserData*  
 Die maximale Länge (in Byte) der Daten dieser Spalte in der Benutzerdatei, ohne die Länge eines Längenindikators oder Abschlusszeichens.  
  
 Festlegen von *CbUserData* auf SQL_NULL_DATA wird angegeben, dass alle Werte in der Spalte "Daten" sind, oder auf NULL festgelegt werden soll.  
  
 Festlegen von *CbUserData* auf SQL_VARLEN_DATA gibt an, dass das System die Länge der Daten in jeder Spalte bestimmen soll. Für einige Spalten könnte dies bedeuten, dass ein Längen-/NULL-Indikator generiert wird, der den Daten in einer Kopie von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vorangestellt wird, oder dass der Indikator in Daten, die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kopiert werden, erwartet wird.  
  
 Für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Zeichen und Binärdatentypen *CbUserData* bcp_length_variable, bcp_length_null, 0 oder ein positiver Wert sein kann. Wenn *CbUserData* auf sql_varlen_data festgelegt, das System verwendet entweder den Längenindikator, sofern vorhanden, oder eine abschlusszeichensequenz, um die Länge der Daten zu bestimmen. Wenn sowohl ein Längenindikator als auch eine Abschlusszeichensequenz angegeben sind, wird beim Massenkopieren der Wert verwendet, der zu der kleineren zu kopierenden Datenmenge führt. Wenn *CbUserData* auf sql_varlen_data festgelegt, die Daten der Typ ist ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Zeichen- oder Binärdatentyp ist und weder ein Längenindikator noch eine abschlusszeichensequenz angegeben ist, gibt das System eine Fehlermeldung zurück.  
  
 Wenn *CbUserData* 0 oder ein positiver Wert sein, das System verwendet *CbUserData* als maximale Datenlänge. Allerdings If, zusätzlich zu einem positiven *CbUserData*, eine Länge Längenindikator oder eine abschlusszeichensequenz angegeben ist, bestimmt das System die Datenlänge mithilfe der Methode, führt die geringste Menge an Daten, die kopiert werden.  
  
 Die *CbUserData* Wert stellt die Anzahl der Datenbytes dar. Zeichendaten durch Unicode-Zeichen, und klicken Sie dann auf einen positiven dargestellt *CbUserData* Parameterwert darstellt, die Anzahl der Zeichen multipliziert mit der Größe in Bytes, der einzelnen Zeichen.  
  
 *pUserDataTerm*  
 Die Abschlusszeichensequenz, die für diese Spalte verwendet werden soll. Dieser Parameter ist in erster Linie für Zeichendatentypen nützlich, da alle anderen Typen eine feste Länge besitzen oder, im Falle von Binärdaten, einen Indikator für die Länge erfordern, um die Anzahl der vorhandenen Bytes präzise zu erfassen.  
  
 Legen Sie diesen Parameter auf NULL fest, um zu vermeiden, dass extrahierte Daten terminiert werden, oder um anzugeben, dass Daten in einer Benutzerdatei nicht terminiert werden.  
  
 Wird mehr als eine Methode zur Angabe der Länge der Benutzerdateispalte verwendet (z. B. ein Abschlusszeichen und ein Längenindikator oder ein Abschlusszeichen und eine maximale Spaltenlänge), wird beim Massenkopieren die Methode ausgewählt, die zu der kleineren zu kopierenden Datenmenge führt.  
  
 Die API für das Massenkopieren führt nach Bedarf eine Zeichenkonvertierung von Unicode in MBCS aus. Stellen Sie unbedingt sicher, dass sowohl die Bytezeichenfolge des Abschlusszeichens und die Länge der Bytezeichenfolge richtig festgelegt werden.  
  
 *cbUserDataTerm*  
 Die Länge (in Byte) der Abschlusszeichensequenz, die für diese Spalte verwendet werden soll. Wenn kein Abschlusszeichen vorhanden ist oder in den Daten gewünscht wird, legen Sie diesen Wert auf 0 fest.  
  
 *idxServerCol*  
 Ist die Ordnungsposition der Spalte in der Datenbanktabelle. Die erste Spaltennummer ist 1. Die Ordnungsposition einer Spalte wird von [SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md)ausgegeben.  
  
 Wenn dieser Wert 0 ist, wird beim Massenkopieren die Spalte in der Datendatei ignoriert.  
  
## <a name="returns"></a>Rückgabewert  
 SUCCEED oder FAIL.  
  
## <a name="remarks"></a>Hinweise  
 Die **Bcp_colfmt** -Funktion können Sie das Benutzerdateiformat für das Massenkopieren angeben. Für Massenkopieren besteht ein Format aus folgenden Bestandteilen:  
  
-   Eine Zuordnung von Benutzerdateispalten zu Datenbankspalten  
  
-   Der Datentyp der einzelnen Benutzerdateispalten  
  
-   Die Länge des optionalen Indikators für jede Spalte  
  
-   Die maximale Länge der Daten pro Benutzerdateispalte  
  
-   Die optionale abschließende Bytesequenz für jede Spalte  
  
-   Die Länge der optionalen abschließenden Bytesequenz  
  
 Jeder Aufruf von **Bcp_colfmt** gibt das Format für eine benutzerdateispalte an. Angenommen, um die Standardeinstellungen für drei Spalten in einer Benutzerdatendatei fünf Spalten zu ändern, rufen Sie zuerst [Bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md)**(5)**, und rufen dann **Bcp_colfmt** fünf Mal mit drei dieser Aufrufe Ihr benutzerdefiniertes Format festgelegt. Legen Sie für die verbleibenden zwei Aufrufe *eUserDataType* auf 0 und *CbIndicator*, *CbUserData*, und *CbUserDataTerm* auf 0, SQL_VARLEN _Data, und 0 bzw. Mit diesem Verfahren werden alle fünf Spalten kopiert, drei mit dem benutzerdefinierten Format und zwei mit dem Standardformat.  
  
 Für *CbIndicator*, ein Wert von 8, um einen großen Werttyp anzugeben ist jetzt gültig. Wenn das Präfix für ein Feld angegeben wird, dessen entsprechende Spalte den neuen max-Typ aufweist, kann dafür nur 8 festgelegt werden. Weitere Informationen finden Sie unter [Bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md).  
  
 Die **Bcp_columns** -Funktion muss aufgerufen werden, bevor Aufrufe **Bcp_colfmt**.  
  
 Rufen Sie **Bcp_colfmt** einmal für jede Spalte in der Benutzerdatei.  
  
 Aufrufen von **Bcp_colfmt** mehr als einmal für eine Spalte wird ein Fehler verursacht.  
  
 Sie brauchen nicht alle Daten in einer Benutzerdatei in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tabelle kopieren. Um eine Spalte zu überspringen, geben Sie das Format der Daten für die Spalte an, indem die *IdxServerCol* Parameter auf 0. Wenn Sie eine Spalte überspringen möchten, müssen Sie ihren Typ angeben.  
  
 Die [Bcp_writefmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-writefmt.md) Funktion kann verwendet werden, um die Formatspezifikation persistent zu speichern.  
  
## <a name="bcpcolfmt-support-for-enhanced-date-and-time-features"></a>'bcp_colfmt'-Unterstützung für erweiterte Funktionen für Datum und Uhrzeit  
 Informationen zu den Arten der Verwendung der *eUserDataType* -Parameter für Datum/Uhrzeit-Typen finden Sie unter [Massenkopieränderungen für erweiterte Datums- und Uhrzeittypen &#40; OLE DB und ODBC &#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  
  
 Weitere Informationen finden Sie unter [Datum und Uhrzeit-Verbesserungen &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen zum Massenkopieren](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  

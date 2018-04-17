---
title: Bcp_setcolfmt | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- bcp_setcolfmt
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_setcolfmt function
ms.assetid: afb47987-39e7-4079-ad66-e0abf4d4c72b
caps.latest.revision: 36
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 874c1231997c04069c2f508f5a7529a8950eb261
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="bcpsetcolfmt"></a>bcp_setcolfmt
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Die **Bcp_setcolfmt** Funktion ersetzt die [Bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md). Beim Angeben der spaltensortierung der **Bcp_setcolfmt** -Funktion verwendet werden muss. [Bcp_setbulkmode](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setbulkmode.md) können verwendet werden, um mehr als ein Spaltenformat anzugeben.  
  
 Diese Funktion bietet einen flexiblen Ansatz für das Angeben des Spaltenformats in einem Massenkopiervorgang. Sie wird verwendet, um einzelne Spaltenformatattribute festzulegen. Jeder Aufruf von **Bcp_setcolfmt** legt ein spaltenformatattribut fest.  
  
 Die **Bcp_setcolfmt** Funktion gibt die Quelle oder Ziel-Format der Daten in einer Benutzerdatei an. Bei Verwendung als Quellformat **Bcp_setcolfmt** gibt das Format einer vorhandenen Datendatei an, die als Daten in einem Massenkopiervorgang in einer Tabelle in der Datenquelle verwendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Bei Verwendung als Zielformat wird die Datendatei wird erstellt mithilfe der angegebenen mit Spaltenformate **Bcp_setcolfmt**.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
RETCODE bcp_setcolfmt (  
        HDBC hdbc,  
        INT field,  
        INT property,  
        void* pValue,  
        INT cbValue);  
```  
  
## <a name="arguments"></a>Argumente  
 *HDBC*  
 Das für den Massenkopiervorgang aktivierte ODBC-Verbindungshandle.  
  
 *field*  
 Die Spaltenordnungszahl, für die die Eigenschaft festgelegt wird  
  
 *Eigenschaft*  
 Eine der Eigenschaftskonstanten. Eigenschaftskonstanten werden in dieser Tabelle definiert.  
  
|Eigenschaft|Wert|Description|  
|--------------|-----------|-----------------|  
|BCP_FMT_TYPE|BYTE|Der Datentyp dieser Spalte in der Benutzerdatei. Wenn die Daten nicht mit dem Datentyp der entsprechenden Spalte in der Datenbanktabelle übereinstimmen, werden die Daten, wenn möglich, durch das Massenkopieren konvertiert.<br /><br /> Der BCP_FMT_TYPE-Parameter wird von den SQL Server-Datentyptoken in sqlncli.h anstelle der ODBC C-Datentypenumeratoren aufgelistet. Sie können beispielsweise eine Zeichenfolge, ODBC-Typ SQL_C_CHAR, mithilfe des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-spezifischen SQLCHARACTER-Typs angeben.<br /><br /> Um die Standarddatendarstellung für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datentyp anzugeben, legen Sie diesen Parameter auf 0 fest.<br /><br /> Für einen Massenkopiervorgang aus SQL Server in eine Datei, wenn BCP_FMT_TYPE SQLDECIMAL oder sqlnumeric festgelegt, ist, wenn die Quellspalte nicht **decimal** oder **numerischen**, die standardmäßige Genauigkeit und Dezimalstellenanzahl verwendet werden. Andernfalls, wenn die Quellspalte **decimal** oder **numerischen**, die Genauigkeit und Dezimalstellen der Quellspalte verwendet werden.|  
|BCP_FMT_INDICATOR_LEN|INT|Die Länge des Indikators (Präfix) in Bytes<br /><br /> Die Länge eines Längen-/NULL-Indikators innerhalb der Spaltendaten in Bytes. Gültige Indikatorlängenwerte sind 0 (wenn kein Indikator verwendet wird), 1, 2 oder 4.<br /><br /> Legen Sie diesen Parameter auf SQL_VARLEN_DATA fest, um die Verwendung eines standardmäßigen Massenkopierindikators anzugeben.<br /><br /> Indikatoren werden im Speicher direkt vor allen anderen Daten angezeigt. In der Datendatei werden sie direkt vor den Daten, auf die sie sich beziehen, angezeigt.<br /><br /> Wird mehr als eine Methode zur Angabe der Länge der Datendateispalte verwendet (z. B. ein Indikator und eine maximale Spaltenlänge oder ein Indikator und eine Abschlusszeichensequenz), wird beim Massenkopieren die Methode ausgewählt, die zu der kleineren zu kopierenden Datenmenge führt.<br /><br /> Datendateien, die durch Massenkopieren generiert wurden, wobei das Datenformat nicht durch Benutzereingriff angepasst wird, enthalten Indikatoren, wenn die Spaltendaten eine unterschiedliche Länge haben oder die Spalte NULL als Wert akzeptieren kann.|  
|BCP_FMT_DATA_LEN|DBINT|Die Länge der Daten (Spaltenlänge) in Bytes<br /><br /> Dies ist die maximale Länge (in Bytes) der Daten dieser Spalte in der Benutzerdatei, ohne die Länge eines Längenindikators oder Abschlusszeichens.<br /><br /> Durch Festlegen von BCP_FMT_DATA_LEN auf SQL_NULL_DATA wird angegeben, dass alle Werte in der Datendateispalte auf NULL festgelegt sind oder sein sollten.<br /><br /> Wird BCP_FMT_DATA_LEN auf SQL_VARLEN_DATA festgelegt, bedeutet dies, dass das System die Länge der Daten für jede Spalte bestimmen soll. Für einige Spalten könnte dies bedeuten, dass ein Längen-/NULL-Indikator generiert wird, der den Daten in einer Kopie von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vorangestellt wird, oder dass der Indikator in Daten, die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kopiert werden, erwartet wird.<br /><br /> BCP_FMT_DATA_LEN kann für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Zeichen und Binärdatentypen BCP_LENGTH_VARIABLE, BCP_LENGTH_NULL, 0 oder ein positiver Wert sein. Wenn BCP_FMT_DATA_LEN auf SQL_VARLEN_DATA festgelegt ist, verwendet das System entweder den Längenindikator, sofern vorhanden, oder eine Abschlusszeichensequenz, um die Länge der Daten zu bestimmen. Wenn sowohl ein Längenindikator als auch eine Abschlusszeichensequenz angegeben sind, wird beim Massenkopieren der Wert verwendet, der zu der kleineren zu kopierenden Datenmenge führt. Ist BCP_FMT_DATA_LEN auf SQL_VARLEN_DATA festgelegt, ist der Datentyp ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Zeichen oder -Binärtyp. Ist weder ein Längenindikator noch eine Abschlusszeichensequenz angegeben, gibt das System eine Fehlermeldung zurück.<br /><br /> Wenn BCP_FMT_DATA_LEN 0 oder ein positiver Wert ist, verwendet das System BCP_FMT_DATA_LEN als maximale Datenlänge. Wenn jedoch zusätzlich zu einem positiven BCP_FMT_DATA_LEN-Wert ein Längenindikator oder eine Abschlusszeichensequenz angegeben ist, bestimmt das System die Datenlänge mithilfe der Methode, die zu der kleineren zu kopierenden Datenmenge führt.<br /><br /> Der BCP_FMT_DATA_LEN-Wert stellt die Anzahl der Datenbytes dar. Werden Zeichendaten durch Unicode-Zeichen dargestellt, repräsentiert ein positiver BCP_FMT_DATA_LEN-Parameterwert die Anzahl der Zeichen multipliziert mit der Größe (in Bytes) der einzelnen Zeichen.|  
|BCP_FMT_TERMINATOR|LPCBYTE|Zeiger auf die Abschlusszeichensequenz (entweder ANSI oder Unicode), die für diese Spalte verwendet werden soll. Dieser Parameter ist in erster Linie für Zeichendatentypen nützlich, da alle anderen Typen eine feste Länge besitzen oder, im Falle von Binärdaten, einen Indikator für die Länge erfordern, um die Anzahl der vorhandenen Bytes präzise zu erfassen.<br /><br /> Legen Sie diesen Parameter auf NULL fest, um zu vermeiden, dass extrahierte Daten terminiert werden, oder um anzugeben, dass Daten in einer Benutzerdatei nicht terminiert werden.<br /><br /> Wird mehr als eine Methode zur Angabe der Länge der Benutzerdateispalte verwendet (z. B. ein Abschlusszeichen und ein Längenindikator oder ein Abschlusszeichen und eine maximale Spaltenlänge), wird beim Massenkopieren die Methode ausgewählt, die zu der kleineren zu kopierenden Datenmenge führt.<br /><br /> Die API für das Massenkopieren führt nach Bedarf eine Zeichenkonvertierung von Unicode in MBCS aus. Stellen Sie unbedingt sicher, dass sowohl die Bytezeichenfolge des Abschlusszeichens und die Länge der Bytezeichenfolge richtig festgelegt werden.|  
|BCP_FMT_SERVER_COL|INT|Die Position einer Spalte innerhalb der Datenbank|  
|BCP_FMT_COLLATION|LPCSTR|Sortierungsname.|  
  
 *pValue*  
 Der Zeiger auf den zu verknüpfenden Wert an die *Eigenschaft*. Er ermöglicht es, jede Spaltenformateigenschaft einzeln festzulegen.  
  
 *cbvalue*  
 Die Länge des Puffers der Eigenschaft in Bytes.  
  
## <a name="returns"></a>Rückgabewert  
 SUCCEED oder FAIL.  
  
## <a name="remarks"></a>Hinweise  
 Diese Funktion ersetzt die **Bcp_colfmt** Funktion. Die Funktionalität des **Bcp_colfmt** finden Sie im **Bcp_setcolfmt** Funktion. Zusätzlich wird auch Unterstützung für Spaltensortierung bereitgestellt. Es wird empfohlen, die folgenden Spaltenformatattribute in der unten gegebenen Reihenfolge festzulegen:  
  
 BCP_FMT_SERVER_COL  
  
 BCP_FMT_DATA_LEN  
  
 BCP_FMT_TYPE  
  
 Die **Bcp_setcolfmt** -Funktion können Sie das Benutzerdateiformat für das Massenkopieren angeben. Für Massenkopieren besteht ein Format aus folgenden Bestandteilen:  
  
-   Eine Zuordnung von Benutzerdateispalten zu Datenbankspalten  
  
-   Der Datentyp der einzelnen Benutzerdateispalten  
  
-   Die Länge des optionalen Indikators für jede Spalte  
  
-   Die maximale Länge der Daten pro Benutzerdateispalte  
  
-   Die optionale abschließende Bytesequenz für jede Spalte  
  
-   Die Länge der optionalen abschließenden Bytesequenz  
  
 Jeder Aufruf von **Bcp_setcolfmt** gibt das Format für eine benutzerdateispalte an. Angenommen, um die Standardeinstellungen für drei Spalten in einer Benutzerdatendatei fünf Spalten zu ändern, rufen Sie zuerst [Bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md)**(5)**, und rufen dann **Bcp_setcolfmt** fünf Mal mit drei dieser Aufrufe Ihr benutzerdefiniertes Format festgelegt werden. Klicken Sie für die verbleibenden zwei Aufrufe BCP_FMT_TYPE auf 0 festgelegt, und legen Sie BCP_FMT_INDICATOR_LENGTH, BCP_FMT_DATA_LEN und *CbValue* auf 0, SQL_VARLEN_DATA und 0 bzw. Mit diesem Verfahren werden alle fünf Spalten kopiert, drei mit dem benutzerdefinierten Format und zwei mit dem Standardformat.  
  
 Die **Bcp_columns** Funktion aufgerufen werden muss, bevor **Bcp_setcolfmt**.  
  
 Rufen Sie **Bcp_setcolfmt** einmal für jede Eigenschaft jeder Spalte in der Benutzerdatei.  
  
 Sie müssen nicht alle Daten in einer Benutzerdatei in eine SQL Server-Tabelle kopieren. Um eine Spalte zu überspringen, geben Sie das Format der Daten für die Spalte an, indem Sie den BCP_FMT_SERVER_COL-Parameter auf 0 festlegen. Wenn Sie eine Spalte überspringen möchten, müssen Sie ihren Typ angeben.  
  
 Die [Bcp_writefmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-writefmt.md) Funktion kann verwendet werden, um die Formatspezifikation persistent zu speichern.  
  
## <a name="bcpsetcolfmt-support-for-enhanced-date-and-time-features"></a>bcp_setcolfmt-Unterstützung für erweiterte Funktionen für Datum und Uhrzeit  
 Mit der BCP_FMT_TYPE-Eigenschaft für Datums-/Uhrzeittypen verwendeten Typen werden als im angegebenen [Massenkopieränderungen für erweiterte Datums- und Uhrzeittypen &#40;OLE DB- und ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  
  
 Weitere Informationen finden Sie unter [Datum und Uhrzeit-Verbesserungen & #40; ODBC & #41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen zum Massenkopieren](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  

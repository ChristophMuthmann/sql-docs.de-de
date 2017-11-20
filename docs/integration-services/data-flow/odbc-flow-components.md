---
title: ODBC-Flusskomponenten | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cf751f1e-2348-4a77-904c-bd92c0d7d0ae
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bb47de9a618b4d83e961ff2e032861375b0d6c22
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="odbc-flow-components"></a>ODBC-Flusskomponenten
  In diesem Thema werden die erforderlichen Begriffe der Erstellung eines ODBC-Datenflusses mit [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]  
  
 Der Konnektor für Open Database Connectivity (ODBC) von Attunity für [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] erleichtert SSIS-Entwicklern das Erstellen von Paketen, mit denen Daten aus Datenbanken mit ODBC-Unterstützung geladen bzw. wieder entladen werden.  
  
 Der ODBC-Connector ist auf die Erzielung der optimalen Leistung ausgelegt, was das Laden (bzw. Entladen) von Daten in eine Datenbank mit ODBC-Unterstützung im [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]-Kontext betrifft.  
  
## <a name="benefits"></a>Vorteile  
 Die ODBC-Quelle und das ODBC-Ziel für [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] erhöhen die Wettbewerbsfähigkeit von SSIS in Projekten, in denen es um das Laden (bzw. Entladen) von Daten in Datenbanken mit ODBC-Unterstützung geht.  
  
 Sowohl für die ODBC-Quelle als auch für das ODBC-Ziel ist eine Datenintegration in Datenbanken mit ODBC-Aktivierung bei hoher Leistung möglich. Beide Komponenten können für die Verwendung mit Zeile-für-Zeile-Parameterarraybindungen für ODBC-Anbieter mit hoher Leistung konfiguriert werden, die diesen Bindungsmodus unterstützen, sowie für die Verwendung mit Einzelzeilen-Parameterbindungen für ODBC-Anbieter mit niedriger Leistung.  
  
## <a name="getting-started-with-the-odbc-source-and-destination"></a>Erste Schritte mit der ODBC-Quelle und dem ODBC-Ziel  
 Bevor Sie Pakete einrichten können, die [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]verwenden, müssen Sie die Verfügbarkeit der folgenden Elemente sicherstellen.  
  
-   [ODBC-Quelle](../../integration-services/data-flow/odbc-source.md)  
  
-   [ODBC-Ziel](../../integration-services/data-flow/odbc-destination.md)  
  
 Die ODBC-Quelle und das ODBC-Ziel stellen eine einfache Möglichkeit dar, Daten zu entladen und zu laden und aus einer Quelldatenbank mit ODBC-Unterstützung in eine Zieldatenbank mit ODBC-Unterstützung zu übertragen.  
  
 Um die Quelle oder das Ziel zum Laden oder Entladen von Daten zu verwenden, öffnen Sie in [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] ein neues [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]-Projekt. Ziehen Sie die Quelle oder das Ziel anschließend in die Entwurfsoberfläche von [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
-   Die ODBC-Quellkomponente liest Daten aus der Quelldatenbank mit ODBC-Unterstützung.  
  
 Sie können die ODBC-Quelle mit jedem Ziel oder jeder von SSIS unterstützten Transformationskomponente verbinden.  
  
 **Siehe auch:**  
  
 ODBC-Quelle  
  
 Quellen-Editor für ODBC (Seite Verbindungs-Manager)  
  
 Quellen-Editor für ODBC (Seite Fehlerausgabe)  
  
-   Das ODBC-Ziel lädt Daten in eine Datenbank mit ODBC-Unterstützung. Sie können das Ziel mit jeder Quelle oder jeder von SSIS unterstützten Transformationskomponente verbinden.  
  
 **Siehe auch:**  
  
 ODBC-Ziel  
  
 Ziel-Editor für ODBC (Verbindungs-Manager-Seite)  
  
 Ziel-Editor für ODBC (Seite "Fehlerausgabe")  
  
## <a name="operating-scenarios"></a>Betriebsszenarien  
 In diesem Abschnitt werden einige Hauptverwendungsarten von ODBC-Quell- und -Zielkomponenten beschrieben.  
  
### <a name="bulk-copy-data-from-sql-server-tables-to-any-odbc-supported-database-table"></a>Massenkopieren von Daten aus SQL Server-Tabellen in beliebige Datenbanktabellen mit ODBC-Unterstützung  
 Sie können die Komponenten verwenden, um für Daten das Massenkopieren aus einer oder mehreren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabellen in eine einzelne Datenbanktabelle mit ODBC-Unterstützung durchzuführen.  
  
 Im folgenden Beispiel wird gezeigt, wie Sie einen SSIS-Datenflusstask erstellen, mit dem Daten aus einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle extrahiert und in eine DB2-Tabelle geladen werden.  
  
-   Erstellen Sie in [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] ein [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]-Projekt.  
  
-   Erstellen Sie einen OLE DB-Verbindungs-Manager, der eine Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank herstellt, in der die zu kopierenden Daten enthalten sind.  
  
-   Erstellen Sie einen ODBC-Verbindungs-Manager, der einen lokal installierten DB2 ODBC-Treiber mit einem DSN verwendet, der auf eine lokale DB2-Datenbank oder DB2-Remotedatenbank verweist. In diese Datenbank werden die Daten aus der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank geladen.  
  
-   Ziehen Sie eine OLE DB-Quelle in die Entwurfsoberfläche. Konfigurieren Sie anschließend die Quelle, um die Daten aus der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank und der Tabelle mit den Daten abzurufen, die Sie extrahieren möchten. Verwenden Sie den OLE DB-Verbindungs-Manager, den Sie zuvor erstellt haben.  
  
-   Ziehen Sie ein ODBC-Ziel in die Entwurfsoberfläche, verbinden Sie die Quellausgabe mit dem ODBC-Ziel, und konfigurieren Sie dann das Ziel, um die Daten in die DB2-Tabelle mit den Daten zu laden, die Sie aus der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank extrahieren. Verwenden Sie den ODBC-Verbindungs-Manager, den Sie zuvor erstellt haben.  
  
### <a name="bulk-copy-data-from-odbc-supported-database-tables-to-any-sql-server-table"></a>Massenkopieren von Daten aus Datenbanktabellen mit ODBC-Unterstützung in beliebige SQL Server-Tabellen  
 Sie können die Komponenten verwenden, um für Daten das Massenkopieren aus einer oder mehreren Datenbanktabellen mit ODBC-Unterstützung in eine einzelne [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbanktabelle durchzuführen.  
  
 Im folgenden Beispiel wird gezeigt, wie Sie einen SSIS-Datenflusstask erstellen, bei dem Daten aus einer Sybase-Datenbanktabelle extrahiert und in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbanktabelle geladen werden.  
  
-   Erstellen Sie in [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] ein neues [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]  
  
-   Erstellen Sie einen ODBC-Verbindungs-Manager, der einen lokal installierten Sybase ODBC-Treiber mit einem DSN verwendet, der auf eine lokale Sybase-Datenbank oder Sybase-Remotedatenbank verweist. Die Daten werden in diese Datenbank extrahiert.  
  
-   Erstellen Sie einen OLE DB-Verbindungs-Manager, der eine Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank herstellt, in die Sie die Daten laden möchten.  
  
-   Ziehen Sie eine ODBC-Quelle in die Entwurfsoberfläche. Konfigurieren Sie anschließend die Quelle, um die zu kopierenden Daten aus der entsprechenden Sybase-Tabelle abzurufen. Verwenden Sie den ODBC-Verbindungs-Manager, den Sie zuvor erstellt haben.  
  
-   Ziehen Sie ein OLE DB-Ziel in die Entwurfsoberfläche, verbinden Sie die Quellausgabe mit dem OLE DB-Ziel, und konfigurieren Sie dann das Ziel, um die Daten in die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle mit den Daten zu laden, die Sie aus der Sybase-Datenbank extrahieren. Verwenden Sie den OLE DB-Verbindungs-Manager, den Sie zuvor erstellt haben.  
  
## <a name="supported-data-types"></a>Unterstützte Datentypen  
 Die SSIS-Komponenten für ODBC-Massenvorgänge unterstützen alle integrierten ODBC-Datentypen sowie große Objekte (CLOBs und BLOBs).  
  
Es ist keine Datentypunterstützung für erweiterbare C-Typen vorhanden, die in der ODBC 3.8-Spezifikation beschrieben werden.In der folgenden Tabelle wird beschrieben, welche SSIS-Datentypen für die einzelnen ODBC-SQL-Typen verwendet werden. Ein SSIS-Entwickler kann die Standardzuordnung überschreiben und einen anderen SSIS-Datentyp für Eingabe-/Ausgabespalten angeben, ohne dass sich dies auf die Leistung für die erforderlichen Datenkonvertierungen auswirkt.  
  
|ODBC-SQL-Typ|SSIS-Datentyp|Kommentare|  
|-----------------|------------------|------------|  
|SQL_BIT|DT_BOOL||  
|SQL_TINYINT|DT_I1<br /><br />DT_UI1|SQL-Datentypen werden SSIS-Typen ohne Vorzeichen zugeordnet (DT_UI1, DT_UI2, DT_UI4, DT_UI8), wenn der ODBC-Treiber UNSIGNED_ATTRIBUTE für diesen SQL-Datentyp auf SQL_TRUE festlegt.|  
|SQL_SMALLINT|DT_I2<br /><br />DT_UI2|SQL-Datentypen werden SSIS-Typen ohne Vorzeichen zugeordnet (DT_UI1, DT_UI2, DT_UI4, DT_UI8), wenn der ODBC-Treiber UNSIGNED_ATTRIBUTE für diesen SQL-Datentyp auf SQL_TRUE festlegt.|  
|SQL_INTEGER|DT_I4<br /><br />DTUI4|SQL-Datentypen werden SSIS-Typen ohne Vorzeichen zugeordnet (DT_UI1, DT_UI2, DT_UI4, DT_UI8), wenn der ODBC-Treiber UNSIGNED_ATTRIBUTE für diesen SQL-Datentyp auf SQL_TRUE festlegt.|  
|SQL_BIGINT|DT_I8<br /><br />DT_UI8|SQL-Datentypen werden SSIS-Typen ohne Vorzeichen zugeordnet (DT_UI1, DT_UI2, DT_UI4, DT_UI8), wenn der ODBC-Treiber UNSIGNED_ATTRIBUTE für diesen SQL-Datentyp auf SQL_TRUE festlegt.|  
|SQL_DOUBLE|DT_R8|  
|SQL_FLOAT|DT_R8|  
|SQL_REAL|DT_R4|  
|SQL_NUMERIC (p,s)|DT_NUMERIC (p,s)|Der numerische Datentyp wird DT_NUMERIC zugeordnet, wenn Folgendes gilt: P ist größer oder gleich 38, S ist größer oder gleich 0 und S ist kleiner oder gleich P.|  
||DT_R8|Der numerische Datentyp wird DT_R8 zugeordnet, wenn mindestens eine der folgenden Bedingungen erfüllt ist:<br /><br />Genauigkeit ist größer als 38<br /><br />Skalierung ist kleiner als 0 (null)<br /><br />Skalierung ist größer als 38<br /><br />Skalierung ist größer als Genauigkeit|  
||DT_CY|Der numerische Datentyp wird DT_CY zugeordnet, wenn er als money-Datentyp deklariert wird.|  
|SQL_DECIMAL (p,s)|DT_NUMERIC (p,s)|Der decimal-Datentyp wird DT_NUMERIC zugeordnet, wenn Folgendes gilt: P ist größer oder gleich 38, S ist größer oder gleich 0 und S ist kleiner oder gleich P.|  
||DT_R8|Der decimal-Datentyp wird DT_R8 zugeordnet, wenn mindestens eine der folgenden Bedingungen erfüllt ist:<br /><br />Genauigkeit ist größer als 38<br /><br />Skalierung ist kleiner als 0 (null)<br /><br />Skalierung ist größer als 38<br /><br />Skalierung ist größer als Genauigkeit|  
||DT_CY|Der decimal-Datentyp wird DT_CY zugeordnet, wenn er als money-Datentyp deklariert wird.|  
|SQL_DATE<br /><br />SQL_TYPE_DATE|DT_DBDATE|  
|SQL_TIME<br /><br />SQL_TYPE_TIME|DT_DBTIME|  
|SQL_TIMESTAMP<br /><br />SQL_TYPE_TIMESTAMP|DT_DBTIMESTAMP<br /><br />DT_DBTIMESTAMP2|SQL_TIMESTAMP-Datentypen werden DT_DBTIMESTAMP2 zugeordnet, wenn die Skalierung größer als 3 ist. In allen anderen Fällen werden sie DT_DBTIMESTAMP zugeordnet.|  
|SQL_CHAR<br /><br />SQLVARCHAR|DT_STR<br /><br />DT_WSTR<br /><br />DT_TEXT<br /><br />DT_NTEXT|DT_STR wird verwendet, wenn die Spaltenlänge kleiner oder gleich 8000 ist und die **ExposeStringsAsUnicode** -Eigenschaft den Wert „false“ aufweist.<br /><br />DT_WSTR wird verwendet, wenn die Spaltenlänge kleiner oder gleich 8000 ist und die **ExposeStringsAsUnicode** -Eigenschaft den Wert „true“ aufweist.<br /><br />DT_TEXT wird verwendet, wenn die Spaltenlänge größer als 8000 ist und die **ExposeStringsAsUnicode** -Eigenschaft den Wert „false“ aufweist.<br /><br />DT_NTEXT wird verwendet, wenn die Spaltenlänge größer als 8000 ist und die **ExposeStringsAsUnicode** -Eigenschaft den Wert „true“ aufweist.|  
|SQL_LONGVARCHAR|DT_TEXT<br /><br />DT_NTEXT|DT_NTEXT wird verwendet, wenn die **ExposeStringsAsUnicode** -Eigenschaft den Wert „true“ aufweist.|  
|SQL_WCHAR<br /><br />SQL_WVARCHAR|DT_WSTR<br /><br />DT_NTEXT|DT_WSTR wird verwendet, wenn die Spaltenlänge kleiner oder gleich 4000 ist.<br /><br />DT_NTEXT wird verwendet, wenn die Spaltenlänge größer als 4000 ist.|  
|SQL_WLONGVARCHAR|DT_NTEXT|  
|SQL_BINARY|DT_BYTE<br /><br />DT_IMAGE|DT_BYTES wird verwendet, wenn die Spaltenlänge kleiner oder gleich 8000 ist.<br /><br />DT_IMAGE wird verwendet, wenn die Spaltenlänge größer als 8000 ist.|  
|SQL_LONGVARBINARY|DT_IMAGE|  
|SQL_GUID|DT_GUID|  
|SQL_INTERVAL_YEAR<br /><br />SQL_INTERVAL_MONTH<br /><br />SQL_INTERVAL_DAY<br /><br />SQL_INTERVAL_HOUR<br /><br />SQL_INTERVAL_MINUTE<br /><br />SQL_INTERVAL_SECOND<br /><br />SQL_INTERVAL_YEAR_TO_MONTH<br /><br />SQL_INTERVAL_DAY_TO_HOUR<br /><br />SQL_INTERVAL_DAY_TO_MINUTE<br /><br />SQL_INTERVAL_DAY_TO_SECOND<br /><br />SQL_INTERVAL_HOUR_TO_MINUTE<br /><br />SQL_INTERVAL_HOUR_TO_SECOND<br /><br />SQL_INTERVAL_MINUTE_TO_SECOND|DT_WSTR|  
|Anbieterspezifische Datentypen|DT_BYTES<br /><br />DT_IMAGE|DT_BYTES wird verwendet, wenn die Spaltenlänge kleiner oder gleich 8000 ist.<br /><br />DT_IMAGE wird verwendet, wenn die Spaltenlänge 0 (null) oder größer als 8000 ist.|  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [ODBC-Quelle](../../integration-services/data-flow/odbc-source.md)  
  
-   [ODBC-Ziel](../../integration-services/data-flow/odbc-destination.md)  
  
 


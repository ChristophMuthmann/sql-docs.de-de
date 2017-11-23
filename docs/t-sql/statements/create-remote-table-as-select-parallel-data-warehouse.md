---
title: Erstellen Sie REMOTE Tabelle AS SELECT (Parallel Datawarehouse) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
ms.prod: 
ms.prod_service: pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 16ef8191-7587-45a3-9ee9-7d99b7088de3
caps.latest.revision: "9"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5b1c445662f29241d8a2a1a547ef498f7491590b
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="create-remote-table-as-select-parallel-data-warehouse"></a>Erstellen Sie REMOTE Tabelle AS SELECT (Parallel Datawarehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Wählt Daten aus einer [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] Datenbank und kopiert die Daten in eine neue Tabelle in einem SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbank auf einem Remoteserver. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]verwendet das Gerät mit, alle Vorteile der MPP abfrageverarbeitung, um die Daten für die Remotekopie auszuwählen. Verwenden Sie dies für Szenarien, die erfordern [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Funktionalität.  
  
 Um den Remoteserver zu konfigurieren, finden Sie unter "Remote Tabelle kopieren" in der [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 ![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Thema Linksymbol") [Transact-SQL-Syntaxkonventionen &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CREATE REMOTE TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name     AT ('<connection_string>')  
    [ WITH ( BATCH_SIZE = batch_size ) ]  
    AS <select_statement>  
[;]  
  
<connection_string> ::=   
    Data Source = { IP_address | hostname } [, port ]; User ID = user_name ;Password = password;  
  
<select_statement> ::=  
    [ WITH <common_table_expression> [ ,...n ] ]  
    SELECT <select_criteria>  
```  
  
## <a name="arguments"></a>Argumente  
 *database_name*  
 Die Datenbank, die Remotetabelle in zu erstellen. *Database_name* ist eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbank. Standardmäßig ist die Standarddatenbank für die Anmeldung des Benutzers auf dem Ziel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz.  
  
 *schema_name*  
 Das Schema für die neue Tabelle. Standardmäßig ist das Standardschema für die Anmeldung des Benutzers auf dem Ziel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz.  
  
 *table_name*  
 Der Name der neuen Tabelle. Details zu Tabellennamen zulässig "Benennungsregeln für Objekt" finden Sie unter der [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 Die Remotetabelle wird als Heap erstellt. Check-Einschränkungen oder Trigger keine. Die Sortierung der Remotetabellenspalten wird die Sortierung der Spalten der Quelltabelle identisch. Dies gilt für Spalten vom Typ **Char**, **Nchar**, **Varchar**, und **Nvarchar**.  
  
 *Verbindungszeichenfolge*  
 Eine Zeichenfolge, die angibt, die `Data Source`, `User ID`, und `Password` Parameter für das Herstellen einer Verbindung mit remote-Servers und der Datenbank.  
  
 Die Verbindungszeichenfolge ist eine durch Semikolons getrennte Liste von Schlüssel-Wert-Paaren. Schlüsselwörter wird die Groß-und Kleinschreibung nicht berücksichtigt. Leerzeichen zwischen den Schlüssel-Wert-Paaren werden ignoriert. Allerdings können Werte Groß-/Kleinschreibung beachtet, je nach Datenquelle sein.  
  
 *Datenquelle*  
 Der Parameter, der angibt, der Name oder IP-Adresse und TCP-Portnummer für die remote SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *Hostname* oder *IP-Adresse*  
 Name des Computers Remoteserver oder die IPv4-Adresse des Remoteservers. IPv6-Adressen werden nicht unterstützt. Sie können angeben, ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] benannte Instanz im Format **"Computername\Instanzename"** oder **IP_address\Instance_Name**. Der Server muss remote und kann daher nicht als (local) angegeben werden.  
  
 TCP *Port* Anzahl  
 Die TCP-Portnummer für die Verbindung. Sie können eine TCP-Portnummer zwischen 0 und 65535 für eine Instanz von SQL Server angeben, die nicht auf dem Standardport 1433 lauscht. Zum Beispiel: **ServerA 1450** oder **10.192.14.27,1435**  
  
> [!NOTE]  
>  Es wird empfohlen, über die IP-Adresse eine Verbindung mit einem Remoteserver. Abhängig von Ihrer Netzwerkkonfiguration möglicherweise Herstellen einer Verbindung mit dem Computernamen erfordern weitere Schritte zum einen nicht-Appliance DNS-Server zu verwenden, um mit dem richtigen Server den Namen aufzulösen. Dieser Schritt ist nicht erforderlich, bei der Verbindung mit einer IP-Adresse. Weitere Informationen finden Sie unter "Verwenden eine DNS-Weiterleitung Resolve-nicht-Appliance DNS-Namen (Analytics Platform System)" in der [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 *Benutzername*  
 Ein gültiger [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldename für die Authentifizierung. Maximale Anzahl von Zeichen ist 128.  
  
 *Kennwort*  
 Das Anmeldekennwort. Maximale Anzahl von Zeichen ist 128.  
  
 *batch_size*  
 Die maximale Anzahl von Zeilen pro Batch. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]sendet Zeilen in Batches auf den Zielserver an. *Batch_size* ist eine positive ganze Zahl > = 0. Standard ist 0.  
  
 MIT *Common_table_expression*  
 Gibt ein temporäres benanntes Resultset an, das als allgemeiner Tabellenausdruck (CTE, Common Table Expression) bekannt ist. Weitere Informationen finden Sie unter [WITH Common_table_expression &#40; Transact-SQL &#41; ](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 Wählen Sie \<Select_criteria > Abfrageprädikat, der angibt, welche Daten die neue Remotetabelle ausgefüllt werden. Informationen für die SELECT-Anweisung finden Sie unter [SELECT &#40; Transact-SQL &#41; ](../../t-sql/queries/select-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Benötigen Sie Folgendes:  
  
-   SELECT-Berechtigung für jedes Objekt in der SELECT-Klausel.  
  
-   Erfordert die CREATE TABLE-Berechtigung in der SMP-Zieldatenbank.  
  
-   Erfordert ALTER, INSERT und SELECT-Berechtigungen auf dem SMP Zielschema an.  
  
## <a name="error-handling"></a>Fehlerbehandlung  
 Wenn das Kopieren von Daten für die Remotedatenbank fehlschlägt, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] wird den Vorgang abbrechen, schreibt einen Fehler und versuchen, die Remotetabelle zu löschen. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]eine erfolgreiche Bereinigung der neuen Tabelle ist nicht sichergestellt werden.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 **Remote-Zielserver**:  
  
-   TCP ist die Standardeinstellung und unterstützt nur Protokoll zum Herstellen einer Verbindung mit einem Remoteserver.  
  
-   Der Zielserver muss ein nicht-Appliance-Server sein. CREATE REMOTE TABLE kann nicht verwendet werden, zum Kopieren von Daten aus einer Anwendung in eine andere.  
  
-   Die CREATE REMOTE TABLE-Anweisung werden nur neue Tabellen erstellt. Aus diesem Grund kann nicht die neue Tabelle bereits vorhanden sein. Die remote-Datenbank und das Schema müssen bereits vorhanden sein.  
  
-   Der Remoteserver benötigen Speicherplatz zum Speichern der Daten, die auf dem Gerät zu übertragen werden die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Remotedatenbank.  
  
 **SELECT-Anweisung**:  
  
-   Die ORDER BY und TOP-Klauseln werden in die Kriterien von select nicht unterstützt.  
  
-   CREATE REMOTE TABLE kann nicht ausgeführt werden, innerhalb einer aktiven Transaktion oder wenn der AUTOCOMMIT-aus-Einstellung für die Sitzung aktiv ist.  
  
 [SET ROWCOUNT &#40; Transact-SQL &#41; ](../../t-sql/statements/set-rowcount-transact-sql.md) hat keine Auswirkung auf diese Anweisung. Um ein ähnliches Verhalten zu erzielen, verwenden [nach oben &#40; Transact-SQL &#41; ](../../t-sql/queries/top-transact-sql.md).  
  
## <a name="locking-behavior"></a>Sperrverhalten  
 Nach dem Erstellen der Remotetabelle, ist die Zieltabelle nicht gesperrt, bis der Kopiervorgang gestartet wird. Aus diesem Grund ist es möglich, dass ein anderer Prozess auf die Remotetabelle löschen, nachdem er erstellt wurde und bevor der Kopiervorgang gestartet wird. In diesem Fall [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] generiert einen Fehler, und der Kopiervorgang fehl.  
  
## <a name="metadata"></a>Metadaten  
 Verwendung [sys.dm_pdw_dms_workers &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md) den Status des Kopiervorgangs der ausgewählten Daten auf den SMP-Remoteserver anzeigen. Zeilen mit dem Typ PARALLEL_COPY_READER werden diese Informationen enthalten.  
  
## <a name="security"></a>Sicherheit  
 CREATE REMOTE TABLE verwendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung für die Verbindung zur Remoteinstanz [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz; es werden keine Windows-Authentifizierung verwendet.  
  
 Die [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] externes zugänglichen Netzwerk muss Firewall sein, und mit Ausnahme von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , administrative Ports und Managementports.  
  
 Um versehentliche Datenverluste oder Beschädigungen zu vermeiden, sollte das Benutzerkonto, das verwendet wird, auf dem Gerät in die Zieldatenbank kopiert nur die minimalen erforderlichen Berechtigungen in der Zieldatenbank verfügen.  
  
 Verbindungseinstellungen können Sie sich auf dem SMP verbinden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz mit SSL schützen von Daten für Benutzer und Kennwort, jedoch mit tatsächlichen Daten, die unverschlüsselt in Klartext gesendet werden. In diesem Fall könnte ein böswilliger Benutzer den Text der CREATE REMOTE TABLE-Anweisung, der enthält Abfangen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Benutzernamen und das Kennwort für die Anmeldung bei der SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz. Um dieses Risiko zu vermeiden, verwenden Sie die Verschlüsselung von Daten für die Verbindung mit dem SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz.  
  
##  <a name="Examples"></a> Beispiele  
  
### <a name="a-creating-a-remote-table"></a>A. Erstellen einer Remotetabelle  
 In diesem Beispiel wird eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SMP Remotetabelle aufgerufen `MyOrdersTable` Datenbank `OrderReporting` und Schema `Orders`. Die `OrderReporting` Datenbank ist auf einem Server mit dem Namen `SQLA` , die den Standardport 1433 lauscht. Die Verbindung mit dem Server verwendet die Anmeldeinformationen des Benutzers `David`, dessen Kennwort `e4n8@3`.  
  
```  
CREATE REMOTE TABLE OrderReporting.Orders.MyOrdersTable  
AT ( 'Data Source = SQLA, 1433; User ID = David; Password = e4n8@3;' )  
AS SELECT <select_criteria>;  
```  
  
### <a name="b-querying-the-sysdmpdwdmsworkers-dmv-for-remote-table-copy-status"></a>B. Abfragen der DMV sys.dm_pdw_dms_workers für Kopierstatus Remotetabelle  
 Diese Abfrage zeigt, wie Kopierstatus für eine Remotetabelle Kopie anzeigen.  
  
```  
SELECT * FROM sys.dm_pdw_dms_workers   
WHERE type = 'PARALLEL_COPY_READER';  
```  
  
### <a name="c-using-a-query-join-hint-with-create-remote-table"></a>C. Verwenden einen Join-Abfragehinweis mit CREATE REMOTE TABLE  
 Diese Abfrage zeigt die grundlegende Syntax für die Verwendung eines Join-Abfragehinweis mit CREATE REMOTE TABLE. Nachdem die Abfrage, mit dem Steuerungsknoten übermittelt wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], auf den Serverknoten ausführen, wird der Hash Join-Strategie angewendet, während der Generierung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Abfrageplan. Weitere Informationen zu joinhinweise und wie Sie die OPTION-Klausel verwenden, finden Sie unter [OPTION-Klausel &#40; Transact-SQL &#41; ](../../t-sql/queries/option-clause-transact-sql.md).  
  
```  
USE ssawPDW;  
CREATE REMOTE TABLE OrderReporting.Orders.MyOrdersTable  
AT ( 'Data Source = SQLA, 1433; User ID = David; Password = e4n8@3;' )  
    AS SELECT T1.* FROM OrderReporting.Orders.MyOrdersTable T1   
    JOIN OrderReporting.Order.Customer T2  
    ON T1.CustomerID=T2.CustomerID OPTION (HASH JOIN);  
```  
  
  


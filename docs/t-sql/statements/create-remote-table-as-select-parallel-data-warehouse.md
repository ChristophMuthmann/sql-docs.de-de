---
title: CREATE REMOTE TABLE AS SELECT (Parallel Data Warehouse) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/10/2017
ms.prod: ''
ms.prod_service: pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 16ef8191-7587-45a3-9ee9-7d99b7088de3
caps.latest.revision: 9
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a11ac54520c834ec31d61e820bbc7fc28f63d6c7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-remote-table-as-select-parallel-data-warehouse"></a>REMOTE TABLE AS SELECT (Parallel Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Wählt Daten aus einer [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]-Datenbank und kopiert die Daten in eine neue Tabelle in einer SMP-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank auf einem Remoteserver. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] verwendet die Appliance mit allen Vorteilen der MPP-Abfrageverarbeitung, um die Daten für die Remotekopie auszuwählen. Verwenden Sie diese Option für Szenarios, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Funktionalität erfordern.  
  
 Informationen zum Konfigurieren des Remoteservers finden Sie unter „Remotetabellenkopie“ in der [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 ![Symbol zum Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions &#40;Transact-SQL&#41; (Transact-SQL-Syntaxkonventionen (Transact-SQL))](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 Die Datenbank zum Erstellen der Remotetabelle. *database_name* ist eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank. Der Standard ist die Standarddatenbank für die Anmeldung des Benutzers an der Ziel-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz.  
  
 *schema_name*  
 Das Schema der neuen Tabelle. Der Standard ist das Standardschema für die Anmeldung des Benutzers an der Ziel-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz.  
  
 *table_name*  
 Der Name der neuen Tabelle. Weitere Informationen zu zulässigen Tabellennamen finden Sie unter "Objektbenennungsregeln" in der [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 Die Remotetabelle wird als Heap erstellt. Sie hat keine Überprüfungseinschränkungen oder -trigger. Die Sortierung der Remotetabellenspalten und die Sortierung der Spalten der Quelltabelle sind identisch. Dies gilt für Spalten vom Typ **char**, **nchar**, **varchar** und **nvarchar**.  
  
 *connection_string*  
 Eine Zeichenfolge, die die Parameter `Data Source`, `User ID` und `Password` für das Herstellen einer Verbindung mit dem Remoteserver und der Datenbank angibt.  
  
 Die Verbindungszeichenfolge ist eine durch Semikolon getrennte Liste von Schlüssel-Wert-Paaren. Bei Schlüsselwörtern muss die Groß-/Kleinschreibung nicht beachtet werden. Leerzeichen zwischen den Schlüssel-Wert-Paaren werden ignoriert. Allerdings muss bei Werten je nach Datenquelle möglicherweise die Groß-/Kleinschreibung beachtet werden.  
  
 *Datenquelle*  
 Der Parameter, der den Namen oder die IP-Adresse und die TCP-Portnummer für den Remote-SMP-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] angibt.  
  
 *hostname* oder *IP_address*  
 Name des Remoteservercomputers oder IPv4-Adresse des Remoteservers. IPv6-Adressen werden nicht unterstützt. Sie können eine benannte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz im Format **Computer_Name\Instance_Name** oder **IP_address\Instance_Name** angeben. Der Server muss remote sein und kann daher nicht als (local) angegeben werden.  
  
 TCP *port* number  
 Die für die Verbindung verwendete TCP-Portnummer. Sie können eine TCP-Portnummer zwischen 0 und 65535 für eine Instanz von SQL Server angeben, die nicht am Standardport 1433 lauscht. Beispiele: **ServerA,1450** oder **10.192.14.27,1435**  
  
> [!NOTE]  
>  Es wird empfohlen, über die IP-Adresse eine Verbindung mit einem Remoteserver herzustellen. Abhängig von Ihrer Netzwerkkonfiguration erfordert die Herstellung einer Verbindung mit dem Computernamen möglicherweise weitere Schritte, damit Sie mit Ihrem DNS-Server, der nicht zur Appliance gehört, den Namen zum korrekten Server auflösen können. Dieser Schritt ist nicht erforderlich, wenn Sie die Verbindung mit einer IP-Adresse herstellen. Weitere Informationen finden Sie unter "Verwenden einer DNS-Weiterleitung zum Auflösen von DNS-Namen, die nicht zu Appliances gehören (Analytics Platform System)" in der [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 *user_name*  
 Eine gültige [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmelde-ID für die Authentifizierung. Es können maximal 128 Zeichen eingegeben werden.  
  
 *password*  
 Das Anmeldekennwort. Es können maximal 128 Zeichen eingegeben werden.  
  
 *batch_size*  
 Die maximale Anzahl der Zeilen pro Batch. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] sendet Zeilen in Batches an den Zielserver. *Batch_size* ist eine positive ganze Zahl >=0. Standard ist "0".  
  
 WITH *common_table_expression*  
 Gibt ein temporäres benanntes Resultset an, das als allgemeiner Tabellenausdruck (CTE, Common Table Expression) bekannt ist. Weitere Informationen finden Sie unter [WITH common_table_expression &#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 SELECT \<select_criteria > Abfrageprädikat, das angibt, welche Daten die neue Remotetabelle auffüllen. Informationen zur SELECT-Anweisung finden Sie unter [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert:  
  
-   SELECT-Berechtigung für jedes Objekt in der SELECT-Klausel.  
  
-   Erfordert die CREATE TABLE-Berechtigung für die SMP-Zieldatenbank.  
  
-   Erfordert die Berechtigungen ALTER, INSERT und SELECT auf dem SMP-Zielschema.  
  
## <a name="error-handling"></a>Fehlerbehandlung  
 Wenn das Kopieren von Daten für die Remotedatenbank fehlschlägt, bricht der [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] den Vorgang ab, protokolliert einen Fehler und versucht, die Remotetabelle zu löschen. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] gewährleistet nicht die erfolgreiche Bereinigung der neuen Tabelle.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 **Remotezielserver**:  
  
-   TCP ist die Standardeinstellung und das einzige unterstützte Protokoll zum Herstellen einer Verbindung mit einem Remoteserver.  
  
-   Der Zielserver muss Server sein, der nicht zur Appliance gehört. CREATE REMOTE TABLE kann nicht verwendet werden, um Daten aus einer Anwendung in eine andere zu kopieren.  
  
-   Die CREATE REMOTE TABLE-Anweisung erstellt nur neue Tabellen. Aus diesem Grund ist es nicht möglich, dass die neue Tabelle bereits vorhanden ist. Remotedatenbank und Remoteschema müssen bereits vorhanden sein.  
  
-   Der Remoteserver benötigt verfügbaren Speicherplatz zum Speichern der Daten, die von der Appliance zur [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Remotedatenbank übertragen werden.  
  
 **SELECT-Anweisung**:  
  
-   Die ORDER BY- und die TOP-Klausel werden nicht in den Auswahlkriterien unterstützt.  
  
-   CREATE REMOTE TABLE kann nicht innerhalb einer aktiven Transaktion, oder wenn die AUTOCOMMIT OFF-Einstellung für die Sitzung aktiv ist, ausgeführt werden.  
  
 [SET ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/statements/set-rowcount-transact-sql.md) hat keine Auswirkung auf diese Anweisung. Verwenden Sie [TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md), um ein ähnliches Verhalten zu erzielen.  
  
## <a name="locking-behavior"></a>Sperrverhalten  
 Nach dem Erstellen der Remotetabelle ist die Zieltabelle so lange nicht gesperrt, bis der Kopiervorgang gestartet wird. Aus diesem Grund ist es möglich, dass ein anderer Prozess die Remotetabelle löscht, nachdem sie erstellt wurde und bevor der Kopiervorgang gestartet wird. In diesem Fall generiert [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] einen Fehler, und der Kopiervorgang schlägt fehl.  
  
## <a name="metadata"></a>Metadaten  
 Verwenden Sie [sys.dm_pdw_dms_workers &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md), um den Status des Kopiervorgangs der ausgewählten Daten auf den SMP-Remoteserver anzuzeigen. Zeilen mit dem Typ PARALLEL_COPY_READER enthalten diese Informationen.  
  
## <a name="security"></a>Security  
 CREATE REMOTE TABLE verwendet die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung, um eine Verbindung zur Remote-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz herzustellen. Die Windows-Authentifizierung wird nicht verwendet.  
  
 Das extern ausgerichtete Netzwerk [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] muss durch eine Firewall geschützt sein. Ausnahmen sind [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Ports, administrative Ports und Managementports.  
  
 Um versehentliche Datenverluste oder Beschädigungen zu vermeiden, sollte das Benutzerkonto, das verwendet wird, um aus der Appliance in die Zieldatenbank zu kopieren, nur über die erforderlichen Mindestberechtigungen in der Zieldatenbank verfügen.  
  
 Verbindungseinstellungen ermöglichen Ihnen, eine Verbindung mit der SMP-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz herzustellen, wobei SSL den Benutzernamen und Kennwortdaten schützt, die eigentlichen Daten jedoch unverschlüsselt als Klartext gesendet werden. In diesem Fall könnte ein böswilliger Benutzer den Text der CREATE REMOTE TABLE-Anweisung abfangen, der den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Benutzernamen und das Kennwort für die Anmeldung bei der SMP-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz enthält. Um dieses Risiko zu vermeiden, verwenden Sie die Verschlüsselung von Daten für die Verbindung mit der SMP-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz.  
  
##  <a name="Examples"></a> Beispiele  
  
### <a name="a-creating-a-remote-table"></a>A. Erstellen einer Remotetabelle  
 In diesem Beispiel wird eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-SMP-Remotetabelle, die `MyOrdersTable` heißt, in der Datenbank `OrderReporting` und dem Schema `Orders` erstellt. Die `OrderReporting`-Datenbank befindet sich auf einem Server mit dem Namen `SQLA`, der am Standardport 1433 lauscht. Die Verbindung mit dem Server verwendet die Anmeldeinformationen des Benutzers `David`, dessen Kennwort `e4n8@3` lautet.  
  
```  
CREATE REMOTE TABLE OrderReporting.Orders.MyOrdersTable  
AT ( 'Data Source = SQLA, 1433; User ID = David; Password = e4n8@3;' )  
AS SELECT <select_criteria>;  
```  
  
### <a name="b-querying-the-sysdmpdwdmsworkers-dmv-for-remote-table-copy-status"></a>B. Abfragen der sys.dm_pdw_dms_workers-DMV nach dem Kopierstatus der Remotetabelle  
 Diese Abfrage zeigt, wie der Kopierstatus für eine Remotetabellenkopie angezeigt wird.  
  
```  
SELECT * FROM sys.dm_pdw_dms_workers   
WHERE type = 'PARALLEL_COPY_READER';  
```  
  
### <a name="c-using-a-query-join-hint-with-create-remote-table"></a>C. Verwenden eines Join-Abfragehinweises mit CREATE REMOTE TABLE  
 Diese Abfrage zeigt die grundlegende Syntax für die Verwendung eines Join-Abfragehinweises mit CREATE REMOTE TABLE. Nachdem die Abfrage an den Steuerungsknoten übermittelt wurde, wendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (wird auf den Computeknoten ausgeführt) die Hashjoinstrategie an, wenn der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abfrageplan generiert wird. Weitere Informationen zu Joinhinweisen und der Verwendung der OPTION-Klausel finden Sie unter [OPTION-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/option-clause-transact-sql.md).  
  
```  
USE ssawPDW;  
CREATE REMOTE TABLE OrderReporting.Orders.MyOrdersTable  
AT ( 'Data Source = SQLA, 1433; User ID = David; Password = e4n8@3;' )  
    AS SELECT T1.* FROM OrderReporting.Orders.MyOrdersTable T1   
    JOIN OrderReporting.Order.Customer T2  
    ON T1.CustomerID=T2.CustomerID OPTION (HASH JOIN);  
```  
  
  


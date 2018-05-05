---
title: bcp-Hilfsprogramm | Microsoft-Dokumentation
ms.custom: ''
ms.date: 02/12/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.component: bcp
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- bcp utility [SQL Server]
- exporting data
- row exporting [SQL Server]
- copying data [SQL Server], bcp utility
- command prompt utilities [SQL Server], bcp
- tables [SQL Server], importing data
- column importing [SQL Server]
- bcp utility [SQL Server], command options
- file exporting [SQL Server]
- bulk copy [SQL Server]
- bcp utility [SQL Server], about bcp utility
- tables [SQL Server], exporting data
- row importing [SQL Server]
- importing data, bcp utility
- file importing [SQL Server]
- column exporting [SQL Server]
ms.assetid: c0af54f5-ca4a-4995-a3a4-0ce39c30ec38
caps.latest.revision: 222
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f54b14989ac5df37bbb8ee386c783c9721a32206
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="bcp-utility"></a>Hilfsprogramms bcp
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

 > Weitere Informationen, die sich auf vorherige Versionen von SQL Server beziehen, finden Sie unter [bcp-Hilfsprogramm](https://msdn.microsoft.com/en-US/library/ms162802(SQL.120).aspx).

 > Die neueste Version des Hilfsprogramms Bcp, finden Sie unter [Microsoft über die Befehlszeile Hilfsprogramme 14.0 für SQL Server ](http://go.microsoft.com/fwlink/?LinkID=825643)

 > Verwenden von Bcp unter Linux, finden Sie unter [Sqlcmd und Bcp unter Linux installieren](../linux/sql-server-linux-setup-tools.md).

 > Ausführliche Informationen zur Verwendung von Bcp mit Azure SQL Data Warehouse finden Sie unter [Laden von Daten mithilfe von Bcp](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp).

  Mit dem Hilfsprogramm **bcp**( **B**ulk **C**opy**P**rogram) werden Daten per Massenvorgang zwischen einer Instanz von [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] und einer Datendatei in einem benutzerdefinierten Format kopiert. Das Hilfsprogramm **bcp** kann verwendet werden, um große Mengen neuer Zeilen in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Tabellen zu importieren oder um Daten aus Tabellen in Datendateien zu exportieren. Außer in Verbindung mit der Option **queryout** sind für das Hilfsprogramm keine Kenntnisse von [!INCLUDE[tsql](../includes/tsql-md.md)]erforderlich. Um Daten in eine Tabelle zu importieren, müssen Sie entweder eine für diese Tabelle erstellte Formatdatei verwenden oder die Struktur der Tabelle und die Art der Daten kennen, die in den Tabellenspalten zulässig sind.  
  
 ![Artikellinksymbol](../database-engine/configure-windows/media/topic-link.gif "Topic link icon") Informationen zu den **bcp**-Syntaxkonventionen finden Sie unter [Transact-SQL-Syntaxkonventionen &#40;Transact-SQL&#41;](../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
> [!NOTE]
> Wenn Sie Ihre Daten mit **bcp** sichern, müssen Sie zum Aufzeichnen des Datenformats eine Formatdatei erstellen. **bcp** -Datendateien enthalten **keine** Schema- oder Formatinformationen. Daher können Sie die Daten möglicherweise nicht mehr importieren, wenn Sie eine Tabelle löschen und keine Formatdatei vorhanden ist.  
  
<table><th>Syntax</th><tr><td><pre>
bcp [<a href="#db_name">database_name.</a>] <a href="#schema">schema</a>.{<a href="#tbl_name">table_name</a> | <a href="#vw_name">view_name</a> | <a href="#query">"query"</a>
    {<a href="#in">in</a> <a href="#data_file">data_file</a> | <a href="#out">out</a> <a href="#data_file">data_file</a> | <a href="#qry_out">queryout</a> <a href="#data_file">data_file</a> | <a href="#format">format</a> <a href="#format">nul</a>}
<a>                                                                                                         </a>
    [<a href="#a">-a packet_size</a>]
    [<a href="#b">-b batch_size</a>]
    [<a href="#c">-c</a>]
    [<a href="#C">-C { ACP | OEM | RAW | code_page } </a>]
    [<a href="#d">-d database_name</a>]
    [<a href="#e">-e err_file</a>]
    [<a href="#E">-E</a>]
    [<a href="#f">-f format_file</a>]
    [<a href="#F">-F first_row</a>]
    [<a href="#G">-G Azure Active Directory Authentication</a>]
    [<a href="#h">-h"hint [,...n]"</a>]
    [<a href="#i">-i input_file</a>]
    [<a href="#k">-k</a>]
    [<a href="#K">-K application_intent</a>]
    [<a href="#L">-L last_row</a>]
    [<a href="#m">-m max_errors</a>]
    [<a href="#n">-n</a>]
    [<a href="#N">-N</a>]
    [<a href="#o">-o output_file</a>]
    [<a href="#P">-P password</a>]
    [<a href="#q">-q</a>]
    [<a href="#r">-r row_term</a>]
    [<a href="#R">-R</a>]
    [<a href="#S">-S [server_name[\instance_name]</a>]
    [<a href="#t">-t field_term</a>]
    [<a href="#T">-T</a>]
    [<a href="#U">-U login_id</a>]
    [<a href="#v">-v</a>]
    [<a href="#V">-V (80 | 90 | 100 | 110 | 120 | 130 ) </a>]
    [<a href="#w">-w</a>]
    [<a href="#x">-x</a>]
</pre></td></tr></table>  
  
## <a name="arguments"></a>Argumente  
 ***data_file***<a name="data_file"></a>  
 Der vollständige Pfad der Datendatei. Wenn Daten in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]massenimportiert werden, enthält die Datendatei die Daten, die in die angegebene Tabelle oder Sicht kopiert werden sollen. Beim Massenexportieren aus [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]enthält die Datendatei die Daten, die aus der Tabelle oder Sicht kopiert wurden. Der Pfad kann 1 bis 255 Zeichen enthalten. Die Datendatei kann maximal 2^63-1 Zeilen enthalten.  
  
 ***database_name***<a name="db_name"></a>  
 Der Name der Datenbank, in der die angegebene Tabelle oder Sicht vorhanden ist. Wenn kein Name angegeben ist, wird diese Datenbank als Standarddatenbank des Benutzers verwendet.  
  
 Sie können den Datenbanknamen mit **d-** auch explizit angeben.  
  
 **in** *data_file* | **out** *data_file* | **queryout** *data_file* | **format nul**  
 Gibt die Richtung des Massenkopierens wie folgt an:  
  
-   **in**<a name="in"></a> werden Daten aus einer Datei in die Datenbanktabelle oder -sicht kopiert.  
  
-   **out**<a name="out"></a> werden Daten aus der Datenbanktabelle oder -sicht in eine Datei kopiert. Wenn Sie eine vorhandene Datei angeben, wird die Datei überschrieben. Beachten Sie, dass das Hilfsprogramm **bcp** beim Extrahieren von Daten leere Zeichenfolgen als NULL-Zeichenfolgen und NULL-Zeichenfolgen als leere Zeichenfolgen darstellt.  
  
-   **queryout**<a name="qry_out"></a> werden Daten aus einer Abfrage kopiert. Diese Option muss nur beim Massenkopieren von Daten über eine Abfrage angegeben werden.  
  
-   **format**<a name="format"></a> wird eine Formatdatei basierend auf der angegebenen Option (**-n**, **-c**, **-w**oder **-N**) und den Tabellen- oder Sichttrennzeichen erstellt. Beim Massenkopieren von Daten kann der Befehl **bcp** auf eine Formatdatei verweisen. Dies erspart Ihnen die wiederholte interaktive Eingabe von Formatinformationen. Für die Option **format** ist die Option **-f** erforderlich. Zum Erstellen einer XML-Formatdatei muss zudem die Option **-x** angegeben werden. Weitere Informationen finden Sie unter [Erstellen einer Formatdatei &#40;SQL Server&#41;](../relational-databases/import-export/create-a-format-file-sql-server.md). Sie müssen **nul** als Wert angeben (**format nul**).  
  
 ***owner***<a name="schema"></a>  
 Dies ist der Namen des Besitzers der Tabelle oder Sicht. *owner* ist optional, wenn der Benutzer, der den Vorgang ausführt, der Besitzer der angegebenen Tabelle oder Sicht ist. Wenn *owner* nicht angegeben wird und der Benutzer, der den Vorgang ausführt, nicht Besitzer der angegebenen Tabelle oder Sicht ist, gibt [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] eine Fehlermeldung zurück, und der Vorgang wird abgebrochen.  
  
**"** ***query*** **"**<a name="query"></a> Eine [!INCLUDE[tsql](../includes/tsql-md.md)]-Abfrage, die ein Resultset zurückgibt. Wenn die Abfrage mehrere Resultsets zurückgibt, wird nur das erste Resultset in die Datendatei kopiert; nachfolgende Resultsets werden nicht berücksichtigt. Schließen Sie die Abfrage in doppelte Anführungszeichen und alle Elemente, die in die Abfrage eingebettet sind, in einfache Anführungszeichen ein. **queryout** muss auch angegeben werden, wenn Sie Daten aus einer Abfrage massenkopieren.  
  
 Die Abfrage kann auf eine gespeicherte Prozedur verweisen, sofern alle Tabellen, auf die innerhalb der gespeicherten Prozedur verwiesen werden, vor der Ausführung der bcp-Anweisung vorhanden sind. Wenn die gespeicherte Prozedur beispielsweise eine temporäre Tabelle generiert, tritt bei der **bcp** -Anweisung ein Fehler auf, da die temporäre Tabelle nur zur Laufzeit und nicht zum Zeitpunkt der Anweisungsausführung verfügbar ist. Ziehen Sie in diesem Fall in Erwägung, die Ergebnisse der gespeicherten Prozedur in eine Tabelle einzufügen und dann **bcp** zum Kopieren der Daten aus der Tabelle in eine Datendatei zu verwenden.  
  
 ***table_name***<a name="tbl_name"></a>  
 Der Name der Zieltabelle, wenn Daten in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] importiert werden (**in**), oder der Name der Quelltabelle, wenn Daten aus [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] exportiert werden (**out**).  
  
 ***view_name***<a name="vw_name"></a>   
 Der Name der Zielsicht, wenn Daten in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] kopiert werden (**in**), oder der Name der Quellsicht, wenn Daten aus [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] kopiert werden (**out**). Als Zielsichten können nur Sichten verwendet werden, in denen alle Spalten auf dieselbe Tabelle verweisen. Weitere Informationen zu den Einschränkungen beim Kopieren von Daten in Sichten finden Sie unter [INSERT &#40;Transact-SQL&#41;](../t-sql/statements/insert-transact-sql.md).  
  
 **-a** ***packet_size***<a name="a"></a>  
 Gibt an, wie viele Bytes pro Netzwerkpaket an den Server bzw. vom Server gesendet werden. Eine Serverkonfigurationsoption kann mithilfe von [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] (oder der gespeicherten Systemprozedur **sp_configure** ) festgelegt werden. Die Serverkonfigurationsoption kann jedoch mithilfe dieser Option einzeln überschrieben werden. *packet_size* kann einen Wert von 4096 bis 65535 Bytes annehmen. Der Standardwert ist 4096.  
  
 Durch einen höheren Wert für die Paketgröße kann die Leistung von Massenkopiervorgängen verbessert werden. Wenn eine größere Paketgröße angefordert, aber nicht erteilt wird, wird die Standardeinstellung verwendet. Die vom Hilfsprogramm **bcp** generierte Leistungsstatistik zeigt die verwendete Paketgröße an.  
  
 **-b** ***batch_size***<a name="b"></a>  
 Gibt die Anzahl von Zeilen pro importierten Datenbatch an. Jeder Batch wird als separate Transaktion importiert und protokolliert, für die erst dann ein Commit ausgeführt wird, nachdem der gesamte Batch importiert wurde. Standardmäßig werden alle Zeilen in der Datendatei als jeweils ein Batch importiert. Um die Zeilen auf mehrere Batches aufzuteilen, geben Sie mit *batch_size* eine Batchgröße an, die kleiner ist als die Anzahl von Zeilen in der Datendatei. Wenn die Transaktion für einen Batch einen Fehler erzeugt, wird nur für die Einfügungen aus dem aktuellen Batch ein Rollback ausgeführt. Auf Batches, die bereits durch Transaktionen importiert wurden, für die ein Commit ausgeführt wurde, wirken sich spätere Fehler nicht aus.  
  
 Verwenden Sie diese Option nicht in Verbindung mit der Option **-h "** ROWS_PER_BATCH **=***bb***"**.  
 
 **-c**<a name="c"></a>  
 Führt den Vorgang mithilfe eines Zeichendatentyps aus. Diese Option fordert für keines der Felder zu einer Eingabe auf. Es werden folgende Einstellungen verwendet: **char** als Speichertyp, keine Präfixe, **\t** (Tabstoppzeichen) als Feldtrennzeichen und **\r\n** (Zeilenumbruchzeichen) als Zeilenabschlusszeichen. **-c** ist nicht kompatibel mit **-w**.  
  
 Weitere Informationen finden Sie unter [Verwenden des Zeichenformats zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md).  
  
 **-C** { **ACP** | **OEM** | **RAW** | *Codepage* }<a name="C"></a>   
 Gibt die Codepage für die in der Datendatei enthaltenen Daten an. *Codepage* ist nur dann von Bedeutung, wenn die Daten **char**-, **varchar**- oder **text** -Spalten mit Zeichenwerten enthalten, die größer als 127 oder kleiner als 32 sind.  
  
> [!NOTE]
> Es wird empfohlen, für jede Spalte in einer Formatdatei einen Sortierungsnamen anzugeben, außer wenn die 65001-Option Priorität vor der Angabe von Sortierung/Codepage haben soll.
  
|Codepagewert|Description|  
|---------------------|-----------------|  
|ACP|[!INCLUDE[vcpransi](../includes/vcpransi-md.md)]/Microsoft Windows (ISO 1252).|  
|OEM|Standardcodepage, die vom Client verwendet wird. Die Standardcodepage, die verwendet wird, wenn **-C** nicht angegeben wird.|  
|RAW|Es erfolgt keine Konvertierung von einer Codepage zu einer anderen. Dies ist die schnellste Option, da keine Konvertierung vorgenommen wird.|  
|*Codepage*|Bestimmte Codepagenummer, z. B. 850.<br /><br /> In Versionen vor Version 13 ([!INCLUDE[ssSQL15](../includes/sssql15-md.md)]) wird die Codepage 65001 (UTF-8-Codierung) nicht unterstützt. Ab Version 13 kann die UTF-8-Codierung in frühere Versionen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]importiert werden.|  
  
 **-d** ***database_name***<a name="d"></a>   
 Gibt die Datenbank an, mit der eine Verbindung hergestellt werden soll. bcp.exe stellt standardmäßig eine Verbindung mit der Standarddatenbank des Benutzers her. Wenn **-d** *Datenbankname* und ein dreiteiliger Name (*Datenbankname.schema.table*, passed as the first parameter to bcp.exe) is specified, an error will occur because you cannot specify the database name twice.Wenn *Datenbankname* mit einem Bindestrich (-) oder einem Schrägstrich (/) beginnt, fügen Sie keinen Leerraum zwischen **-d** und dem Datenbanknamen hinzu.  
  
 **-e** ***Fehlerdatei***<a name="e"></a>  
 Gibt den vollständigen Pfad einer Fehlerdatei an, in der alle Zeilen gespeichert werden, die das **bcp** -Hilfsprogramm nicht von der Datei in die Datenbank übertragen kann. Die durch den **bcp** -Befehl generierten Fehlermeldungen werden an die Arbeitsstation des Benutzers gesendet. Wenn diese Option nicht verwendet wird, wird keine Fehlerdatei erstellt.  
  
 Wenn *Fehlerdatei* mit einem Bindestrich (-) oder einem Schrägstrich (/) beginnt, darf kein Leerzeichen zwischen **-e** und dem *Fehlerdatei* -Wert enthalten sein.  
  
 **-E**<a name="E"></a>   
 Gibt an, dass der oder die Identitätswerte in der importierten Datendatei für die Identitätsspalte verwendet werden sollen. Wenn **-E** nicht angegeben wird, werden die Identitätswerte für diese Spalte in der zu importierenden Datendatei ignoriert. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] weist automatisch eindeutige Werte zu, basierend auf den Ausgangswerten und den inkrementellen Werten, die beim Erstellen der Tabelle angegeben wurden.  
  
 Wenn die Datendatei keine Werte für die Identitätsspalte in der Tabelle oder Sicht enthält, geben Sie mithilfe einer Formatdatei an, dass die Identitätsspalte der Tabelle oder Sicht beim Importieren von Daten ausgelassen werden soll. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] weist der Spalte automatisch eindeutige Werte zu. Weitere Informationen finden Sie unter [DBCC CHECKIDENT &#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-checkident-transact-sql.md).  
  
 Für die Option **-E** sind besondere Berechtigungen erforderlich. Weitere Informationen finden Sie unter „[Hinweise](#remarks)“ weiter unten in diesem Thema.  
   
 **-f** ***Formatdatei***<a name="f"></a>  
 Gibt den vollständigen Pfad einer Formatdatei an. Die Bedeutung dieser Option hängt von der Umgebung ab, in der sie verwendet wird. Folgende Bedeutungen sind möglich:  
  
-   Wird **-f** mit der Option **format** verwendet, wird die angegebene *Formatdatei* für die angegebene Tabelle oder Sicht erstellt. Zum Erstellen einer XML-Formatdatei müssen Sie zudem die Option **-x** angeben. Weitere Informationen finden Sie unter [Erstellen einer Formatdatei &#40;SQL Server&#41;](../relational-databases/import-export/create-a-format-file-sql-server.md).  
  
-   Wird **-f** mit der Option **in** oder **out** verwendet, ist eine bereits vorhandene Formatdatei erforderlich.  
  
    > [!NOTE]
    > Die Verwendung einer Formatdatei mit der Option **in** oder **out** ist optional. Fehlt die Option **-f** und wurde **-n**, **-c**, **-w**oder **-N** nicht angegeben, werden Sie vom Befehl zur Angabe von Formatinformationen aufgefordert, und Sie erhalten die Möglichkeit, Ihre Antworten in einer Formatdatei (mit dem Standardnamen Bcp.fmt) zu speichern.
  
 Wenn *Fehlerdatei* mit einem Bindestrich (-) oder einem Schrägstrich (/) beginnt, darf kein Leerzeichen zwischen **-f** und dem *Fehlerdatei* -Wert enthalten sein.  
  
**-F** ***erste_Zeile***<a name="F"></a>  
 Gibt die Nummer der ersten Zeile an, die aus einer Tabelle exportiert oder von einer Datendatei importiert werden soll. Für diesen Parameter muss ein Wert größer als (>) 0, jedoch kleiner (<) oder gleich (=) der Gesamtanzahl der Zeilen angegeben werden. Fehlt dieser Parameter, wird standardmäßig die erste Zeile der Datei angenommen.  
  
 *erste_Zeile* kann eine positive ganze Zahl mit einem Wert bis zu 2^63-1 sein. **-F** *erste_Zeile* ist 1-basiert.  

**-G**<a name="G"></a>  
 Diese Option wird vom Client beim Herstellen einer Verbindung mit Azure SQL-Datenbank oder Azure SQL-Datenbank verwendet, um anzugeben, dass der Benutzer mithilfe der Azure Active Directory-Authentifizierung authentifiziert werden soll. Erfordert die Option-G [Version 14.0.3008.27 oder höher](http://go.microsoft.com/fwlink/?LinkID=825643). Führen Sie „bcp -v“ aus, um die von Ihnen verwendete Version zu ermitteln. Weitere Informationen finden Sie unter [verwenden Azure Active Directory-Authentifizierung für die Authentifizierung mit SQL-Datenbank oder SQL Data Warehouse](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication). 

> [!TIP]
>  Zum Überprüfen, ob Ihre Version des Bcp-Unterstützung für Azure Active Directory-Authentifizierung (AAD) Typ umfasst **Bcp--** (Bcp\<Speicherplatz >\<Dash >\<Dash >), und überprüfen Sie, ob - G in der Liste der Verfügbare Argumente.

- **Azure Active Directory-Benutzername und -Kennwort:** 

    Wenn Sie einen Azure Active Directory-Benutzernamen und das zugehörige Kennwort verwenden möchten, geben Sie die Option **-G** zusammen mit dem Benutzernamen und dem Kennwort an, indem Sie die Optionen **-U** und **-P** bereitstellen. 

    Im folgenden Beispiel werden Daten mithilfe von Azure AD-Benutzername und Kennwort, in denen Benutzer und das Kennwort ist eine AAD-Anmeldeinformationen. Im Beispiel wird die Tabelle exportiert `bcptest` aus Datenbank `testdb` von Azure-Server `aadserver.database.windows.net` und speichert die Daten in der Datei `c:\last\data1.dat`:
    ``` 
    bcp bcptest out "c:\last\data1.dat" -c -t -S aadserver.database.windows.net -d testdb -G -U alice@aadtest.onmicrosoft.com -P xxxxx
    ``` 

    Im folgende Beispiel wird importiert, Daten mithilfe von Azure AD-Benutzername und Kennwort, in denen Benutzer und das Kennwort ist eine AAD-Anmeldeinformationen. Im Beispiel wird importiert Daten aus der Datei `c:\last\data1.dat` in Tabelle `bcptest` für Datenbank `testdb` auf Azure-Server `aadserver.database.windows.net` mithilfe von Azure AD-Benutzername und Kennwort:
    ```
    bcp bcptest in "c:\last\data1.dat" -c -t -S aadserver.database.windows.net -d testdb -G -U alice@aadtest.onmicrosoft.com -P xxxxx
    ```



- **Integrierte Azure Active Directory-Authentifizierung** 
 
    Wenn Sie die integrierte Azure Active Directory-Authentifizierung verwenden möchten, geben Sie die Option **-G** ohne Benutzername und Kennwort an. Diese Konfiguration wird davon ausgegangen, dass das aktuelle Windows-Benutzerkonto (das Konto, unter die Bcp-Befehl ausgeführt wird) einen Verbund mit Azure AD ist: 

    Im folgenden Beispiel werden Daten mithilfe der integrierten Azure AD-Konto. Im Beispiel wird die Tabelle exportiert `bcptest` aus Datenbank `testdb` mithilfe von Azure AD Integrated aus Azure-Server `aadserver.database.windows.net` und speichert die Daten in der Datei `c:\last\data2.dat`:

    ```
    bcp bcptest out "c:\last\data2.dat" -S aadserver.database.windows.net -d testdb -G -c -t
    ```

    Im folgende Beispiel wird importiert, Daten mithilfe von Azure AD integrierten auth. Im Beispiel wird importiert Daten aus der Datei `c:\last\data2.txt` in Tabelle `bcptest` für Datenbank `testdb` auf Azure-Server `aadserver.database.windows.net` mithilfe von Azure AD-integrierte Authentifizierung:

    ```
    bcp bcptest in "c:\last\data2.dat" -S aadserver.database.windows.net -d testdb -G -c -t
    ```

  
**-h** ***"load hints***[ ,... *n*]**"**<a name="h"></a>: Gibt den oder die Hinweise an, die beim Massenimport von Daten in eine Tabelle oder Sicht verwendet werden sollen.  
  
* **ORDER**(***column*[ASC | DESC] [**,**...*n*]**)**  
Die Sortierreihenfolge der Daten in der Datendatei. Die Leistung des Massenkopierens wird verbessert, wenn die zu importierenden Daten entsprechend dem gruppierten Index der Tabelle (falls vorhanden) sortiert sind. Wenn die Datendatei in einer anderen Reihenfolge, d. h. nicht nach einem gruppierten Indexschlüssel sortiert ist, oder wenn es keinen gruppierten Index für die Tabelle gibt, wird die ORDER-Klausel ignoriert. Die angegebenen Spaltennamen müssen gültige Spaltennamen in der Zieltabelle sein. Standardmäßig geht **bcp** davon aus, dass die Datendatei nicht sortiert ist. Beim optimierten Massenimport wird in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] auch überprüft, ob die importierten Daten sortiert sind.  
  
* **ROWS_PER_BATCH** **=** ***bb***  
Die Anzahl von Datenzeilen pro Batch (als *bb*). Dieser Hinweis wird verwendet, wenn **-b** nicht angegeben wird. Er bewirkt, dass die gesamte Datendatei in einer einzigen Transaktion an den Server gesendet wird. Der Server optimiert das Massenladen entsprechend dem Wert von *bb*. Standardmäßig ist ROWS_PER_BATCH unbekannt.  
  
* **KILOBYTES_PER_BATCH** **=** ***cc***  
Die ungefähre Anzahl von Kilobytes (KB) an Daten pro Batch (als *cc*). In der Standardeinstellung ist KILOBYTES_PER_BATCH unbekannt.  
  
* **TABLOCK**  
Gibt an, dass eine Massenupdatesperre auf Tabellenebene für die Dauer des Massenladens aktiviert wird. Andernfalls wird eine Sperre auf Zeilenebene aktiviert. Dieser Hinweis verbessert die Leistung beträchtlich, da weniger Sperrkonflikte für die Tabelle auftreten, wenn diese während des Massenkopiervorgangs gesperrt wird. Eine Tabelle kann gleichzeitig von mehreren Clients geladen werden, wenn die Tabelle keine Indizes aufweist und **TABLOCK** angegeben ist. Standardmäßig wird das Sperrverhalten durch die Tabellenoption **table lock on bulk load**bestimmt.  
  
  > [!NOTE]
  > Wenn die Zieltabelle ein gruppierter Columnstore-Index ist, ist der TABLOCK-Hinweis zum Laden durch mehrere Clients parallel nicht erforderlich, da jedem parallel ausgeführten Thread eine eigene Zeilengruppe im Index zugewiesen wird, in die er Daten lädt. Details finden Sie in den Grundlagenthemen zum Columnstore-Index.
  
  **CHECK_CONSTRAINTS**  
  Gibt an, dass alle Einschränkungen, die für die Zieltabelle oder -sicht gelten, während des Massenimportvorgangs überprüft werden müssen. Ohne den CHECK_CONSTRAINTS-Hinweis werden alle CHECK- und FOREIGN KEY-Einschränkungen ignoriert. Nach dem Vorgang wird die Einschränkung für die Tabelle als nicht vertrauenswürdig markiert.  
  
  > [!NOTE]
  > UNIQUE-, PRIMARY KEY- und NOT NULL-Einschränkungen werden immer erzwungen.
  
  Zu einem bestimmten Zeitpunkt sollten Sie allerdings die Einschränkungen für die gesamte Tabelle überprüfen. Wenn die Tabelle vor dem Massenimportvorgang nicht leer war, überschreitet der Aufwand der erneuten Überprüfung möglicherweise denjenigen der Anwendung von CHECK-Einschränkungen auf die inkrementellen Daten. Daher empfiehlt es sich normalerweise, die Einschränkungsüberprüfung beim inkrementellen Massenimportieren zu aktivieren.  
  
  Die Deaktivierung von Einschränkungen (das Standardverhalten) kann z. B. erwünscht sein, wenn die Eingabedaten Zeilen enthalten, die Einschränkungen verletzen. Wenn CHECK-Einschränkungen deaktiviert sind, können Sie die Daten importieren und anschließend [!INCLUDE[tsql](../includes/tsql-md.md)] -Anweisungen verwenden, um ungültige Daten zu entfernen.  
  
  > [!NOTE]
  > **bcp** erzwingt nun Datenüberprüfungen, die dazu führen können, dass Skripts einen Fehler erzeugen, wenn sie für ungültige Daten in einer Datendatei ausgeführt werden.
  
  > [!NOTE]
  > Der Schalter **-m** *max_errors* gilt nicht für die Einschränkungsüberprüfung.
  
* **FIRE_TRIGGERS**  
Wird mit dem **in** -Argument angegeben und bewirkt, dass jeder INSERT-Trigger, der für die Zieltabelle definiert ist, während des Massenkopiervorgangs ausgeführt wird. Wenn FIRE_TRIGGERS nicht angegeben wird, werden keine INSERT-Trigger ausgeführt. FIRE_TRIGGERS wird für die Argumente **out**, **queryout**und **format** ignoriert.  
  
 **-i** ***input_file***<a name="i"></a>  
 Gibt den Namen einer Antwortdatei an, die für jedes Datenfeld die Antworten auf die Fragen der Eingabeaufforderung enthält, wenn ein Massenkopiervorgang im interaktiven Modus ausgeführt wird (**-n**, **-c**, **-w**oder **-N** wurde nicht angegeben).  
  
 Wenn *Eingabedatei* mit einem Bindestrich (-) oder einem Schrägstrich (/) beginnt, darf kein Leerzeichen zwischen **-i** und dem *Eingabedatei* -Wert enthalten sein.  
  
 **-k**<a name="k"></a>  
 Gibt an, dass während des Vorgangs keine Standardwerte in leere Spalten eingefügt werden, sondern ein NULL-Wert für diese Spalten beibehalten werden soll. Weitere Informationen finden Sie unter [Beibehalten von NULL-Werten oder Verwenden von Standardwerten während des Massenimports &#40;SQL Server&#41;](../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md).  
  
 **-K** ***Anwendungszweck***<a name="K"></a>   
 Deklariert den Arbeitsauslastungstyp der Anwendung beim Herstellen einer Verbindung mit einem Server. Der einzig mögliche Wert ist **ReadOnly**. Wenn **-K** nicht angegeben wird, unterstützt das bcp-Hilfsprogramm keine Konnektivität zu einem sekundären Replikat in einer Always On-Verfügbarkeitsgruppe. Weitere Informationen finden Sie unter [Aktive sekundäre Replikate: Lesbare sekundäre Replikate &#40;Always On-Verfügbarkeitsgruppen&#41;](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)wichtig sind.  
  
 **-L** ***letzte_Zeile***<a name="L"></a>  
 Gibt die Nummer der letzten Zeile an, die aus einer Tabelle exportiert oder von einer Datendatei importiert werden soll. Für diesen Parameter muss ein Wert größer als (>) 0, jedoch kleiner (<) oder gleich (=) der Nummer der letzten Zeile angegeben werden. Fehlt dieser Parameter, wird standardmäßig die letzte Zeile der Datei angenommen.  
  
 *letzte_Zeile* kann eine positive ganze Zahl mit einem Wert bis zu 2^63-1 sein.  
  
**-m** ***max_errors***<a name="m"></a>  
Gibt an, wie viele Syntaxfehler maximal auftreten können, bevor der **bcp** -Vorgang abgebrochen wird. Ein Syntaxfehler setzt einen Fehler bei der Datenkonvertierung in den Zieldatentyp voraus. Der Wert von *max_Fehler* schließt alle Fehler aus, die nur auf dem Server erkannt werden können, z.B. Einschränkungsverletzungen.  
  
 Eine Zeile, die vom Hilfsprogramm **bcp** nicht kopiert werden kann, wird ignoriert und als ein Fehler gezählt. Wenn diese Option nicht enthalten ist, wird der Standardwert 10 verwendet.  
  
> [!NOTE]
> Die Option **-m** gilt nicht für die Konvertierung der Datentypen **money** oder **bigint** .
  
**-n**<a name="n"></a>  
Führt das Massenkopieren mithilfe der systemeigenen (Datenbank-)Datentypen der Daten aus. Diese Option fordert für keines der Felder zu einer Eingabe auf; es werden die systemeigenen Werte verwendet.  
  
Weitere Informationen finden Sie unter [Verwenden des nativen Formats zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md).  
  
**-N**<a name="N"></a>  
Führt den Massenkopiervorgang mithilfe der systemeigenen (Datenbank-)Datentypen für Daten, die keinen Zeichendatentyp haben, und mithilfe von Unicode-Zeichen für Zeichendaten aus. Diese Option bietet ein besseres Leistungsverhalten als die Option **-w** und sollte verwendet werden, um Daten mithilfe einer Datendatei zwischen [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanzen zu übertragen. Die Option fordert nicht für jedes Feld zu einer Eingabe auf. Verwenden Sie diese Option, wenn Sie Daten mit erweiterten ANSI-Zeichen übertragen und die Leistungsvorteile des einheitlichen Modus nutzen möchten.  
  
 Weitere Informationen finden Sie unter [Verwenden des nativen Unicode-Formats zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md).  
  
 Wenn Sie Daten unter Verwendung von bcp.exe mit **-N** exportieren und dann importieren und eine Spalte mit Nicht-Unicode-Zeichen fester Länge vorliegt (z.B.**char(10)**), wird möglicherweise eine Warnung über abgeschnittene Daten angezeigt.  
  
 Die Warnung kann ignoriert werden. Eine Möglichkeit zum Auflösen dieser Warnung besteht darin, **-n** anstelle von **-N**zu verwenden.  
  
 **-o** ***output_file***<a name="o"></a>  
 Gibt den Namen einer Datei an, in die die Ausgabe geschrieben wird, die von der Eingabeaufforderung umgeleitet wurde.  
  
 Wenn *Ausgabedatei* mit einem Bindestrich (-) oder einem Schrägstrich (/) beginnt, darf kein Leerzeichen zwischen **-o** und dem *Ausgabedatei* -Wert enthalten sein.  
  
 **-P** ***Kennwort***<a name="P"></a>  
 Gibt das Kennwort für die Anmelde-ID an. Wenn diese Option nicht verwendet wird, fordert der Befehl **bcp** zur Eingabe eines Kennworts auf. Wenn diese Option am Ende der Befehlszeile ohne Kennwort verwendet wird, verwendet **bcp** das Standardkennwort (NULL).  
  
> [!IMPORTANT]
> [!INCLUDE[ssNoteStrongPass](../includes/ssnotestrongpass-md.md)]
  
 Zum Maskieren des Kennworts sollten Sie die Option **-P** nicht in Verbindung mit der Option **-U** angeben. Drücken Sie stattdessen nach der Angabe von **bcp** mit der Option **-U** und anderen Schaltern (geben Sie **-P**nicht an) die EINGABETASTE. Sie werden daraufhin zur Angabe eines Kennworts aufgefordert. Durch diese Methode wird sichergestellt, dass das Kennwort bei der Eingabe maskiert wird.  
  
 Wenn *Kennwort* mit einem Bindestrich (-) oder einem Schrägstrich (/) beginnt, darf kein Leerzeichen zwischen **-P** und dem *Kennwort* -Wert enthalten sein.  
  
 **-q**<a name="q"></a>  
 Führt die SET QUOTED_IDENTIFIERS ON-Anweisung in der Verbindung zwischen dem **bcp** -Hilfsprogramm und einer [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Instanz aus. Verwenden Sie diese Option, wenn Sie einen Datenbank-, Besitzer-, Tabellen- oder Sichtnamen angeben möchten, der ein Leerzeichen oder ein einfaches Anführungszeichen enthält. Schließen Sie den gesamten dreiteiligen Tabellen- oder Sichtnamen in Anführungszeichen ("") ein.  
  
 Um einen Datenbanknamen anzugeben, der ein Leerzeichen oder ein einfaches Anführungszeichen enthält, müssen Sie die Option **-q** verwenden.  
  
 **-q** gilt nicht für Werte, die an **-d**übergeben wurden.  
  
 Weitere Informationen finden Sie unter [Hinweise](#remarks)weiter unten in diesem Thema.  
  
 **-r** ***Zeilenabschluss***<a name="r"></a>  
 Gibt das Zeilenabschlusszeichen an. Der Standardwert ist **\n** (Zeilenumbruchzeichen). Mit diesem Parameter können Sie das standardmäßige Zeilenabschlusszeichen überschreiben. Weitere Informationen finden Sie unter [Specify Field and Row Terminators &#40;SQL Server&#41;](../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md).  
  
 Wenn Sie das Zeilenabschlusszeichen in Hexadezimalschreibweise in einem bcp.exe-Befehl angeben, wird der Wert bei 0x00 abgeschnitten. Wenn Sie 0x410041 angeben, wird z. B. 0x41 verwendet.  
  
 Wenn *Zeilenabschluss* mit einem Bindestrich (-) oder einem Schrägstrich (/) beginnt, darf kein Leerzeichen zwischen **-r** und dem *Zeilenabschluss* -Wert enthalten sein.  
  
 **-R**<a name="R"></a>  
 Gibt an, dass beim Massenkopieren von Währungs-, Datums- und Zeitdaten in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] das Länderformat verwendet wird, das durch die Gebietsschemaeinstellung des Clientcomputers definiert wird. Standardmäßig werden Ländereinstellungen ignoriert.  
  
 **-S** ***server_name*** [\\***instance_name***]<a name="S"></a>: Gibt die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Instanz an, mit der eine Verbindung hergestellt werden soll. Wenn kein Server angegeben wird, stellt das Hilfsprogramm **bcp** eine Verbindung mit der Standardinstanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] auf dem lokalen Computer her. Diese Option ist erforderlich, wenn **bcp** von einem Remotecomputer im Netzwerk oder von einer lokalen benannten Instanz ausgeführt wird. Um eine Verbindung mit der Standardinstanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] auf einem Server herzustellen, geben Sie lediglich *Servername*an. Wenn Sie eine Verbindung mit der benannten Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] herstellen möchten, geben Sie *server_name***\\*** instance_name* an.  
  
 **-t** ***Feldabschluss***<a name="t"></a>  
 Gibt das Feldabschlusszeichen an. Der Standardwert ist **\t** (Tabstoppzeichen). Mit diesem Parameter können Sie das standardmäßige Feldabschlusszeichen überschreiben. Weitere Informationen finden Sie unter [Angeben von Feld- und Zeilenabschlusszeichen &#40;SQL Server&#41;](../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md).  
  
 Wenn Sie das Feldabschlusszeichen in Hexadezimalschreibweise in einem bcp.exe-Befehl angeben, wird der Wert bei 0x00 abgeschnitten. Wenn Sie 0x410041 angeben, wird z. B. 0x41 verwendet.  
  
 Wenn *Feldabschluss* mit einem Bindestrich (-) oder einem Schrägstrich (/) beginnt, darf kein Leerzeichen zwischen **-r** und dem *Feldabschluss* -Wert enthalten sein.  
  
 **-T**<a name="T"></a>  
 Gibt an, dass das Hilfsprogramm **bcp** die Verbindung mit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mithilfe integrierter Sicherheit über eine vertrauenswürdige Verbindung herstellt. Die Anmeldeinformationen des Netzwerkbenutzers ( *Anmelde-ID*und *Kennwort* ) sind nicht erforderlich. Wenn **-T** nicht angegeben wird, müssen Sie **-U** und **-P** angeben, um sich erfolgreich anzumelden.
 
> [!IMPORTANT]
> Wenn das Hilfsprogramm **bcp** die Verbindung mit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mithilfe integrierter Sicherheit über eine vertrauenswürdige Verbindung herstellt, verwenden Sie die Option **-T** (vertrauenswürdige Verbindung) anstelle der Kombination aus *Benutzername* und *Kennwort* . Wenn das Hilfsprogramm **bcp** eine Verbindung mit SQL-Datenbank oder SQL Data Warehouse herstellt, wird die Windows-Authentifizierung oder Azure Active Directory-Authentifizierung nicht unterstützt. Verwenden Sie die Optionen **-U** und **-P** . 
  
 **-U** ***Anmelde-ID***<a name="U"></a>  
 Gibt die Anmelde-ID an, die zum Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]verwendet wird.  
  
> [!IMPORTANT]
> Wenn das Hilfsprogramm **bcp** die Verbindung mit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mithilfe integrierter Sicherheit über eine vertrauenswürdige Verbindung herstellt, verwenden Sie die Option **-T** (vertrauenswürdige Verbindung) anstelle der Kombination aus *Benutzername* und *Kennwort* . Wenn das Hilfsprogramm **bcp** eine Verbindung mit SQL-Datenbank oder SQL Data Warehouse herstellt, wird die Windows-Authentifizierung oder Azure Active Directory-Authentifizierung nicht unterstützt. Verwenden Sie die Optionen **-U** und **-P** .
  
 **-v**<a name="v"></a>  
 Meldet die Versionsnummer und Copyrightinformationen des **bcp** -Hilfsprogramms.  
  
 **-V** (**80** | **90** | **100** | **110** | **120** | **130** )<a name="V"></a>  
 Führt den Massenkopiervorgang mithilfe von Datentypen aus einer früheren Version von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]aus. Diese Option fordert nicht für jedes Feld zu einer Eingabe auf. Es werden die Standardwerte verwendet.  
  
 **80** = [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)]  
  
 **90** = [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]  
  
 **100** = [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] und [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]  
  
 **110** = [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
  
 **120** = [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
  
 **130** = [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]  
  
 Verwenden Sie die Option "-V80", um beispielsweise Daten für Typen zu erstellen, die nicht von [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)]unterstützt werden, jedoch in spätere Versionen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]integriert wurden.  
  
 Weitere Informationen finden Sie unter [Importieren von Daten aus früheren SQL Server-Versionen im nativen Format oder im Zeichenformat](../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md).  
  
 **-w**<a name="w"></a>  
 Führt den Massenkopiervorgang mithilfe von Unicode-Zeichen aus. Diese Option fordert für keines der Felder zu einer Eingabe auf. Es werden folgende Einstellungen verwendet: **nchar** als Speichertyp, keine Präfixe, **\t** (Tabstoppzeichen) als Feldtrennzeichen und **\n** (Zeilenumbruchzeichen) als Zeilenabschlusszeichen. **-w** ist nicht kompatibel mit **-c**.  
  
 Weitere Informationen finden Sie unter [Verwenden des Unicode-Zeichenformats zum Importieren und Exportieren von Daten &#40;SQL Server&#41;](../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md).  
  
 **-x**<a name="x"></a>  
 Bei Verwendung mit den Optionen **format** und **-f** *Formatdatei* wird anstelle der standardmäßigen Nicht-XML-Formatdatei eine XML-basierte Formatdatei generiert. Beim Importieren oder Exportieren von Daten hat **-x** keine Funktion. Wird die Option weder mit **format** noch mit **-f** *Formatdatei*verwendet, wird ein Fehler generiert.  
  
## Hinweise<a name="remarks"></a>
 Der **bcp** 13.0-Client wird bei der Installation der [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] -Tools installiert. Wenn sowohl Tools für [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] als auch für eine frühere Version von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]installiert sind, verwenden Sie, abhängig von der Reihenfolge der Werte in der PATH-Umgebungsvariablen, möglicherweise den früheren **bcp** -Client anstelle des **bcp** 13.0-Clients. Diese Umgebungsvariable definiert die Verzeichnisse, in denen von Windows nach ausführbaren Dateien gesucht wird. Führen Sie an der Windows-Befehlszeile den Befehl **bcp /v** aus, um zu ermitteln, welche Version Sie verwenden. Informationen zum Festlegen des Befehlspfads in der PATH-Umgebungsvariablen finden Sie in der Windows-Hilfe.  
 
Das Hilfsprogramm „bcp“ kann auch separat aus dem [Microsoft SQL Server 2016 Feature Pack](https://www.microsoft.com/en-us/download/details.aspx?id=52676)heruntergeladen werden.  Wählen Sie entweder `ENU\x64\MsSqlCmdLnUtils.msi` oder `ENU\x86\MsSqlCmdLnUtils.msi`aus.

  
 XML-Formatdateien werden nur unterstützt, wenn die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Tools zusammen mit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client installiert werden.  
  
 Informationen zum Speicherort und zum Verwenden des Hilfsprogramms **bcp** sowie zu den für Eingabeaufforderungs-Hilfsprogramme geltenden Syntaxkonventionen finden Sie unter [Referenz zum Eingabeaufforderungs-Hilfsprogramm &#40;Datenbankmodul&#41;](../tools/command-prompt-utility-reference-database-engine.md).  
  
 Informationen zum Vorbereiten von Daten für Massenimport- oder Massenexportvorgänge finden Sie unter [Vorbereiten von Daten für den Massenexport oder -import &#40;SQL Server&#41;](../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md).  
  
 Informationen dazu, wann Zeileneinfügevorgänge, die durch den Massenimport ausgeführt werden, im Transaktionsprotokoll protokolliert werden, finden Sie unter [Voraussetzungen für die minimale Protokollierung beim Massenimport](../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md).  
  
## <a name="native-data-file-support"></a>Systemeigene Datendateiunterstützung  
 In [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]unterstützt das **bcp** -Hilfsprogramm nur native Datendateien, die mit [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)], [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]und [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]kompatibel sind.  
  
## <a name="computed-columns-and-timestamp-columns"></a>Berechnete Spalten und Zeitstempel-Spalten  
 In der zu importierenden Datendatei enthaltene Werte für berechnete oder **timestamp** -Spalten werden ignoriert. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] weist Werte automatisch zu. Wenn die Datendatei keine Werte für die berechneten oder **timestamp** -Spalten der Tabelle enthält, geben Sie mithilfe einer Formatdatei an, dass die berechneten oder **timestamp** -Spalten beim Importieren von Daten ausgelassen werden sollen. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] weist diesen Spalten automatisch Werte zu.  
  
 Berechnete und **timestamp** -Spalten werden wie gewohnt aus [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in eine Datendatei massenkopiert.  
  
## <a name="specifying-identifiers-that-contain-spaces-or-quotation-marks"></a>Angeben von Bezeichnern mit Leerzeichen oder Anführungszeichen  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Bezeichner können Zeichen wie z.B. eingebettete Leerzeichen und Anführungszeichen enthalten. Diese Bezeichner müssen folgendermaßen behandelt werden:  
  
-   Wenn Sie an der Eingabeaufforderung einen Bezeichner oder Dateinamen angeben, der ein Leerzeichen oder ein Anführungszeichen enthält, müssen Sie den Bezeichner in Anführungszeichen ("") einschließen.  
  
     Mit dem Befehl `bcp out` wird beispielsweise die Datendatei `Currency Types.dat`erstellt:  
  
    ```  
    bcp AdventureWorks2012.Sales.Currency out "Currency Types.dat" -T -c  
    ```  
  
-   Sie müssen die Option **-q** verwenden, um einen Datenbanknamen anzugeben, der ein Leerzeichen oder Anführungszeichen enthält.  
  
-   Bei Besitzer-, Tabellen- oder Sichtnamen, die eingebettete Leerzeichen oder Anführungszeichen enthalten, ist Folgendes möglich:  
  
    -   Angeben der Option **-q** .  
  
    -   Einschließen des Besitzer-, Tabellen- oder Sichtnamens in eckige Klammern ([]) innerhalb der Anführungszeichen.  
  
## <a name="data-validation"></a>Datenüberprüfung  
 **bcp** erzwingt nun Datenüberprüfungen, die dazu führen können, dass Skripts einen Fehler erzeugen, wenn sie für ungültige Daten in einer Datendatei ausgeführt werden. So wird durch **bcp** jetzt Folgendes überprüft:  
  
-   Die native Darstellung der Datentypen **float** oder **real** ist gültig.  
  
-   Unicode-Daten besitzen eine gerade Bytelänge.  
  
 Formulare mit ungültigen Daten, die in früheren Versionen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] noch massenimportiert werden konnten, werden nun möglicherweise nicht mehr geladen. In früheren Versionen trat der Fehler erst auf, wenn ein Client versuchte, auf die ungültigen Daten zuzugreifen. Durch die zusätzliche Überprüfung werden überraschende Ergebnisse beim Abfragen der Daten nach dem Massenladen minimiert.  
  
## <a name="bulk-exporting-or-importing-sqlxml-documents"></a>Massenexportieren und -importieren von SQLXML-Dokumenten  
 Verwenden Sie in der Formatdatei einen der folgenden Datentypen für den Massenexport oder -import von SQLXML-Daten.  
  
|Datentyp|Wirkung|  
|---------------|------------|  
|SQLCHAR oder SQLVARYCHAR|Die Daten werden in der Clientcodepage gesendet bzw. in der durch die Sortierung implizierten Codeseite. Der Effekt ist derselbe, als wenn der Schalter **-c** ohne eine Formatdatei angegeben wird.|  
|SQLNCHAR oder SQLNVARCHAR|Die Daten werden im Unicode-Format gesendet. Der Effekt ist derselbe, als wenn der Schalter **-w** ohne eine Formatdatei angegeben wird.|  
|SQLBINARY oder SQLVARYBIN|Die Daten werden ohne Konvertierung gesendet.|  
  
## <a name="permissions"></a>Berechtigungen  
 Um **bcp out** ausführen zu können, sind SELECT-Berechtigungen für die Quelltabelle erforderlich.  
  
 Um **bcp in** ausführen zu können, sind mindestens SELECT/INSERT-Berechtigungen für die Zieltabelle erforderlich. Darüber hinaus sind ALTER TABLE-Berechtigungen erforderlich, wenn eine der folgenden Bedingungen zutrifft:  
  
-   Es sind Einschränkungen vorhanden, und der CHECK_CONSTRAINTS-Hinweis wurde nicht angegeben.  
  
    > [!NOTE]
    > Die Deaktivierung von Einschränkungen wurde als Standardverhalten festgelegt. Verwenden Sie die Option **-h** mit dem CHECK_CONSTRAINTS-Hinweis, wenn Einschränkungen explizit aktiviert werden sollen.
  
-   Es sind Trigger vorhanden, und der FIRE_TRIGGER-Hinweis wurde nicht angegeben.  
  
    > [!NOTE]
    > Standardmäßig werden Trigger nicht ausgelöst. Verwenden Sie die Option **-h** mit dem FIRE_TRIGGERS-Hinweis, wenn Trigger explizit ausgelöst werden sollen.
  
-   Mithilfe der Option **-E** importieren Sie Identitätswerte aus einer Datendatei.  
  
> [!NOTE]
> ALTER TABLE-Berechtigungen für die Zieltabelle sind erst seit [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]erforderlich. Diese neue Anforderung kann dazu führen, dass **bcp** -Skripts, die keine Trigger und Einschränkungsüberprüfungen erzwingen, einen Fehler erzeugen, wenn das Benutzerkonto nicht über ALTER TABLE-Berechtigungen für die Zieltabelle verfügt.
  
## <a name="character-mode--c-and-native-mode--n-best-practices"></a>Zeichenmodus (-c)- und einheitlicher Modus (-n) – Bewährte Methoden  
 Dieser Abschnitt beinhaltet Empfehlungen für den Zeichenmodus (-c) und den einheitlichen Modus (-n).  
  
-   (Administrator/Benutzer) Wenn möglich, verwenden Sie das einheitliche Format (-n), um das Trennzeichenproblem zu vermeiden. Verwenden Sie das einheitliche Format für Export- und Importvorgänge mit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Exportieren Sie Daten aus [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mit der -c- oder -w-Option, wenn die Daten in eine Nicht-[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Datenbank importiert werden.  
  
-   (Administrator) überprüfen Sie Daten, wenn Sie BCP OUT verwenden. Wenn Sie z. B. BCP OUT, BCP IN und dann BCP OUT verwenden, überprüfen Sie, ob die Daten ordnungsgemäß exportiert werden, und ob die Abschlusszeichenwerte nicht als Teil eines Datenwerts verwendet werden. Erwägen Sie, die Standardabschlusszeichen (mithilfe von -t- und -r-Optionen) mit zufälligen Hexadezimalwerten zu überschreiben, um Konflikte zwischen Abschlusszeichenwerten und Datenwerten zu vermeiden.  
  
-   (Benutzer) Verwenden Sie ein langes und eindeutiges Abschlusszeichen (eine Byte- oder Zeichensequenz), um die Wahrscheinlichkeit eines Konflikts mit dem tatsächlichen Zeichenfolgenwert zu minimieren. Verwenden Sie dazu die -t-Option und die -r-Option.  
  
## <a name="examples"></a>Beispiele  
 Dieser Abschnitt enthält die folgenden Beispiele:  
 
-   A. Identifizieren der Version des Hilfsprogramms **bcp**
  
-   B. Kopieren von Tabellenzeilen in eine Datendatei (mit einer vertrauenswürdigen Verbindung)  
  
-   [C.](#c-copying-table-rows-into-a-data-file-with-mixed-mode-authentication) Kopieren von Tabellenzeilen in eine Datendatei (mit Authentifizierung im gemischten Modus)  
  
-   D. Kopieren von Daten aus einer Datei in eine Tabelle  
  
-   E. Kopieren einer bestimmten Spalte in eine Datendatei  
  
-   F. Kopieren einer bestimmten Zeile in eine Datendatei  
  
-   G. Kopieren von Daten aus einer Abfrage in eine Datendatei  
  
-   H. Erstellen von Formatdateien
    
-   I. Verwenden einer Formatdatei für einen Massenimport mithilfe von **bcp**  


### <a name="example-test-conditions"></a>**Beispieltestbedingungen**
In den folgenden Beispielen wird die `WideWorldImporters` -Beispieldatenbank für SQL Server (ab 2016) und Azure SQL-Datenbank verwendet.  `WideWorldImporters` kann von heruntergeladen werden [ https://github.com/Microsoft/sql-server-samples/releases/tag/wide-world-importers-v1.0 ](https://github.com/Microsoft/sql-server-samples/releases/tag/wide-world-importers-v1.0).  Die Syntax zum Wiederherstellen der Beispieldatenbank finden Sie unter [RESTORE (Transact-SQL)](../t-sql/statements/restore-statements-transact-sql.md) .  Sofern nicht anders angegeben, wird bei diesem Beispiel vorausgesetzt, dass Sie die Windows-Authentifizierung verwenden und über eine vertrauenswürdige Verbindung mit der Serverinstanz verfügen, auf der Sie den **bcp** -Befehl ausführen.  Ein Verzeichnis namens `D:\BCP` wird in vielen der Beispiele verwendet.

Das folgende Skript erstellt eine leere Kopie der `WideWorldImporters.Warehouse.StockItemTransactions`-Tabelle und fügt dann eine Primärschlüsseleinschränkung hinzu.  Führen Sie das folgende T-SQL-Skript in SQL Server Management Studio (SSMS) aus.

```tsql  
USE WideWorldImporters;  
GO  

SET NOCOUNT ON;

IF NOT EXISTS (SELECT * FROM sys.tables WHERE name = 'Warehouse.StockItemTransactions_bcp')     
BEGIN
    SELECT * INTO WideWorldImporters.Warehouse.StockItemTransactions_bcp
    FROM WideWorldImporters.Warehouse.StockItemTransactions  
    WHERE 1 = 2;  

    ALTER TABLE Warehouse.StockItemTransactions_bcp 
    ADD CONSTRAINT PK_Warehouse_StockItemTransactions_bcp PRIMARY KEY NONCLUSTERED 
    (StockItemTransactionID ASC);
END
```

> [!NOTE]
> Schneiden Sie die `StockItemTransactions_bcp` -Tabelle bei Bedarf ab.
>
> TRUNCATE TABLE WideWorldImporters.Warehouse.StockItemTransactions_bcp;

### <a name="a--identify-bcp-utility-version"></a>A.  Identifizieren der Version des Hilfsprogramms **bcp**
Geben Sie folgenden Befehl an der Eingabeaufforderung ein:
```
bcp -v
```
  
### <a name="b-copying-table-rows-into-a-data-file-with-a-trusted-connection"></a>B. Kopieren von Tabellenzeilen in eine Datendatei (mit einer vertrauenswürdigen Verbindung)  
In den folgenden Beispielen wird die Verwendung der Option **out** in der `WideWorldImporters.Warehouse.StockItemTransactions`-Tabelle veranschaulicht.

- **Grundlegend**  
In diesem Beispiel wird die Datendatei `StockItemTransactions_character.bcp` erstellt, und die Tabellendaten werden mithilfe eines **Zeichenformats** in die Datendatei kopiert.

  Geben Sie folgenden Befehl an der Eingabeaufforderung ein:
  ```
  bcp WideWorldImporters.Warehouse.StockItemTransactions out D:\BCP\StockItemTransactions_character.bcp -c -T
  ```
 
 - **Expanded**  
In diesem Beispiel wird die Datendatei `StockItemTransactions_native.bcp` erstellt, und die Tabellendaten werden mithilfe des **nativen** Formats in die Datendatei kopiert.  Im Beispiel werden auch die maximale Anzahl von Syntaxfehlern, eine Fehlerdatei und eine Ausgabedatei angegeben.

    Geben Sie folgenden Befehl an der Eingabeaufforderung ein:
    ```
    bcp WideWorldImporters.Warehouse.StockItemTransactions OUT D:\BCP\StockItemTransactions_native.bcp -m 1 -n -e D:\BCP\Error_out.log -o D:\BCP\Output_out.log -S -T
    ``` 
 
Informieren Sie sich unter `Error_out.log` und `Output_out.log`.  `Error_out.log` sollte leer sein.  Vergleichen Sie die Dateigrößen zwischen `StockItemTransactions_character.bcp` und `StockItemTransactions_native.bcp`. 
   
### <a name="c-copying-table-rows-into-a-data-file-with-mixed-mode-authentication"></a>C. Kopieren von Tabellenzeilen in eine Datendatei (mit Authentifizierung im gemischten Modus)  
Im folgenden Beispiel wird die Verwendung der Option **out** in der `WideWorldImporters.Warehouse.StockItemTransactions`-Tabelle veranschaulicht.  In diesem Beispiel wird die Datendatei `StockItemTransactions_character.bcp` erstellt, und die Tabellendaten werden mithilfe eines **Zeichenformats** in die Datendatei kopiert.  
  
 Bei diesem Beispiel wird vorausgesetzt, dass Sie die Authentifizierung im gemischten Modus verwenden. Sie müssen daher den Schalter **-U** verwenden, um die Anmelde-ID anzugeben. Sofern Sie keine Verbindung mit der Standardinstanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] auf dem lokalen Computer herstellen, müssen Sie außerdem mit dem Schalter **-S** den Systemnamen und optional einen Instanznamen angeben.  

Geben Sie folgenden Befehl an der Eingabeaufforderung ein: \(Das System fordert Sie zur Eingabe des Kennworts auf.\)
```  
bcp WideWorldImporters.Warehouse.StockItemTransactions out D:\BCP\StockItemTransactions_character.bcp -c -U<login_id> -S<server_name\instance_name>
```  
  
### <a name="d-copying-data-from-a-file-to-a-table"></a>D. Kopieren von Daten aus einer Datei in eine Tabelle  
Die folgenden Beispiele veranschaulichen die Option **in** für die `WideWorldImporters.Warehouse.StockItemTransactions_bcp`-Tabelle unter Verwendung der oben erstellten Dateien.
  
- **Standard**  
Dieses Beispiel verwendet die `StockItemTransactions_character.bcp` -Datendatei, die zuvor erstellt wurde.

  Geben Sie folgenden Befehl an der Eingabeaufforderung ein:
  ```  
  bcp WideWorldImporters.Warehouse.StockItemTransactions_bcp IN D:\BCP\StockItemTransactions_character.bcp -c -T  
  ```  

- **Expanded**  
Dieses Beispiel verwendet die `StockItemTransactions_native.bcp` -Datendatei, die zuvor erstellt wurde.  Im Beispiel werden auch der Hinweis **TABLOCK**, die Batchgröße, die maximale Anzahl von Syntaxfehlern, eine Fehlerdatei und eine Ausgabedatei angegeben.
  
  Geben Sie folgenden Befehl an der Eingabeaufforderung ein:
  ```  
  bcp WideWorldImporters.Warehouse.StockItemTransactions_bcp IN D:\BCP\StockItemTransactions_native.bcp -b 5000 -h "TABLOCK" -m 1 -n -e D:\BCP\Error_in.log -o D:\BCP\Output_in.log -S -T 
  ```    
  Informieren Sie sich unter `Error_in.log` und `Output_in.log`.
   
### <a name="e-copying-a-specific-column-into-a-data-file"></a>E. Kopieren einer bestimmten Spalte in eine Datendatei  
Zum Kopieren einer bestimmten Spalte können Sie die Option **queryout** verwenden.  Im folgenden Beispiel wird nur die `StockItemTransactionID` -Spalte der `Warehouse.StockItemTransactions` -Tabelle in eine Datendatei kopiert. 
  
Geben Sie folgenden Befehl an der Eingabeaufforderung ein:
  
```  
bcp "SELECT StockItemTransactionID FROM WideWorldImporters.Warehouse.StockItemTransactions WITH (NOLOCK)" queryout D:\BCP\StockItemTransactionID_c.bcp -c -T
```  
  
### <a name="f-copying-a-specific-row-into-a-data-file"></a>F. Kopieren einer bestimmten Zeile in eine Datendatei  
Zum Kopieren einer bestimmten Zeile können Sie die Option **queryout** verwenden. Im folgenden Beispiel wird nur die Zeile für den Kontakt `Amy Trefl` aus der `WideWorldImporters.Application.People`-Tabelle in eine Datendatei `Amy_Trefl_c.bcp` kopiert.  Hinweis: Der Schalter **-d** wird zum Identifizieren der Datenbank verwendet.
  
Geben Sie folgenden Befehl an der Eingabeaufforderung ein: 
```  
bcp "SELECT * from Application.People WHERE FullName = 'Amy Trefl'" queryout D:\BCP\Amy_Trefl_c.bcp -d WideWorldImporters -c -T
```  
  
### <a name="g-copying-data-from-a-query-to-a-data-file"></a>G. Kopieren von Daten aus einer Abfrage in eine Datendatei  
Verwenden Sie die Option **queryout** zum Kopieren des Resultsets einer Transact-SQL-Anweisung in eine Datendatei.  Im folgenden Beispiel werden die Namen aus der `WideWorldImporters.Application.People`-Tabelle nach vollständigem Namen geordnet in die Datendatei `People.txt` kopiert.  Hinweis: Der Schalter **-t** wird verwendet, um eine durch Trennzeichen getrennte Datei zu erstellen.
  
Geben Sie folgenden Befehl an der Eingabeaufforderung ein:
```  
bcp "SELECT FullName, PreferredName FROM WideWorldImporters.Application.People ORDER BY FullName" queryout D:\BCP\People.txt -t, -c -T
```  
  
### <a name="h-creating-format-files"></a>H. Erstellen von Formatdateien  
In dem folgenden Beispiel werden drei verschiedene Formatdateien für die `Warehouse.StockItemTransactions`-Tabelle in der `WideWorldImporters`-Datenbank erstellt.  Überprüfen Sie den Inhalt der einzelnen erstellten Dateien.
  
Geben Sie folgende Befehle an der Eingabeaufforderung ein:
  
```  
REM non-XML character format
bcp WideWorldImporters.Warehouse.StockItemTransactions format nul -f D:\BCP\StockItemTransactions_c.fmt -c -T 

REM non-XML native format
bcp WideWorldImporters.Warehouse.StockItemTransactions format nul -f D:\BCP\StockItemTransactions_n.fmt -n -T

REM XML character format
bcp WideWorldImporters.Warehouse.StockItemTransactions format nul -f D:\BCP\StockItemTransactions_c.xml -x -c -T
 
```  
  
> [!NOTE]  
>  Um die Option **-x** zu verwenden, müssen Sie über einen **bcp** 9.0-Client verfügen. Informationen zum Verwenden des **bcp** 9.0-Clients finden Sie unter „[Hinweise](#remarks)“.  
  
 Weitere Informationen finden Sie unter [Nicht-XML-Formatdateien &#40;SQL Server&#41;](../relational-databases/import-export/non-xml-format-files-sql-server.md) und [XML-Formatdateien &#40;SQL Server&#41;](../relational-databases/import-export/xml-format-files-sql-server.md).  
  
### <a name="i-using-a-format-file-to-bulk-import-with-bcp"></a>I. Verwenden einer Formatdatei für einen Massenimport mithilfe von bcp  
Wenn Sie eine zuvor erstellte Formatdatei zum Importieren von Daten in eine [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Instanz verwenden möchten, müssen Sie den Schalter **-f** mit der Option **in** verwenden.  So wird beispielsweise durch den folgenden Befehl der Inhalt der Datendatei `StockItemTransactions_character.bcp`in eine Kopie der `Warehouse.StockItemTransactions_bcp` -Tabelle massenkopiert, wobei die zuvor erstellte Formatdatei `StockItemTransactions_c.xml`verwendet wird.  Hinweis: Der Schalter **-L** wird dazu verwendet, um nur die ersten 100 Datensätze zu importieren.
  
Geben Sie folgenden Befehl an der Eingabeaufforderung ein:
```  
bcp WideWorldImporters.Warehouse.StockItemTransactions_bcp in D:\BCP\StockItemTransactions_character.bcp -L 100 -f D:\BCP\StockItemTransactions_c.xml -T 
```  
  
> [!NOTE]  
>  Formatdateien erweisen sich besonders dann als nützlich, wenn die Felder in der Datendatei z. B. hinsichtlich Anzahl, Reihenfolge oder Datentypen von den Tabellenspalten abweichen. Weitere Informationen finden Sie unter [Formatdateien zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)erforderlich.  
  
### <a name="j-specifying-a-code-page"></a>J. Angeben einer Codepage  
 Das folgende teilweise Codebeispiel zeigt einen bcp-Importvorgang mit angegebener Codeseite 65001:  
  
```  
bcp.exe MyTable in "D:\data.csv" -T -c -C 65001 -t , ...  
```  
  
 Das folgende teilweise Codebeispiel zeigt einen bcp-Exportvorgang mit angegebener Codeseite 65001:  
  
```  
bcp.exe MyTable out "D:\data.csv" -T -c -C 65001 -t , ...  
```  
  
## <a name="additional-examples"></a>Zusätzliche Beispiele  
|Die folgenden Themen enthalten Beispiele zur Verwendung von „bcp“: |
|---|
|Datenformate für Massenimport oder Massenexport (SQL Server)<br />&emsp;&#9679;&emsp;[Verwenden das native Format zum Importieren oder Exportieren von Daten (SQL Server)](../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Verwenden des Zeichenformats zum Importieren und Exportieren von Daten (SQL Server)](../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Verwenden von nativen Unicode-Formaten zum Importieren oder Exportieren von Daten (SQL Server)](../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Verwenden des Unicode-Zeichenformats zum Importieren und Exportieren von Daten (SQL Server)](../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)<br /><br />[Angeben von Feld- und Zeilenabschlusszeichen (SQL Server)](../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)<br /><br />[Beibehalten von NULL-Werten oder Verwenden von Standardwerten während des Massenimports (SQL Server)](../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)<br /><br />[Beibehalten von Identitätswerten beim Massenimport von Daten (SQL Server)](../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)<br /><br />Formatdateien zum Importieren oder Exportieren von Daten (SQL Server)<br />&emsp;&#9679&emsp;[Erstellen einer Formatdatei (SQL Server)](../relational-databases/import-export/create-a-format-file-sql-server.md)<br />&emsp;&#9679;&emsp;[Massenimport von Daten mithilfe einer Formatdatei (SQL Server)](../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Überspringen einer Tabellenspalte mithilfe einer Formatdatei (SQL Server)](../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)<br />&emsp;&#9679;&emsp;[Auslassen eines Datenfelds mithilfe einer Formatdatei (SQL Server)](../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)<br />&emsp;&#9679;&emsp;[Verwenden einer Formatdatei zum Zuordnen von Tabellenspalten zu Datendateifeldern (SQL Server)](../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)<br /><br />[Beispiele für den Massenimport und -export von XML-Dokumenten (SQL Server)](../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)<br /><p>                                                                                                                                                                                                                  </p>|

## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Vorbereiten von Daten für den Massenexport oder -import &#40;SQL Server&#41;](../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../t-sql/functions/openrowset-transact-sql.md)   
 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../t-sql/statements/set-quoted-identifier-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [sp_tableoption &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)   
 [Formatdateien zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)  
  
  

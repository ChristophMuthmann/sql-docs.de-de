---
title: "Erstellen der Funktion zum Abrufen der Änderungsdaten | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: change-data-capture
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- incremental load [Integration Services],creating function
ms.assetid: 55dd0946-bd67-4490-9971-12dfb5b9de94
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f3e717ccf46cc7929c510229b19a16eb5a857487
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="create-the-function-to-retrieve-the-change-data"></a>Erstellen der Funktion zum Abrufen der Änderungsdaten
  Nach Abschluss der Ablaufsteuerung für ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket, das ein inkrementelles Laden von Änderungsdaten ausführt, ist der nächste Task die Erstellung einer Tabellenwertfunktion, mit der die Änderungsdaten abgerufen werden. Sie müssen diese Funktion nur einmal vor dem ersten inkrementellen Laden erstellen.  
  
> [!NOTE]  
>  Das Erstellen einer Funktion zum Abrufen der Änderungsdaten ist der zweite Schritt beim Erstellen eines Pakets, das ein inkrementelles Laden von Änderungsdaten ausführt. Eine Beschreibung des Gesamtprozesses zum Entwurf dieses Pakets finden Sie unter [Change Data Capture &#40;SSIS&#41;](../../integration-services/change-data-capture/change-data-capture-ssis.md).  
  
## <a name="design-considerations-for-change-data-capture-functions"></a>Entwurfsaspekte für Change Data Capture-Funktionen  
 Zum Abrufen von Änderungsdaten ruft eine Quellkomponente im Datenfluss des Pakets eine der folgenden Change Data Capture-Abfragefunktionen auf:  
  
-   **cdc.fn_cdc_get_net_changes_<Aufzeichnungsinstanz>** Bei dieser Abfrage enthält die für jedes Update zurückgegebene einzelne Zeile den finalen Status jeder geänderten Zeile. In den meisten Fällen benötigen Sie nur die von einer Abfrage von Nettoänderungen zurückgegebenen Daten. Weitere Informationen finden Sie unter [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md).  
  
-   **cdc.fn_cdc_get_all_changes_<Aufzeichnungsinstanz>** Diese Abfrage gibt alle Änderungen zurück, die während des Aufzeichnungsintervalls in jeder Zeile aufgetreten sind. Weitere Informationen finden Sie unter [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md).  
  
 Die Quellkomponente nimmt dann die von der Funktion zurückgegebenen Ergebnisse und übergibt sie an Downstream-Transformationen und -Ziele, die die Änderungsdaten auf das endgültige Ziel anwenden.  
  
 Eine [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Quellkomponente kann diese Change Data Capture-Funktionen jedoch nicht direkt aufrufen. Eine [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Quellkomponente erfordert Metadaten zu den Spalten, die die Abfrage zurückgibt. Die Change Data Capture-Funktionen definieren nicht die Spalten ihrer Ausgabetabelle. Somit geben diese Funktionen nicht genügend Metadaten für eine [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Quellkomponente zurück.  
  
 Verwenden Sie stattdessen eine Tabellenwert-Wrapperfunktion, da diese Art von Funktion die Spalten ihrer Ausgabetabelle explizit in ihrer RETURNS-Klausel definiert. Diese explizite Definition von Spalten stellt die Metadaten bereit, die eine [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Quellkomponente benötigt. Sie müssen diese Funktion für jede Tabelle erstellen, für die Sie Änderungsdaten abrufen möchten.  
  
 Sie haben zwei Möglichkeiten, die Tabellenwert-Wrapperfunktion zu erstellen, die die Data Capture-Abfragefunktion aufruft:  
  
-   Sie können die gespeicherte Systemprozedur **sys.sp_cdc_generate_wrapper_function** aufrufen, damit diese die Tabellenwertfunktionen für Sie erstellt.  
  
-   Sie können mithilfe der Hinweise und Beispiele in diesem Thema Ihre eigene Tabellenwertfunktion schreiben.  
  
## <a name="calling-a-stored-procedure-to-create-the-table-valued-function"></a>Aufrufen der gespeicherten Prozedur zur Erstellung der Tabellenwertfunktion  
 Die schnellste und einfachste Möglichkeit zur Erstellung der benötigten Tabellenwertfunktionen ist der Aufruf der gespeicherten Systemprozedur **sys.sp_cdc_generate_wrapper_function** . Diese gespeicherte Prozedur erzeugt Skripts zur Erstellung der Wrapperfunktionen, die speziell für die Anforderungen der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Quellkomponente entwickelt wurden.  
  
> [!IMPORTANT]  
>  Die gespeicherte Systemprozedur **sys.sp_cdc_generate_wrapper_function** erstellt nicht direkt die Wrapperfunktionen. Die gespeicherte Prozedur generiert stattdessen die CREATE-Skripts für die Wrapperfunktionen. Der Entwickler muss die von der gespeicherten Prozedur erzeugten CREATE-Skripts ausführen, bevor ein Paket für inkrementelles Laden die Wrapperfunktionen aufrufen kann.  
  
 Um zu verstehen, wie diese gespeicherte Systemprozedur verwendet wird, müssen Sie verstehen, wie diese Prozedur funktioniert, welche Skripts die Prozedur generiert und welche Wrapperfunktionen diese Skripts erstellen.  
  
### <a name="understanding-and-using-the-stored-procedure"></a>Grundlegendes zu gespeicherten Prozeduren und deren Verwendung  
 Die gespeicherte Systemprozedur **sys.sp_cdc_generate_wrapper_function** generiert Skripts zur Erstellung von Wrapperfunktionen, die von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paketen verwendet werden.  
  
 Der folgende Code stellt die ersten Zeilen der Definition der gespeicherten Prozedur dar:  
  
 `CREATE PROCEDURE sys.sp_cdc_generate_wrapper_function`  
  
 `(`  
  
 `@capture_instance sysname = null`  
  
 `@closed_high_end_point bit = 1,`  
  
 `@column_list = null,`  
  
 `@update_flag_list = null`  
  
 `)`  
  
 Alle Parameter für die gespeicherte Prozedur sind optional. Wenn Sie die gespeicherte Prozedur ohne die Bereitstellung von Werten für einen der Parameter aufrufen, erstellt die gespeicherte Prozedur Wrapperfunktionen für alle Aufzeichnungsinstanzen, auf die Sie Zugriff haben.  
  
> [!NOTE]  
>  Weitere Informationen über die Syntax dieser gespeicherten Prozedur und ihre Parameter finden Sie unter [sys.sp_cdc_generate_wrapper_function &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md).  
  
 Die gespeicherte Funktion generiert immer eine Wrapperfunktion, um alle Änderungen aus allen Aufzeichnungsinstanzen zurückzugeben. Wenn der *@supports_net_changes* -Parameter während der Erstellung der Aufzeichnungsinstanz festgelegt wurde, generiert die gespeicherte Prozedur außerdem eine Wrapperfunktion, die die Nettoänderungen von jeder entsprechenden Aufzeichnungsinstanz zurückgibt.  
  
 Die gespeicherte Prozedur gibt ein Resultset mit zwei Spalten zurück:  
  
-   Den Namen der Wrapperfunktion, die von der gespeicherten Prozedur generiert wurde. Diese gespeicherte Prozedur ruft den Funktionsnamen vom Namen der Aufzeichnungsinstanz ab. (Der Funktionsname lautet „fn_all_changes_“, gefolgt vom Namen der Aufzeichnungsinstanz. Das Präfix, das für die Funktion für Nettoänderungen verwendet wird, lautet, wenn es erstellt wird, „fn_net_changes_“.)  
  
-   Die CREATE-Anweisung für die Wrapperfunktion.  
  
### <a name="understanding-and-using-the-scripts-created-by-the-stored-procedure"></a>Grundlegendes zu den von der gespeicherten Prozedur erstellten Skripts und deren Verwendung  
 Normalerweise verwendet ein Entwickler eine INSERT...EXEC-Anweisung, um die gespeicherte Prozedur **sys.sp_cdc_generate_wrapper_function** aufzurufen und die Skripts zu speichern, die die gespeicherte Prozedur in einer temporären Tabelle erstellt. Anschließend könnte jedes Skript einzeln ausgewählt und ausgeführt werden, um die entsprechende Wrapperfunktion zu erstellen. Ein Entwickler könnte jedoch auch einen Satz von SQL-Befehlen verwenden, um alle CREATE-Skripts auszuführen, wie im folgenden Beispielcode dargestellt:  
  
```  
create table #wrapper_functions  
      (function_name sysname, create_stmt nvarchar(max))  
insert into #wrapper_functions  
exec sys.sp_cdc_generate_wrapper_function  
  
declare @stmt nvarchar(max)  
declare #hfunctions cursor local fast_forward for   
      select create_stmt from #wrapper_functions  
open #hfunctions  
fetch #hfunctions into @stmt  
while (@@fetch_status <> -1)  
begin  
      exec sp_executesql @stmt  
      fetch #hfunctions into @stmt  
end  
close #hfunctions  
deallocate #hfunctions  
```  
  
### <a name="understanding-and-using-the-functions-created-by-the-stored-procedure"></a>Grundlegendes zu den von der gespeicherten Prozedur erstellten Funktionen und deren Verwendung  
 Um die Zeitachse der aufgezeichneten Änderungsdaten systematisch abzuarbeiten, gehen die generierten Wrapperfunktionen davon aus, dass der *@end_time* -Parameter für ein Intervall der *@start_time* -Parameter für das folgende Intervall ist. Wenn diese Konvention eingehalten wird, kann die generierte Wrapperfunktion folgende Aufgaben ausführen:  
  
-   Zuordnung der Datums-/Zeitwerte zu den intern verwendeten LSN-Werten  
  
-   Sicherstellen, dass keine Daten verloren gehen oder wiederholt werden  
  
 Zur Vereinfachung der Abfrage aller Zeilen einer Änderungstabelle unterstützt die generierte Wrapperfunktion auch folgende Konventionen:  
  
-   Wenn der @start_time-Parameter NULL ist, verwendet die Wrapperfunktion den niedrigsten LSN-Wert in der Aufzeichnungsinstanz als untere Begrenzung der Abfrage.  
  
-   Wenn der @end_time-Parameter NULL ist, verwendet die Wrapperfunktion den höchsten LSN-Wert in der Aufzeichnungsinstanz als obere Begrenzung der Abfrage.  
  
 Die meisten Benutzer sollten die von der gespeicherten Systemprozedur **sys.sp_cdc_generate_wrapper_function** erstellte Wrapperfunktion ohne Änderungen verwenden können. Wenn Sie die Wrapperfunktion anpassen möchten, müssen Sie jedoch die CREATE-Skripts anpassen, bevor Sie diese ausführen.  
  
 Wenn Ihr Paket die Wrapperfunktion aufruft, muss das Paket Werte für drei Parameter bereitstellen. Diese drei Parameter entsprechen den drei Parametern, die von den Change Data Capture-Funktionen verwendet werden. Dabei handelt es sich um folgende drei Parameter:  
  
-   Die Werte für Startdatum und -uhrzeit sowie für Enddatum und -uhrzeit für das Intervall. Während die Wrapperfunktionen Datums-/Zeitwerte als Endpunkte für das Abfrageintervall verwenden, verwenden die Change Data Capture-Funktionen zwei LSN-Werte als Endpunkte.  
  
-   Den Zeilenfilter. Für die Wrapperfunktionen und die Change Data Capture-Funktionen ist der *@row_filter_option* -Parameter identisch. Weitere Informationen finden Sie unter [cdc.fn_cdc_get_all_changes_&#60;Aufzeichnungsinstanz&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md) und [cdc.fn_cdc_get_net_changes_&#60;Aufzeichnungsinstanz&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md).  
  
 Das von den Wrapperfunktionen zurückgegebene Resultset enthält folgende Daten:  
  
-   Alle angeforderten Spalten der Änderungsdaten  
  
-   Eine Spalte mit dem Namen __CDC_OPERATION, die ein Feld mit einem oder zwei Zeichen verwendet, um den der Zeile zugeordneten Vorgang zu kennzeichnen. Folgende Werte sind für dieses Feld gültig: „I“ für insert (einfügen), „D“ für delete (löschen), „UO“ für update old values (alte Werte aktualisieren) und „UN“ für update new values (neue Werte aktualisieren).  
  
-   Updateflags, wenn Sie diese anfordern, die als bit-Spalten hinter dem Vorgangscode in der vom *@update_flag_list* -Parameter festgelegten Reihenfolge angezeigt werden. Diese Spalten werden bezeichnet, indem an den zugeordneten Spaltennamen „_uflag“ angehängt wird.  
  
 Wenn Ihr Paket eine Wrapperfunktion aufruft, die alle Änderungen abfragt, gibt die Wrapperfunktion außerdem die Spalten __CDC_STARTLSN und \__CDC_SEQVAL zurück. Diese beiden Spalten sind die erste bzw. die zweite Spalte des Resultsets. Die Wrapperfunktion sortiert das Resultset außerdem auf der Grundlage dieser beiden Spalten.  
  
## <a name="writing-your-own-table-value-function"></a>Schreiben einer eigenen Tabellenwert-Funktion  
 Sie können [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] auch verwenden, um eine eigene Tabellenwert-Wrapperfunktion zu schreiben, die die Change Data Capture-Abfragefunktion aufruft, und die Tabellenwert-Wrapperfunktion in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] speichern. Weitere Informationen zum Erstellen einer Transact-SQL-Funktion finden Sie unter [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md).  
  
 Das folgende Beispiel definiert eine Tabellenwertfunktion, mit der für das angegebene Änderungsintervall Änderungen von einer Customer-Tabelle abgerufen werden. Diese Funktion verwendet Change Data Capture-Funktionen, um die **datetime** -Werte den binären Protokollfolgenummer-Werten (Log Sequence Number, LSN) zuzuordnen, die die Änderungstabellen intern verwenden. Diese Funktion behandelt auch mehrere besondere Bedingungen:  
  
-   Wenn für die Startzeit ein NULL-Wert übergeben wird, verwendet diese Funktion den frühesten verfügbaren Wert.  
  
-   Wenn für die Beendigungszeit ein NULL-Wert übergeben wird, verwendet diese Funktion den letzten verfügbaren Wert.  
  
-   Wenn die Start-LSN mit der Beendigungs-LSN übereinstimmt, was in der Regel darauf hinweist, dass für das ausgewählte Intervall keine Datensätze vorliegen, wird diese Funktion beendet.  
  
### <a name="example-of-a-table-value-function-that-queries-for-change-data"></a>Beispiel einer Tabellenwert-Funktion, mit der Änderungsdaten abgefragt werden  
  
```  
CREATE function CDCSample.uf_Customer (  
     @start_time datetime  
    ,@end_time datetime  
)  
returns @Customer table (  
     CustomerID int  
    ,TerritoryID int  
    ,CustomerType nchar(1)  
    ,rowguid uniqueidentifier  
    ,ModifiedDate datetime  
    ,CDC_OPERATION varchar(1)  
) as  
begin  
    declare @from_lsn binary(10), @to_lsn binary(10)  
  
    if (@start_time is null)  
        select @from_lsn = sys.fn_cdc_get_min_lsn('Customer')  
    else  
        select @from_lsn = sys.fn_cdc_increment_lsn(sys.fn_cdc_map_time_to_lsn('largest less than or equal',@start_time))  
  
    if (@end_time is null)  
        select @to_lsn = sys.fn_cdc_get_max_lsn()  
    else  
        select @to_lsn = sys.fn_cdc_map_time_to_lsn('largest less than or equal',@end_time)  
  
    if (@from_lsn = sys.fn_cdc_increment_lsn(@to_lsn))  
        return  
  
    -- Query for change data  
    insert into @Customer  
    select   
        CustomerID,      
        TerritoryID,   
        CustomerType,   
        rowguid,   
        ModifiedDate,   
        case __$operation  
                when 1 then 'D'  
                when 2 then 'I'  
                when 4 then 'U'  
                else null  
         end as CDC_OPERATION  
    from   
        cdc.fn_cdc_get_net_changes_Customer(@from_lsn, @to_lsn, 'all')  
  
    return  
end   
go  
  
```  
  
### <a name="retrieving-additional-metadata-with-the-change-data"></a>Abrufen weiterer Metadaten mit den Änderungsdaten  
 Obwohl die zuvor gezeigte vom Benutzer erstellte Tabellenwert-Funktion nur die **__$operation**-Spalte verwendet, gibt die **cdc.fn_cdc_get_net_changes_<Aufzeichnungsinstanz>**-Funktion für jede Änderungszeile vier Metadatenspalten zurück. Wenn Sie diese Werte in Ihrem Datenfluss verwenden möchten, können Sie diese als zusätzliche Spalten aus der Tabellenwert-Wrapperfunktion zurückgeben.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**__$start_lsn**|**binary(10)**|LSN, die dem Commit für die Änderung zugeordnet wurde.<br /><br /> Alle Änderungen, für die ein Commit in derselben Transaktion ausgeführt wurde, verwenden dieselbe Commit-LSN. Wenn beispielsweise bei einem Updatevorgang in der Quelltabelle zwei unterschiedliche Zeilen geändert werden, enthält die Änderungstabelle vier Zeilen (zwei mit den alten Werten und zwei mit den neuen Werten), die jeweils denselben **__$start_lsn** -Wert aufweisen.|  
|**__$seqval**|**binary(10)**|Sequenzwert, mit dem Zeilenänderungen in einer Transaktion sortiert werden.|  
|**__$operation**|**int**|Der Vorgang der Datenbearbeitungssprache (Data Manipulation Language, DML), der der Änderung zugeordnet ist. Kann einen der folgenden Werte annehmen:<br /><br /> 1 = Löschen<br /><br /> 2 = Einfügen<br /><br /> 3 = Update (Werte vor dem Updatevorgang)<br /><br /> 4 = Update (Werte nach dem Updatevorgang)|  
|**__$update_mask**|**varbinary(128)**|Eine Bitmaske, die auf den Spaltenordnungszahlen der Änderungstabelle basiert, die geänderte Spalten identifiziert. Sie könnten diesen Wert überprüfen, wenn Sie bestimmen müssten, welche Spalten sich geändert haben.|  
|**\<erfasste Quelltabellenspalten>**|variiert|Bei den von der Funktion zurückgegebenen verbleibenden Spalten handelt es sich um die Spalten aus der Quelltabelle, die beim Erstellen der Aufzeichnungsinstanz als aufgezeichnete Spalten identifiziert wurden. Wenn in der Liste der aufgezeichneten Spalten ursprünglich keine Spalten angegeben wurden, werden alle Spalten in der Quelltabelle zurückgegeben.|  
  
 Weitere Informationen finden Sie unter [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md).  
  
## <a name="next-step"></a>Nächster Schritt  
 Nach dem Erstellen der Tabellenwertfunktion, mit der Änderungsdaten abgefragt werden, ist der nächste Schritt der Entwurf des Datenflusses im Paket.  
  
 **Nächstes Thema**[Abrufen und Verstehen der Änderungsdaten](../../integration-services/change-data-capture/retrieve-and-understand-the-change-data.md)  
  
  

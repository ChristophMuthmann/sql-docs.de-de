---
title: Sys.fn_net_changes_&lt;Capture_instance&gt; (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server (starting with 2008)
f1_keywords:
- sys.fn_net_changes_TSQL
- fn_net_changes_TSQL
- fn_net_changes
- sys.fn_net_changes
dev_langs:
- TSQL
helpviewer_keywords:
- fn_net_changes_<capture_instance>
- sys.fn_net_changes_<capture_instance>
ms.assetid: 342fa030-9fd9-4b74-ae4d-49f6038a5073
caps.latest.revision: 
author: BYHAM
ms.author: rickbyh
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a822cb52d98fec1e0d531c09fa3d138d07757cb8
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysfnnetchangesltcaptureinstancegt-transact-sql"></a>Sys.fn_net_changes_&lt;Capture_instance&gt; (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Wrapper für die **net Changes** Abfragefunktionen. Die zum Erstellen dieser Funktionen erforderlichen Skripts werden von der gespeicherten Prozedur sys.sp_cdc_generate_wrapper_function generiert.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
fn_net_changes_<capture_instance> ('start_time', 'end_time', '<row_filter_option>' )  
  
<capture_instance> ::= The name of the capture instance.  
<row_filter_option> ::=  
{ all  
  | all with mask  
  | all with merge  
}  
```  
  
## <a name="arguments"></a>Argumente  
 *start_time*  
 Die **"DateTime"** Wert, der den unteren Endpunkt des Bereichs der Einträge aus der Änderungstabelle in das Resultset eingeschlossen werden sollen.  
  
 Nur Zeilen in der cdc. < Aufzeichnungsinstanz > _CT Änderungstabelle, die eine zugeordnete Commitzeit unbedingt größer als *Start_time* im Resultset enthalten sind.  
  
 Wenn für dieses Argument ein Wert von NULL übergeben wird, entspricht der untere Endpunkt des Abfragebereichs dem unteren Endpunkt des gültigen Bereichs der Aufzeichnungsinstanz.  
  
 *end_time*  
 Die **"DateTime"** Wert, der den oberen Endpunkt des Bereichs der Einträge aus der Änderungstabelle in das Resultset eingeschlossen werden sollen.  
  
 Dieser Parameter kann eine oder zwei Bedeutungen, abhängig vom Wert für die ausgewählten annehmen @closed_high_end_point Wenn Sys. sp_cdc_generate_wrapper_function aufgerufen wird, um das Skript zur Erstellung der Wrapperfunktion zu generieren:  
  
-   @closed_high_end_point = 1  
  
     Nur Zeilen in der cdc. < Aufzeichnungsinstanz > _CT, die einen Wert Änderungstabelle in \_ \_$Start_lsn und eine entsprechende Commitzeit Mal kleiner als oder gleich **Start_time** im Resultset enthalten sind.  
  
-   @closed_high_end_point = 0  
  
     Nur Zeilen in der cdc. < Aufzeichnungsinstanz > _CT, die einen Wert Änderungstabelle in \_ \_$Start_lsn und eine entsprechende Commitzeit unbedingt kleiner als **Start_time** im Resultset enthalten sind.  
  
 Wenn für dieses Argument ein Wert von NULL übergeben wird, entspricht der obere Endpunkt des Abfragebereichs dem oberen Endpunkt des gültigen Bereichs der Aufzeichnungsinstanz.  
  
 *<row_filter_option>* ::= { all | all with mask | all with merge }  
 Eine Option, die den Inhalt der Metadatenspalten sowie die im Resultset zurückgegebenen Zeilen bestimmt. Eine der folgenden Optionen ist möglich:  
  
 all  
 Gibt den endgültigen Inhalt einer geänderten Zeile in den Inhaltsspalten zurück sowie den erforderlichen Vorgang zum Anwenden der Zeile in der Metadatenspalte __CDC_OPERATION.  
  
 all with mask  
 Gibt den endgültigen Inhalt einer geänderten Zeile in den Inhaltsspalten zurück sowie den erforderlichen Vorgang zum Anwenden der einzelnen Zeilen in der Metadatenspalte __CDC_OPERATION. Wenn bei Generierung des Skripts zur Erstellung der Wrapperfunktion eine Aktualisierungsflagliste angegeben wurde, müssen Sie mit dieser Option die Aktualisierungsmaske füllen.  
  
 all with merge  
 Gibt den endgültigen Inhalt aller in den Inhaltsspalten geänderten Zeilen zurück.  
  
 Die Spalte __CDC_OPERATION wird einer der beiden folgenden Werte sein:  
  
-   D, wenn die Zeile gelöscht werden muss  
  
-   M, wenn die Zeile eingefügt oder aktualisiert werden muss  
  
 Die Logik zum Bestimmen, ob eine Einfügung oder eine Aktualisierung erforderlich ist, um eine Änderung auf ein Ziel anzuwenden, führt zu mehr Komplexität bei der Abfrage. Verwenden Sie diese Option für verbesserte Leistung, wenn nicht zwischen Einfügungs- und Aktualisierungsvorgängen unterschieden werden muss. Dieser Ansatz eignet sich besonders für Zielumgebungen, in denen Mergevorgänge direkt verfügbar sind, z. B. in einer [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]-Umgebung.  
  
## <a name="table-returned"></a>Zurückgegebene Tabelle  
  
|Spaltenname|Spaltentyp|Description|  
|-----------------|-----------------|-----------------|  
|\<Spalten aus @column_list>|**varies**|Die Spalten, die im identifiziert werden die **Column_list** Argument an die Sp_cdc_generate_wrapper_function, wenn sie aufgerufen wird, um das Skript zur Erstellung des Wrappers zu generieren. Wenn *Column_list* NULL ist, alle verfolgten Quellspalten werden im Resultset angezeigt.|  
|__CDC_OPERATION|**nvarchar(2)**|Ein Vorgangscode, der angibt, welcher Vorgang auf die Zeile der Zielumgebung angewendet werden muss. Der Vorgang ist variiert basierend auf den Wert des Arguments *Row_filter_option* , die im folgenden Aufruf angegeben wird:<br /><br /> *Row_filter_option* = 'all', 'all with Mask'<br /><br /> 'D' - Löschvorgang<br /><br /> 'I' - Einfügevorgang<br /><br /> 'UN' - Aktualisierungsvorgang<br /><br /> *Row_filter_option* = 'all with Merge'<br /><br /> 'D' - Löschvorgang<br /><br /> 'M' - Einfüge- oder Aktualisierungsvorgang|  
|\<Spalten aus @update_flag_list>|**bit**|Ein Bitflag, das durch Anfügen von _uflag an den Spaltennamen benannt wird. Ein Wert ungleich NULL das Flag nimmt nur, wenn *Row_filter_option* **= 'all with Mask'** und \__CDC_OPERATION **= un '**. Es wird auf 1 eingestellt, wenn die entsprechende Spalte innerhalb des Abfragefensters geändert wurde. Andernfalls ist es 0.|  
  
## <a name="remarks"></a>Hinweise  
 Die Funktion "fn_net_changes_" < Capture_instance > dient als Wrapper für die Abfragefunktion CDC. fn_cdc_get_net_changes_ < Capture_instance >. Die sp_cdc_generate_wrapper gespeicherte Prozedur dient zum Erstellen des Skripts für den Wrapper.  
  
 Wrapperfunktionen werden nicht automatisch erstellt. Es gibt zwei Dinge, die Sie ausführen müssen, um Wrapperfunktionen zu erstellen:  
  
1.  Führen Sie die gespeicherte Prozedur aus, um das Skript zu generieren, das den Wrapper erstellt.  
  
2.  Führen Sie das Skript aus, das die Wrapperfunktion tatsächlich erstellt.  
  
 Wrapperfunktionen ermöglichen es Benutzern, systematisch Änderungen abzufragen, die innerhalb einer begrenzten Intervalls aufgetreten **"DateTime"** Werte anstelle von LSN-Werte. Die Wrapperfunktionen führen alle erforderlichen Konvertierungen zwischen den bereitgestellten **"DateTime"** Werte und die LSN-Werte, die intern als Argumente für die Abfragefunktionen benötigt. Wenn die Wrapperfunktionen seriell zum Verarbeiten eines Datenstroms von Änderungsdaten verwendet werden, wird sichergestellt, dass keine Daten verloren gehen oder wiederholt werden, vorausgesetzt, dass die folgende Konvention eingehalten wird: der @end_time Wert des einem Aufruf zugeordneten Intervalls wird als die angegeben@start_time Wert für die nachfolgenden Aufruf zugeordneten Intervalls.  
  
 Wenn Sie den Parameter @closed_high_end_point bei Erstellung des Skripts verwenden, können Sie Wrapper generieren, die im angegebenen Abfragefenster eine geschlossene obere Grenze oder eine offene untere Grenze unterstützen. Sie können also entscheiden, ob Einträge mit einer Commitzeit in das Intervall aufgenommen werden sollen, die der oberen Grenze des Extrahierungsintervalls entspricht. Standardmäßig wird die Obergrenze aufgenommen.  
  
 Das Resultset zurückgegeben, durch die **net Changes** Wrapper-Funktion gibt nur die verfolgten Spalten, die sich die @column_list Wenn der Wrapper generiert wurde. Wenn @column_list NULL ist, werden alle verfolgten Quellspalten zurückgegeben. Den Quellspalten folgt die Vorgangspalte, __CDC_OPERATION. Es handelt sich um eine Spalte mit einem oder zwei Zeichen, die den Vorgang identifiziert.  
  
 Bitflags werden dann dem Resultset für jede Spalte, die im Parameters identifiziert wird angehängt @update_flag_list. Für die **net Changes** Wrapper sind die Bitflags immer NULL sein, wenn die @row_filter_option also im Aufruf der Wrapperfunktion verwendete 'all' oder 'all with Merge' ist. Der Wert des Flags ist ebenfalls NULL, wenn die @row_filter_option auf 'all with mask' und __CDC_OPERATION auf 'D' oder 'I' gesetzt ist. Wenn \__CDC_OPERATION ist un ", das Flag wird festgelegt auf 1 oder 0 gesetzt, je nachdem, ob die **net** Aktualisierungsvorgang aufgrund eine Änderung der Spalte.  
  
 Die Change Data Capture-Konfigurationsvorlage 'Instantiate CDC Wrapper TVFs for Schema' veranschaulicht die Verwendung der gespeicherten Prozedur sp_cdc_generate_wrapper_function zum Abrufen von CREATE-Skripts für alle Wrapperfunktionen für die definierten Abfragefunktionen eines Schemas. Diese Skripts werden dann von der Vorlage erstellt. Weitere Informationen zu Vorlagen finden Sie unter [Vorlagen-Explorer](http://msdn.microsoft.com/library/b9ee55c5-bb44-4f76-90ac-792d8d83b4c8).  
  
## <a name="see-also"></a>Siehe auch  
 [sys.sp_cdc_generate_wrapper_function &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md)   
 [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)  
  
  

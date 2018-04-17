---
title: Sys.fn_all_changes_&lt;Capture_instance&gt; (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server (starting with 2008)
f1_keywords:
- fn_all_changes
- sys.fn_all_changes
- fn_all_changes_TSQL
- sys.fn_all_changes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_all_changes_<capture_instance>
- sys.fn_all_changes_<capture_instance>
ms.assetid: 564fae96-b88c-4f22-9338-26ec168ba6f5
caps.latest.revision: 15
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c86286a8412f41dbc8c30bc5bcd68489aa27f99e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysfnallchangesltcaptureinstancegt-transact-sql"></a>Sys.fn_all_changes_&lt;Capture_instance&gt; (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Wrapper für die **alle Änderungen** Abfragefunktionen. Die zum Erstellen dieser Funktionen erforderlichen Skripts werden von der gespeicherten Prozedur sys.sp_cdc_generate_wrapper_function generiert.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
fn_all_changes_<capture_instance> ('start_time' ,'end_time', '<row_filter_option>' )  
  
<capture_instance> ::= The name of the capture instance.  
<row_filter_option> ::=  
{ all  
  | all update old  
}  
```  
  
## <a name="arguments"></a>Argumente  
 *start_time*  
 Die **"DateTime"** Wert, der den unteren Endpunkt des Bereichs der Einträge aus der Änderungstabelle in das Resultset eingeschlossen werden sollen.  
  
 Nur Zeilen in der cdc. < Aufzeichnungsinstanz > _CT Änderungstabelle, die eine zugeordnete Commitzeit größer als *Start_time* im Resultset enthalten sind.  
  
 Wenn für dieses Argument ein Wert von NULL übergeben wird, entspricht der untere Endpunkt des Abfragebereichs dem unteren Endpunkt des gültigen Bereichs der Aufzeichnungsinstanz.  
  
 *end_time*  
 Die **"DateTime"** Wert, der den oberen Endpunkt des Bereichs der Einträge aus der Änderungstabelle in das Resultset eingeschlossen werden sollen.  
  
 Dieser Parameter kann eine oder zwei Bedeutungen je nach dem Wert für die ausgewählten annehmen @closed_high_end_point Wenn Sys. sp_cdc_generate_wrapper_function aufgerufen wird, um das Skript für die Wrapperfunktion zu generieren:  
  
-   @closed_high_end_point = 1  
  
     Nur Zeilen in der Änderungstabelle cdc.<Aufzeichnungsinstanz>_CT, denen eine Commitzeit früher als oder gleich end_time zugeordnet ist, werden in das Resultset aufgenommen.  
  
-   @closed_high_end_point = 0  
  
     Ausschließlich Zeilen in der Änderungstabelle cdc.Aufzeichnungsinstanz_CT, denen eine Commitzeit früher als end_time zugeordnet ist, werden in das Resultset aufgenommen.  
  
 Wenn für dieses Argument ein Wert von NULL übergeben wird, entspricht der obere Endpunkt des Abfragebereichs dem oberen Endpunkt des gültigen Bereichs der Aufzeichnungsinstanz.  
  
 <row_filter_option> ::= { all | all update old }  
 Eine Option, die den Inhalt der Metadatenspalten sowie die im Resultset zurückgegebenen Zeilen bestimmt.  
  
 Eine der folgenden Optionen ist möglich:  
  
 all  
 Gibt alle Änderungen innerhalb des angegebenen LSN-Bereichs zurück. Bei Änderungen aufgrund eines Updatevorgangs gibt diese Option nur die Zeile zurück, die die neuen Werte nach Anwendung des Updates enthält.  
  
 all update old  
 Gibt alle Änderungen innerhalb des angegebenen LSN-Bereichs zurück. Bei Änderungen aufgrund eines Updatevorgangs gibt die Option die beiden Zeilen zurück, die die Spaltenwerte vor und nach dem Update enthalten.  
  
## <a name="table-returned"></a>Zurückgegebene Tabelle  
  
|Spaltenname|Spaltentyp|Description|  
|-----------------|-----------------|-----------------|  
|__CDC_STARTLSN|**binary(10)**|Die Commit-LSN der Transaktion, die der Änderung zugeordnet ist. Alle Änderungen, die in der gleichen Transaktion ein Commit ausgeführt werden, verwenden dieselbe Commit-LSN.|  
|__CDC_SEQVAL|**binary(10)**|Sequenzwert, mit dem Zeilenänderungen in einer Transaktion sortiert werden.|  
|\<Spalten aus @column_list>|**Variiert**|Die Spalten, die im identifiziert werden die *Column_list* Argument für sp_cdc_generate_wrapper_function angegebenen, wenn sie aufgerufen wird, um das Skript zu generieren, die Wrapperfunktion erstellt.|  
|__CDC_OPERATION|**nvarchar(2)**|Ein Vorgangscode, der den Vorgang angibt, der zum Anwenden der Zeile auf die Zielumgebung erforderlich ist. Sie richten sich nach dem Wert des Arguments *Row_filter_option* im Aufruf angegebenen:<br /><br /> *Row_filter_option* = 'all'<br /><br /> 'D' - Löschvorgang<br /><br /> 'I' - Einfügevorgang<br /><br /> 'UN' - Updatevorgang, neue Werte<br /><br /> *Row_filter_option* = 'all update old'<br /><br /> 'D' - Löschvorgang<br /><br /> 'I' - Einfügevorgang<br /><br /> 'UN' - Updatevorgang, neue Werte<br /><br /> 'UO' - Updatevorgang, alte Werte|  
|\<Spalten aus @update_flag_list>|**bit**|Ein Bitflag, das durch Anfügen von _uflag an den Spaltennamen benannt wird. Das Flag ist immer auf NULL, wenn festgelegt \__CDC_OPERATION d ', 'I' oder 'uo'. Wenn \__CDC_OPERATION ist un ', es wird auf 1 festgelegt, wenn das Update eine Änderung an der entsprechenden Spalte erzeugt. Andernfalls ist es 0.|  
  
## <a name="remarks"></a>Hinweise  
 Die Funktion fn_all_changes_<Aufzeichnungsinstanz> wird als Wrapper für die Abfragefunktion cdc.fn_cdc_get_all_changes_<Aufzeichnungsinstanz> verwendet. Die gespeicherte Prozedur sys.sp_cdc_generate_wrapper wird zum Generieren des Skripts zum Erstellen des Wrappers verwendet.  
  
 Wrapperfunktionen werden nicht automatisch erstellt. Es gibt zwei Dinge, die Sie ausführen müssen, um Wrapperfunktionen zu erstellen:  
  
1.  Führen Sie die gespeicherte Prozedur aus, um das Skript zu generieren, das den Wrapper erstellt.  
  
2.  Führen Sie das Skript aus, das die Wrapperfunktion tatsächlich erstellt.  
  
 Wrapperfunktionen ermöglichen es Benutzern, systematisch Änderungen abzufragen, die innerhalb einer begrenzten Intervalls aufgetreten **"DateTime"** Werte anstelle von LSN-Werte. Die Wrapperfunktionen führen alle erforderlichen Konvertierungen zwischen den bereitgestellten **"DateTime"** Werte und die LSN-Werte, die intern als Argumente für die Abfragefunktionen benötigt. Wenn die Wrapperfunktionen seriell zum Verarbeiten eines Datenstroms von Änderungsdaten verwendet werden, wird sichergestellt, dass keine Daten verloren gehen oder wiederholt werden, vorausgesetzt, dass die folgende Konvention eingehalten wird: der @end_time Wert des einem Aufruf zugeordneten Intervalls wird als die angegeben@start_time Wert für die nachfolgenden Aufruf zugeordneten Intervalls.  
  
 Wenn Sie den Parameter @closed_high_end_point bei Erstellung des Skripts verwenden, können Sie Wrapper generieren, die im angegebenen Abfragefenster eine geschlossene obere Grenze oder eine offene untere Grenze unterstützen. Sie können also entscheiden, ob Einträge mit einer Commitzeit in das Intervall aufgenommen werden sollen, die der oberen Grenze des Extrahierungsintervalls entspricht. Standardmäßig wird die Obergrenze aufgenommen.  
  
 Das Resultset zurückgegeben, durch die **alle Änderungen** Wrapperfunktion gibt die __ $Start_lsn und \_ \_$seqval-Spalte der Änderungstabelle als Spalte \__CDC_STARTLSN und \__ CDC_SEQVAL, bzw. Es folgen nur die verfolgten Spalten, die in angezeigt wurden die *@column_list* -Parameter, wenn der Wrapper generiert wurde. Wenn *@column_list* NULL ist, alle verfolgten Quellspalten zurückgegeben. Die Quellspalten gefolgt von einer vorgangspalte \__CDC_OPERATION, also eine Spalte mit einem oder zwei Zeichen, die den Vorgang identifiziert.  
  
 Bitflags werden dann dem Resultset für die einzelnen Spalten angehängt, die im Parameter @update_flag_list identifiziert sind. Für die **alle Änderungen** Wrapper sind die Bitflags werden immer NULL sein, wenn __cdc_operation hatte ', 'I' oder 'UO'. Wenn \__CDC_OPERATION ist un ", das Flag wird festgelegt auf 1 oder 0 gesetzt, je nachdem, ob der Updatevorgang eine Änderung der Spalte geführt hat.  
  
 Die Change Data Capture-Konfigurationsvorlage 'Instantiate CDC Wrapper TVFs for Schema' veranschaulicht die Verwendung der gespeicherten Prozedur sp_cdc_generate_wrapper_function zum Abrufen von CREATE-Skripts für alle Wrapperfunktionen für die definierten Abfragefunktionen eines Schemas. Diese Skripts werden dann von der Vorlage erstellt. Weitere Informationen zu Vorlagen finden Sie unter [Vorlagen-Explorer](http://msdn.microsoft.com/library/b9ee55c5-bb44-4f76-90ac-792d8d83b4c8).  
  
## <a name="see-also"></a>Siehe auch  
 [sys.sp_cdc_generate_wrapper_function &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)  
  
  

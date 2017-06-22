---
title: Anzeigen und Lesen des Failoverclusterinstanz-Diagnoseprotokolls | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 68074bd5-be9d-4487-a320-5b51ef8e2b2d
caps.latest.revision: 23
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 912c05cd783ead67aaa506f07586387eabcb2ca4
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="view-and-read-failover-cluster-instance-diagnostics-log"></a>Anzeigen und Lesen des Failoverclusterinstanz-Diagnoseprotokolls
  Alle kritischen Fehler und Warnungsereignisse für die Ressourcen-DLL von SQL Server werden in das Windows-Ereignisprotokoll geschrieben. Ein Ausführungsprotokoll mit für SQL Server spezifischen Diagnoseinformationen wird von der gespeicherten Systemprozedur [sp_server_diagnostics &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) erfasst und in die Protokolldateien der SQL Server-Failoverclusterdiagnose (auch als *SQLDIAG*-Protokolle bezeichnet) geschrieben.  
  
-   **Before you begin:**  [Recommendations](#Recommendations), [Security](#Security)  
  
-   **To View the Diagnostic Log, using:**  [SQL Server Management Studio](#SSMSProcedure), [Transact-SQL](#TsqlProcedure)  
  
-   **To Configure Diagnostic Log settings, using:** [Transact-SQL](#TsqlConfigure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Recommendations"></a> Empfehlungen  
 Die SQLDIAG-Protokolle werden standardmäßig in einem lokalen LOG-Ordner des Verzeichnisses der SQL Server-Instanz gespeichert, z.B. in „C\Programme\Microsoft SQL Server\MSSQL13.\<Instanzname>\MSSQL\LOG“ für den besitzenden Knoten der Always On-Failoverclusterinstanz (FCI). Die Größe jeder SQLDIAG-Protokolldatei wird auf 100 MB begrenzt. Zehn dieser Protokolldateien werden auf dem Computer gespeichert, bevor sie für neue Protokolle wiederverwendet werden.  
  
 Die Protokolle verwenden das Dateiformat für erweiterte Ereignisse. Mit der Systemfunktion **sys.fn_xe_file_target_read_file** können Sie die Dateien lesen, die durch erweiterte Ereignisse erstellt wurden. Pro Zeile wird ein Ereignis im XML-Format zurückgegeben. Fragen Sie die Systemsicht ab, um die XML-Daten als Resultset zu analysieren. Weitere Informationen finden Sie unter [sys.fn_xe_file_target_read_file &#40;Transact-SQL&#41;](../../../relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql.md).  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Die VIEW SERVER STATE-Berechtigung ist erforderlich, um **fn_xe_file_target_read_file**auszuführen.  
  
 Öffnen von SQL Server Management Studio als Administrator  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 **So zeigen Sie die Diagnoseprotokolldateien an:**  
  
1.  Wählen Sie im Menü **Datei** die Option **Öffnen**, **Datei**, und wählen Sie die anzuzeigende Diagnoseprotokolldatei an.  
  
2.  Die Ereignisse werden als Zeilen im rechten Bereich angezeigt. Standardmäßig werden nur die Spalten **name**und **timestamp** angezeigt.  
  
     Dadurch wird außerdem das Menü **ExtendedEvents** aktiviert.  
  
3.  Rufen Sie zum Anzeigen weiterer Spalten das Menü **ExtendedEvents** auf, und wählen Sie **Spalten auswählen**.  
  
     Ein Dialogfeld mit den verfügbaren Spalten wird angezeigt, in dem Sie die anzuzeigenden Spalten auswählen können.  
  
4.  Sie können die Ereignisdaten mithilfe des Menüs **ExtendedEvents** und der Option **Filter** filtern und sortieren.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 **So zeigen Sie die Diagnoseprotokolldateien an:**  
  
 Um alle Protokollelemente in der SQLDIAG-Protokolldatei anzuzeigen, verwenden Sie die folgende Abfrage:  
  
```  
SELECT  
xml_data.value('(event/@name)[1]','varchar(max)') AS 'Name'  
,xml_data.value('(event/@package)[1]','varchar(max)') AS 'Package'  
,xml_data.value('(event/@timestamp)[1]','datetime') AS 'Time'  
,xml_data.value('(event/data[@name=''state'']/value)[1]','int') AS 'State'  
,xml_data.value('(event/data[@name=''state_desc'']/text)[1]','varchar(max)') AS 'State Description'  
,xml_data.value('(event/data[@name=''failure_condition_level'']/value)[1]','int') AS 'Failure Conditions'  
,xml_data.value('(event/data[@name=''node_name'']/value)[1]','varchar(max)') AS 'Node_Name'  
,xml_data.value('(event/data[@name=''instancename'']/value)[1]','varchar(max)') AS 'Instance Name'  
,xml_data.value('(event/data[@name=''creation time'']/value)[1]','datetime') AS 'Creation Time'  
,xml_data.value('(event/data[@name=''component'']/value)[1]','varchar(max)') AS 'Component'  
,xml_data.value('(event/data[@name=''data'']/value)[1]','varchar(max)') AS 'Data'  
,xml_data.value('(event/data[@name=''info'']/value)[1]','varchar(max)') AS 'Info'  
FROM  
 ( SELECT object_name AS 'event'  
  ,CONVERT(xml,event_data) AS 'xml_data'  
  FROM sys.fn_xe_file_target_read_file('C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Log\SQLNODE1_MSSQLSERVER_SQLDIAG_0_129936003752530000.xel',NULL,NULL,NULL)   
)   
AS XEventData  
ORDER BY Time;  
  
```  
  
> [!NOTE]  
>  Sie können die Ergebnisse nach bestimmten Komponenten oder Status filtern, indem Sie die WHERE-Klausel verwenden.  
  
##  <a name="TsqlConfigure"></a> Verwenden von Transact-SQL  
 **So konfigurieren Sie die Diagnoseprotokolleigenschaften**  
  
> [!NOTE]  
>  Ein Beispiel für diese Prozedur finden Sie weiter unten in diesem Abschnitt unter [Beispiel (Transact-SQL)](#TsqlExample).  
  
 Mithilfe der DDL-Anweisung (Data Definition Language) **ALTER SERVER CONFIGURATION** können Sie die Protokollierung von Diagnosedaten, die von der Prozedur [sp_server_diagnostics &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) erfasst wurden, starten bzw. beenden und SQLDIAG-Protokollkonfigurationsparameter festlegen, wie z.B. die Anzahl der Protokolldateirollover, die Protokolldateigröße und den Dateispeicherort. Einzelheiten zur Syntax finden Sie unter [Setting diagnostic log options](../../../t-sql/statements/alter-server-configuration-transact-sql.md#Diagnostic).  
  
###  <a name="ConfigTsqlExample"></a> Beispiele (Transact-SQL)  
  
####  <a name="TsqlExample"></a> Setting diagnostic log options  
 Die Beispiele in diesem Abschnitt veranschaulichen, wie die Werte für die Diagnoseprotokolloption festgelegt werden.  
  
##### <a name="a-starting-diagnostic-logging"></a>A. Starten der Diagnoseprotokollierung  
 Im folgenden Beispiel wird die Protokollierung von Diagnosedaten gestartet.  
  
```  
ALTER SERVER CONFIGURATION SET DIAGNOSTICS LOG ON;  
```  
  
##### <a name="b-stopping-diagnostic-logging"></a>B. Beenden der Diagnoseprotokollierung  
 Im folgenden Beispiel wird die Protokollierung von Diagnosedaten beendet.  
  
```  
ALTER SERVER CONFIGURATION SET DIAGNOSTICS LOG OFF;  
```  
  
##### <a name="c-specifying-the-location-of-the-diagnostic-logs"></a>C. Angeben des Speicherorts für die Diagnoseprotokolle  
 Im folgenden Beispiel wird der Speicherort für die Diagnoseprotokolle auf den angegebenen Dateipfad festgelegt.  
  
```  
ALTER SERVER CONFIGURATION  
SET DIAGNOSTICS LOG PATH = 'C:\logs';  
```  
  
##### <a name="d-specifying-the-maximum-size-of-each-diagnostic-log"></a>D. Angeben der maximalen Größe jedes Diagnoseprotokolls  
 Im folgenden Beispiel wird die maximale Größe jedes Diagnoseprotokolls auf 10 Megabytes festgelegt.  
  
```  
ALTER SERVER CONFIGURATION   
SET DIAGNOSTICS LOG MAX_SIZE = 10 MB;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Failoverrichtlinie für Failoverclusterinstanzen](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)  
  
  

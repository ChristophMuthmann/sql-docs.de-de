---
title: Erstellen des DIAGNOSESITZUNG (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 662d019e-f217-49df-9e2f-b5662fa0342d
caps.latest.revision: "9"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d869ed18b07f824ffa4cc3fc8b746ded5242ed99
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="create-diagnostics-session-transact-sql"></a>CREATE DIAGNOSTICS SESSION (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Diagnosesitzungen können Sie auf die Leistung von System- oder Abfrage ausführlicher und benutzerdefinierte Diagnoseinformationen zu speichern.  
  
 Diagnosesitzungen werden normalerweise verwendet, um Leistung für eine bestimmte Abfrage zu debuggen, oder das Verhalten einer bestimmten Anwendung Komponente während Appliance-Vorgangs zu überwachen.  
  
> [!NOTE]  
>  Sie sollten mit XML vertraut sein, um diagnosesitzungen verwenden.  
  
## <a name="syntax"></a>Syntax  
  
```  
Creating a new diagnostics session:  
CREATE DIAGNOSTICS SESSION diagnostics_name AS N’{<session_xml>}’;  
  
<session_xml>::  
<Session>  
   [ <MaxItemCount>max_item_count_num</MaxItemCount> ]  
   <Filter>  
      { \<Event Name=”event_name”/>  
         [ <Where>\<filter_property_name Name=”value” ComparisonType="comp_type"/></Where> ] [ ,...n ]  
      } [ ,...n ]  
   </Filter> ]   
   <Capture>  
      \<Property Name=”property_name”/> [ ,...n ]  
   </Capture>  
<Session>  
  
Retrieving results for a diagnostics session:  
SELECT * FROM master.sysdiag.diagnostics_name ;  
  
Removing results for a diagnostics session:  
DROP DIAGNOSTICS SESSION diagnostics_name ;  
```  
  
## <a name="arguments"></a>Argumente  
 *diagnostics_name*  
 Der Name des Diagnostics-Sitzung. Diagnose Sitzungsnamen zählen die Zeichen a-Z, A-Z und 0-9. Darüber hinaus müssen Diagnose Sitzungsnamen mit einem Zeichen beginnen. *Diagnostics_name* ist auf 127 Zeichen begrenzt.  
  
 *max_item_count_num*  
 Die Anzahl der Ereignisse in einer Ansicht beibehalten werden. Z. B. werden 100 angegeben wird, die 100 letzten Ereignisse, die den Filterkriterien entsprechen. um die diagnosesitzung beibehalten werden. Wenn weniger als 100 Ereignisse Übereinstimmung gefunden werden, wird die diagnosesitzung weniger als 100 Ereignisse enthalten. *Max_item_count_num* muss mindestens 100 und kleiner oder gleich 100.000.  
  
 *event_name*  
 Definiert die tatsächliche Ereignisse in der diagnosesitzung gesammelt werden sollen.  *Ereignisname* ist eines der Ereignisse aufgeführt, die [sys.pdw_diag_events](http://msdn.microsoft.com/en-us/d813aac0-cea1-4f53-b8e8-d26824bc2587) , in denen `sys.pdw_diag_events.is_enabled='True'`.  
  
 *filter_property_name*  
 Der Name der Eigenschaft für die Ergebnisse zu beschränken. Wenn Sie einschränken möchten, basierend auf der Sitzungs-Id, z. B. *Filter_property_name* muss *SessionId*. Finden Sie unter *Property_name* unten eine Liste der möglichen Werte für *Filter_property_name*.  
  
 *value*  
 Ein Wert für die auszuwertende gegen *Filter_property_name*. Der Werttyp muss den Eigenschaftentyp überein. Beispielsweise ist der Eigenschaftentyp decimal, den Typ des *Wert* decimal werden muss.  
  
 *comp_type*  
 Der Vergleichstyp. Mögliche Werte sind: ist gleich, EqualsOrGreaterThan, EqualsOrLessThan, "GreaterThan", "LessThan", ungleich, Contains, RegEx  
  
 *property_name*  
 Eine Eigenschaft mit dem Ereignis verknüpft wird.  Eigenschaftsnamen können Teil der Capture-Tag sein oder als Teil der Filterkriterien verwendet.  
  
|Eigenschaftsname|Description|  
|-------------------|-----------------|  
|UserName|Ein Name für Benutzer (Anmeldenamen).|  
|SessionID|Eine Sitzungs-ID.|  
|QueryId|Eine Abfrage-ID.|  
|CommandType|Einen Befehlstyp.|  
|CommandText|Text in einen Befehl verarbeitet.|  
|OperationType|Der Vorgangstyp für das Ereignis.|  
|Dauer|Die Dauer des Ereignisses.|  
|SPID|Die Dienst-Prozess-ID|  
  
## <a name="remarks"></a>Hinweise  
 Jeder Benutzer darf maximal 10 gleichzeitige diagnosesitzungen. Finden Sie unter [sys.pdw_diag_sessions](http://msdn.microsoft.com/en-us/ca111ddc-2787-4205-baf0-1a242c0257a9) eine Liste der aktuellen Sitzungen und Drop Sitzungen, die Sie nicht benötigte `DROP DIAGNOSTICS SESSION`.  
  
 Diagnosesitzungen weiterhin Metadaten bis gelöscht zu sammeln.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die **ALTER SERVER STATE** Berechtigung.  
  
## <a name="locking"></a>Sperren  
 Akzeptiert eine gemeinsame Sperre für die Tabelle Diagnosesitzungen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-a-diagnostics-session"></a>A. Erstellen eine diagnosesitzung  
 Dieses Beispiel erstellt ein diagnosesitzung zum Aufzeichnen von Metriken, die von der Leistung des Datenbankmoduls. Das Beispiel erstellt eine diagnosesitzung, der Datenbankmodul-Abfrage wird ausgeführt/End-Ereignisse und ein blockierendes DMS-Ereignis überwacht. Was zurückgegeben wird, wird der Befehlstext, Computername, Anforderungs-Id (Abfrage-Id) und die Sitzung, der das Ereignis erstellt wurde.  
  
```  
CREATE DIAGNOSTICS SESSION MYDIAGSESSION AS N'  
<Session>  
   <MaxItemCount>100</MaxItemCount>  
   <Filter>  
      <Event Name="EngineInstrumentation:EngineQueryRunningEvent" />  
      <Event Name="DmsCoreInstrumentation:DmsBlockingQueueEnqueueBeginEvent" />  
      <Where>  
         <SessionId Value="381" ComparisonType="NotEquals" />  
      </Where>  
   </Filter>  
   <Capture>  
      <Property Name="Query.CommandText" />  
      <Property Name="MachineName" />  
      <Property Name="Query.QueryId" />  
      <Property Name="Alias" />  
      <Property Name="Duration" />  
      <Property Name="Session.SessionId" />  
   </Capture>  
</Session>';  
```  
  
 Führen Sie eine Abfrage nach der Erstellung der diagnosesitzung.  
  
```  
SELECT COUNT(EmployeeKey) FROM AdventureWorksPDW2012..FactSalesQuota;  
```  
  
 Zeigen Sie dann die Diagnoseergebnisse für die Sitzung durch Auswahl aus dem Schema Sysdiag an.  
  
```  
SELECT * FROM master.sysdiag.MYDIAGSESSION;  
```  
  
 Beachten Sie, dass das Schema Sysdiag eine Sicht enthält, mit dem Namen der Diagnose-Sitzungsname.  
  
 Um nur die Aktivität für die Verbindung angezeigt wird, fügen die `Session.SPID` Eigenschaft und fügen `WHERE [Session.SPID] = @@spid;` der Abfrage.  
  
 Wenn Sie mit der diagnosesitzung fertig sind, legen Sie mithilfe der **löschen Diagnose** Befehl.  
  
```  
DROP DIAGNOSTICS SESSION MYDIAGSESSION;  
```  
  
### <a name="b-alternative-diagnostic-session"></a>B. Alternative diagnosesitzung  
 Ein zweites Beispiel mit etwas andere Eigenschaften.  
  
```  
-- Determine the session_id of your current session  
SELECT TOP 1 session_id();  
-- Replace \<*session_number*> in the code below with the numbers in your session_id  
CREATE DIAGNOSTICS SESSION PdwOptimizationDiagnostics AS N'  
<Session>  
   <MaxItemCount>100</MaxItemCount>  
   <Filter>  
      <Event Name="EngineInstrumentation:MemoGenerationBeginEvent" />  
      <Event Name="EngineInstrumentation:MemoGenerationEndEvent" />  
      <Event Name="DSQLInstrumentation:OptimizationBeginEvent" />  
      <Event Name="DSQLInstrumentation:OptimizationEndEvent" />  
      <Event Name="DSQLInstrumentation:BuildRelOpContextTreeBeginEvent" />  
      <Event Name="DSQLInstrumentation:PostPlanGenModifiersEndEvent" />  
      <Where>  
         <SessionId Value="\<*session_number*>" ComparisonType="Equals" />  
      </Where>  
   </Filter>  
   <Capture>  
      <Property Name="Session.SessionId" />  
      <Property Name="Query.QueryId" />  
      <Property Name="Query.CommandText" />  
      <Property Name="Name" />  
      <Property Name="DateTimePublished" />  
      <Property Name="DateTimePublished.Ticks" />  
  </Capture>  
</Session>';  
```  
  
 Führen Sie eine Abfrage, wie z. B. ein:  
  
```  
USE ssawPDW;  
GO  
SELECT * FROM dbo.FactFinance;  
```  
  
 Die folgende Abfrage gibt die Anzeigedauer der Autorisierung:  
  
```  
SELECT *   
FROM master.sysdiag.PdwOptimizationDiagnostics   
ORDER BY DateTimePublished;  
```  
  
 Wenn Sie mit der diagnosesitzung fertig sind, legen Sie mithilfe der **löschen Diagnose** Befehl.  
  
```  
DROP DIAGNOSTICS SESSION PdwOptimizationDiagnostics;  
```  
  
  

---
title: dm_execution_performance_counters (SSISDB-Datenbank) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 1b38e8e3-c560-4b6e-b60e-bfd7cfcd4fdf
caps.latest.revision: "6"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e143b66f9a10627695387bc5215c3b92565e230f
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="functions---dmexecutionperformancecounters"></a>Funktionen – dm_execution_performance_counters
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Gibt die Leistungsstatistik für eine Ausführung zurück, die auf dem [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Server ausgeführt wird.  
  
## <a name="syntax"></a>Syntax  
  
```sql  
dm_execution_performance_counters [ @execution_id = ] execution_id  
  
```  
  
## <a name="arguments"></a>Argumente  
 [ @execution_id = ] *Ausführungs-ID*  
 Der eindeutige Bezeichner der Ausführung, die ein oder mehrere Pakete enthält. Die Ausführung von Paketen mit dem Task "Paket ausführen" erfolgt in der gleichen Ausführung wie die Ausführung des übergeordneten Pakets.  
  
 Wenn eine Ausführungs-ID nicht angegeben wird, werden Leistungsstatistiken für mehrere Ausführungen zurückgegeben. Wenn Sie ein Mitglied der **ssis_admin** -Datenbankrolle sind, werden Leistungsstatistiken für alle aktiven Ausführungen zurückgegeben.  Wenn Sie kein Mitglied der **ssis_admin** -Datenbankrolle sind, werden Leistungsstatistiken zu den aktiven Ausführungen zurückgegeben, für die Sie Leseberechtigungen haben. *execution_id* ist **BigInt**.  
  
## <a name="remarks"></a>Hinweise  
 In der folgenden Tabelle werden die von der dm_execution_performance_counter-Funktion zurückgegebenen Leistungsindikatornamenswerte aufgeführt.  
  
|Indikatorname|Beschreibung|  
|------------------|-----------------|  
|Gelesene BLOB-Bytes|Anzahl der Bytes der BLOB-Daten (Binary Large Object), die das Datenflussmodul in allen Datenquellen liest.|  
|Geschriebene BLOB-Bytes|Anzahl der Bytes der BLOB-Daten (Binary Large Object), die das Datenflussmodul in alle Ziele schreibt.|  
|Verwendete BLOB-Dateien|Anzahl von BLOB-Dateien, die das Datenflussmodul zum Spoolen verwendet.|  
|Pufferspeicher|Arbeitsspeicher, der von den Integration Services-Puffern verwendet wird, einschließlich des physischen und virtuellen Arbeitsspeichers.|  
|Verwendete Puffer|Anzahl von Pufferobjekten aller Typen, die alle Datenflusskomponenten und das Datenflussmodul verwenden.|  
|Gespoolte Puffer|Anzahl der auf den Datenträger geschriebenen Puffer.|  
|Flatpufferspeicher|Arbeitsspeicher in Bytes, der von allen Flatpuffern verwendet wird. Als Flatpuffer werden Speicherblöcke bezeichnet, die von einer Komponente zum Speichern von Daten verwendet werden.|  
|Verwendete Flatpuffer|Anzahl der vom Datenflussmodul verwendeten Flatpuffer. Alle Flatpuffer sind private Puffer.|  
|Privater Pufferspeicher|Arbeitsspeicher, die von allen privaten Puffern verwendet wird. Ein Puffer wird als privat bezeichnet, wenn er von einer Transformation für temporäre Arbeitsvorgänge verwendet wird.<br /><br /> Ein Puffer ist nicht privat, wenn das Datenflussmodul den Puffer zur Unterstützung des Datenflusses erstellt.|  
|Private verwendete Puffer|Anzahl von Puffern, die die Transformationen für temporäre Arbeitsvorgänge verwenden.|  
|Gelesene Zeilen|Gesamtzahl der für die Ausführung bereiten Zeilen.|  
|Geschriebene Zeilen|Gesamtzahl der von der Ausführung geschriebenen Zeilen.|  
  
## <a name="return"></a>Rückgabewert  
 Die dm_execution_performance_counters-Funktion gibt für eine aktive Ausführung eine Tabelle mit den folgenden Spalten zurück. Die zurückgegebenen Informationen sind für alle in der Ausführung enthaltenen Pakete. Sind keine Ausführungen aktiv, wird eine leere Tabelle zurückgegeben.  
  
|Spaltenname|Spaltentyp|Beschreibung|Hinweise|  
|-----------------|-----------------|-----------------|-------------|  
|execution_id|**BigInt**<br /><br /> **NULL** ist kein gültiger Wert.|Eindeutiger Bezeichner für die das Paket enthaltende Ausführung.||  
|counter_name|**nvarchar(128)**|Der Name des Leistungsindikators.|Siehe den Abschnitt von Werten **Hinweise** .|  
|counter_value|**BigInt**|Wert, der vom Indikator zurückgegeben wird.||  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel gibt die Funktion Statistiken für eine aktive Ausführung mit einer ID von 34 zurück.  
  
```sql
select * from [catalog].[dm_execution_performance_counters] (34)  
```  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel gibt die Funktion abhängig von den Berechtigungen Statistiken für alle Ausführungen zurück, die auf dem [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Server ausgeführt werden.  
  
```sql
select * from [catalog].[dm_execution_performance_counters] (NULL)  
  
```  
  
## <a name="permissions"></a>Berechtigungen  
 Diese Funktion erfordert eine der folgenden Berechtigungen:  
  
-   READ- und MODIFY-Berechtigungen für die Instanz der Ausführung  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 Die folgende Liste beschreibt Bedingungen, unter denen die Funktion fehlschlägt.  
  
-   Der Benutzer verfügt nicht über MODIFY-Berechtigungen für die angegebene Ausführung.  
  
-   Die angegebene Ausführungs-ID ist ungültig.  
  
  

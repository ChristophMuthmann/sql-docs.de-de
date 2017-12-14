---
title: catalog.add_data_tap_by_guid | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: ed9d7fa3-61a1-4e21-ba43-1ead7dfc74eb
caps.latest.revision: "15"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: efb6c297b776cd6246f0c6226160afba9302bcdb
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="catalogadddatatapbyguid"></a>catalog.add_data_tap_by_guid
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Fügt einem bestimmten Datenflusspfad in einem Paketdatenfluss für eine Instanz der Ausführung eine Datenabzweigung hinzu.  
  
## <a name="syntax"></a>Syntax  
  
```sql  
catalog add_data_tap_by_guid [ @execution_id = ] execution_id  
, [ @dataflow_task_guid = ] dataflow_task_guid   
, [ @dataflow_path_id_string = ] dataflow_path_id_string  
, [ @data_filename = ] data_filename  
, [ @max_rows = ] max_rows  
, [ @data_tap_id = ] data_tap_id  
```  
  
## <a name="arguments"></a>Argumente  
 [ @execution_id = ] *execution_id*  
 Die Ausführungs-ID für die Ausführung, die das Paket enthält. Das Argument *execution_id* ist vom Typ **bigint**.  
  
 [ @dataflow_task_guid = ] *dataflow_task_guid*  
 Die ID für den Datentaskfluss im Paket, das den Datenflusspfad enthält, der abzurufen ist. Das Argument *dataflow_task_guid* ist vom Typ **uniqueidentifier**.  
  
 [ @dataflow_path_id_string = ] *dataflow_path_id_string*  
 Die Identifikationszeichenfolge für den Datenflusspfad. Mit einem Pfad werden zwei Datenflusskomponenten verbunden. Die **IdentificationString**-Eigenschaft für den Pfad gibt die Zeichenfolge an.  
  
 Um die Identifikationszeichenfolge zu suchen, klicken Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] mit der rechten Maustaste auf den Pfad zwischen zwei Datenflusskomponenten, und klicken dann auf **Eigenschaften**. Die **IdentificationString**-Eigenschaft wird im Fenster **Eigenschaften** angezeigt.  
  
 Das Argument *dataflow_path_id_string* ist vom Typ **nvarchar(4000)**.  
  
 [ @data_filename = ] *data_filename*  
 Der Name der Datei, in der die abgezweigten Daten gespeichert werden. Wenn der Datenflusstask in einer Foreach-Schleife oder einem For-Schleifencontainer ausgeführt wird, werden die abgezweigten Daten für jede Iteration der Schleife in separaten Dateien gespeichert. Jeder Datei wird eine Zahl für die jeweilige Iteration als Präfix vorangestellt. Datenabzweigungsdateien werden in den Ordner „*\<Ordner für die SQL Server-Installation>*\130\DTS\\“ geschrieben. Das Argument *data_filename* ist vom Typ **nvarchar(4000)**.  
  
 [ @max_rows = ] max_rows  
 Die Anzahl der Zeilen, die während der Datenabzweigung aufgezeichnet werden. Wenn dieser Wert nicht angegeben wird, werden alle Zeilen aufgezeichnet. Das Argument „max_rows“ ist vom Typ **int**.  
  
 [ @data_tap_id = ] *data_tap_id*  
 Die ID der Datenabzweigung. Das Argument *data_tap_id* ist vom Typ **bigint**.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird eine Datenabzweigung im Datenflusspfad `Paths[SRC DimDCVentor.OLE DB Source Output]` im Datenflusstask `{D978A2E4-E05D-4374-9B05-50178A8817E8}` erstellt. Die abgezweigten Daten werden in der Datei "DCVendorOutput.csv" gespeichert.  
  
```sql
exec catalog.add_data_tap_by_guid   @execution_id,   
'{D978A2E4-E05D-4374-9B05-50178A8817E8}',   
'Paths[SRC DimDCVentor.OLE DB Source Output]',   
'D:\demos\datafiles\DCVendorOutput.csv'  
```  
  
## <a name="remarks"></a>Hinweise  
 Um Datenabzweigungen hinzuzufügen, muss die Ausführungsinstanz den Status „Erstellt“ (der Wert 1 in der Spalte **Zustand** der Sicht [catalog.operations &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md)) aufweisen. Der Statuswert ändert sicher, wenn Sie die Ausführung starten. Sie können eine Ausführung erstellen, indem Sie [catalog.create_execution &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md) aufrufen.  
  
 Folgende Überlegungen sind bei der gespeicherten Prozedur "add_data_tap_by_guid" zu beachten.  
  
-   Eine neu hinzugefügte Datenabzweigung wird erst beim Ausführen des Pakets überprüft.  
  
-   Es wird empfohlen, die Anzahl von Zeilen, die während der Datenabzweigung aufgezeichnet werden, zu beschränken, damit keine zu großen Datendateien generiert werden. Wenn der Computer, auf dem die gespeicherte Prozedur ausgeführt wird, nicht mehr über genügend Speicherplatz für die Datendateien verfügt, wird die gespeicherte Prozedur nicht mehr ausgeführt.  
  
-   Die Ausführung der gespeicherten Prozedur "add_data_tap_by_guid" wirkt sich auf die Leistung des Pakets aus. Es wird empfohlen, die gespeicherte Prozedur nur zum Beheben von Datenproblemen auszuführen.  
  
-   Um auf die Datei mit den abgerufenen Daten zuzugreifen, müssen Sie über Administratorberechtigungen für den Computer verfügen, auf dem die gespeicherte Prozedur ausgeführt wird. Sie müssen alternativ der Benutzer sein, der die Ausführung startete, die das Paket mit der Datenabzweigung enthält.  
  
## <a name="return-codes"></a>Rückgabecodes  
 0 (Erfolg)  
  
 Wenn die gespeicherte Prozedur fehlschlägt, wird ein Fehler ausgelöst.  
  
## <a name="result-set"></a>Resultset  
 Keine  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   MODIFY-Berechtigungen für die Instanz der Ausführung  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 Die folgende Liste beschreibt Bedingungen, unter denen die gespeicherte Prozedur fehlschlägt.  
  
-   Der Benutzer verfügt nicht über MODIFY-Berechtigungen.  
  
-   Die Datenabzweigung für die angegebene Komponente im angegebenen Paket wurde bereits hinzugefügt.  
  
-   Der für die Anzahl der aufzuzeichnenden Zeilen angegebene Wert ist ungültig.  
  
## <a name="requirements"></a>Anforderungen  
  
## <a name="see-also"></a>Siehe auch  
 [catalog.add_data_tap](../../integration-services/system-stored-procedures/catalog-add-data-tap.md)  
  
  

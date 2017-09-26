---
title: Catalog.add_data_tap_by_guid | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: ed9d7fa3-61a1-4e21-ba43-1ead7dfc74eb
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9bd4ecb4a6a419f1965a349d46d16d764dd83708
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="catalogadddatatapbyguid"></a>catalog.add_data_tap_by_guid
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Fügt einem bestimmten Datenflusspfad in einem Paketdatenfluss für eine Instanz der Ausführung eine Datenabzweigung hinzu.  
  
## <a name="syntax"></a>Syntax  
  
```tsql  
add_data_tap_by_guid [ @execution_id = ] execution_id  
[ @dataflow_task_guid = ] dataflow_task_guid   
[ @dataflow_path_id_string = ] dataflow_path_id_string  
[ @data_filename = ] data_filename  
[ @max_rows = ] max_rows  
[ @data_tap_id = ] data_tap_id  
```  
  
## <a name="arguments"></a>Argumente  
 [ @execution_id =] *Execution_id*  
 Die Ausführungs-ID für die Ausführung, die das Paket enthält. Die *Execution_id* ist ein **"bigint"**.  
  
 [ @dataflow_task_guid =] *Dataflow_task_guid*  
 Die ID für den Datentaskfluss im Paket, das den Datenflusspfad enthält, der abzurufen ist. Die *Dataflow_task_guid* ist ein**"uniqueidentifier"**.  
  
 [ @dataflow_path_id_string =] *Dataflow_path_id_string*  
 Die Identifikationszeichenfolge für den Datenflusspfad. Mit einem Pfad werden zwei Datenflusskomponenten verbunden. Die **IdentificationString** Eigenschaft für den Pfad Gibt die Zeichenfolge an.  
  
 Suchen Sie die ID-Zeichenfolge in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] mit der rechten Maustaste im Pfads zwischen zwei Datenflusskomponenten, und klicken Sie dann auf **Eigenschaften**. Die **IdentificationString** Eigenschaft wird in der **Eigenschaften** Fenster.  
  
 Die *Dataflow_path_id_string* ist ein **nvarchar(4000)**.  
  
 [ @data_filename =] *Data_filename*  
 Der Name der Datei, in der die abgezweigten Daten gespeichert werden. Wenn der Datenflusstask in einer Foreach-Schleife oder einem For-Schleifencontainer ausgeführt wird, werden die abgezweigten Daten für jede Iteration der Schleife in separaten Dateien gespeichert. Jeder Datei wird eine Zahl für die jeweilige Iteration als Präfix vorangestellt. Datenabzweigungsdateien werden geschrieben, zu dem Ordner "*\<SQL Server-Installationsordner >*\130\DTS\\". Die *Data_filename* ist ein **nvarchar(4000)**.  
  
 [ @max_rows =] Max_rows  
 Die Anzahl der Zeilen, die während der Datenabzweigung aufgezeichnet werden. Wenn dieser Wert nicht angegeben wird, werden alle Zeilen aufgezeichnet. Max_rows ist ein **Int**.  
  
 [ @data_tap_id =] *Data_tap_id*  
 Die ID der Datenabzweigung. Die *Data_tap_id* ist ein **"bigint"**.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird eine datenabzweigung erstellt, auf den Datenflusspfad `Paths[SRC DimDCVentor.OLE DB Source Output]`im Datenflusstask `{D978A2E4-E05D-4374-9B05-50178A8817E8}`. Die abgezweigten Daten werden in der Datei "DCVendorOutput.csv" gespeichert.  
  
```  
exec catalog.add_data_tap_by_guid   @execution_id,   
'{D978A2E4-E05D-4374-9B05-50178A8817E8}',   
'Paths[SRC DimDCVentor.OLE DB Source Output]',   
'D:\demos\datafiles\DCVendorOutput.csv'  
  
```  
  
## <a name="remarks"></a>Hinweise  
 Um datenabzweigungen hinzuzufügen, muss die Instanz der Ausführung den Status "erstellt" (der Wert 1 in der **Status** Spalte die [catalog.operations &#40; SSISDB-Datenbank &#41; ](../../integration-services/system-views/catalog-operations-ssisdb-database.md)Ansicht). Der Statuswert ändert sicher, wenn Sie die Ausführung starten. Sie können eine Ausführung erstellen, durch den Aufruf [Catalog. create_execution &#40; SSISDB-Datenbank &#41; ](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md).  
  
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
  
  

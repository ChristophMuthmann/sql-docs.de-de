---
title: Catalog.add_data_tap | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: a25ebcc7-535e-4619-adf6-4e2b5a62ba37
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 686b40e7e1ad7f7843bee5af3295fdf394538f63
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="catalogadddatatap"></a>catalog.add_data_tap
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Fügt auf der Ausgabe einer Komponente in einem Paketdatenfluss für eine Instanz der Ausführung eine Datenabzweigung hinzu.  
  
## <a name="syntax"></a>Syntax  
  
```sql  
catalog.add_data_tap [ @execution_id = ] execution_id  
, [ @task_package_path = ] task_package_path  
, [ @dataflow_path_id_string = ] dataflow_path_id_string  
, [ @data_filename = ] data_filename  
, [ @max_rows = ] max_rows  
, [ @data_tap_id = ] data_tap_id OUTPUT  
```  
  
## <a name="arguments"></a>Argumente  
 [ @execution_id =] *Execution_id*  
 Die Ausführungs-ID für die Ausführung, die das Paket enthält. Die *Execution_id* ist ein **"bigint"**.  
  
 [ @task_package_path =] *Task_package_path*  
 Der Paketpfad für den Datenflusstask. Die **PackagePath** -Eigenschaft für den Datenflusstask gibt den Pfad an. Der Pfad berücksichtigt die Groß- und Kleinschreibung. Suchen Sie den Paketpfad in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] Maustaste auf den Datenflusstask, und klicken Sie dann auf **Eigenschaften**. Die **PackagePath** Eigenschaft wird in der **Eigenschaften** Fenster.  
  
 Die *Task_package_path* ist ein **nvarchar(max)**.  
  
 [ @dataflow_path_id_string =] *Dataflow_path_id_string*  
 Die Identifikationszeichenfolge für den Datenflusspfad. Mit einem Pfad werden zwei Datenflusskomponenten verbunden. Die **IdentificationString** Eigenschaft für den Pfad Gibt die Zeichenfolge an.  
  
 Suchen Sie die ID-Zeichenfolge in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] mit der rechten Maustaste im Pfads zwischen zwei Datenflusskomponenten, und klicken Sie dann auf **Eigenschaften**. Die **IdentificationString** Eigenschaft wird in der **Eigenschaften** Fenster.  
  
 Die *Dataflow_path_id_string* ist ein **nvarchar(4000)**.  
  
 [ @data_filename =] *Data_filename*  
 Der Name der Datei, in der die abgezweigten Daten gespeichert werden. Wenn der Datenflusstask in einer Foreach-Schleife oder einem For-Schleifencontainer ausgeführt wird, werden die abgezweigten Daten für jede Iteration der Schleife in separaten Dateien gespeichert. Jeder Datei wird eine Zahl für die jeweilige Iteration als Präfix vorangestellt.  
  
 Standardmäßig befindet sich die Datei in die \< *Laufwerk*>: Ordner "\Programme\Microsoft SQL Server\130\DTS\DataDumps".  
  
 Die *Data_filename* ist ein **nvarchar(4000)**.  
  
 [ @max_rows =] *Max_rows*  
 Die Anzahl der Zeilen, die während der Datenabzweigung aufgezeichnet werden. Wenn dieser Wert nicht angegeben wird, werden alle Zeilen aufgezeichnet. Die *Max_rows* ist ein **Int**.  
  
 [ @data_tap_id =] *Data_tap_id*  
 Gibt die ID der Datenabzweigung zurück. Die *Data_tap_id* ist ein **"bigint"**.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird eine Datenabzweigung für den Datenflusspfad `'Paths[OLE DB Source.OLE DB Source Output]` im Datenflusstask `\Package\Data Flow Task` erstellt. Die abgezweigten Daten werden gespeichert, der `output0.txt` Datei im Ordner (\<*Laufwerk*>: \Programme\Microsoft SQL Server\130\DTS\DataDumps).  
  
```sql
Declare @execution_id bigint  
Exec SSISDB.Catalog.create_execution @folder_name='Packages',@project_name='SSISPackages', @package_name='Package.dtsx',@reference_id=Null, @use32bitruntime=False, @execution_id=@execution_id OUTPUT  
  
Exec SSISDB.Catalog.set_execution_parameter_value @execution_id,50, 'LOGGING_LEVEL', 0  
  
Exec SSISDB.Catalog.add_data_tap @execution_id, @task_package_path='\Package\Data Flow Task', @dataflow_path_id_string = 'Paths[OLE DB Source.OLE DB Source Output]', @data_filename = 'output0.txt'  
  
Exec SSISDB.Catalog.start_execution @execution_id  
```  
  
## <a name="remarks"></a>Hinweise  
 Um datenabzweigungen hinzuzufügen, muss die Instanz der Ausführung den Status "erstellt" (der Wert 1 in der **Status** Spalte die [catalog.operations &#40; SSISDB-Datenbank &#41; ](../../integration-services/system-views/catalog-operations-ssisdb-database.md)Ansicht). Der Statuswert ändert sicher, wenn Sie die Ausführung starten. Sie können eine Ausführung erstellen, durch den Aufruf [Catalog. create_execution &#40; SSISDB-Datenbank &#41; ](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md).  
  
 Folgende Überlegungen sind bei der gespeicherten Prozedur "add_data_tap" zu beachten.  
  
-   Wenn eine Ausführung ein übergeordnetes Paket und mindestens ein untergeordnetes Paket enthält, müssen Sie eine Datenabzweigung für jedes Paket hinzufügen, für das Sie Daten abzweigen möchten.  
  
-   Wenn ein Paket mehr als einen Datenflusstask mit dem gleichen Namen enthält, wird der Datenflusstask durch "task_package_path" mit Angaben zur abgezweigten Komponentenausgabe eindeutig identifiziert.  
  
-   Wenn Sie eine datenabzweigung hinzufügen, ist es nicht überprüft, bevor das Paket ausgeführt wird.  
  
-   Es wird empfohlen, die Anzahl von Zeilen, die während der Datenabzweigung aufgezeichnet werden, zu beschränken, damit keine zu großen Datendateien generiert werden. Wenn auf dem Computer, auf dem die gespeicherte Prozedur ausgeführt wird, nicht genügend Speicherplatz für die Datendateien verfügbar ist, wird die Ausführung des Pakets beendet und eine Fehlermeldung in ein Protokoll geschrieben.  
  
-   Die Ausführung der gespeicherten Prozedur "add_data_tap" wirkt sich auf die Leistung des Pakets aus. Es wird empfohlen, die gespeicherte Prozedur nur zum Beheben von Datenproblemen auszuführen.  
  
-   Um auf die Datei zuzugreifen, in der die abgezweigten Daten speichert sind, müssen Sie auf dem Computer, auf dem die gespeicherte Prozedur ausgeführt wird, als Administrator angelegt sein. Außerdem müssen Sie die Ausführung gestartet haben, die das Paket mit der Datenabzweigung enthält.  
  
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
  
## <a name="external-resources"></a>Externe Ressourcen  
 Blogeintrag, [SSIS 2012: ein Peek auf Datenabzweigungen](http://go.microsoft.com/fwlink/?LinkId=239983), auf Rafael-salas.com.  
  
## <a name="see-also"></a>Siehe auch  
 [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md)  
  
  


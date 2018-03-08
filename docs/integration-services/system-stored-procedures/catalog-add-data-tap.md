---
title: catalog.add_data_tap | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: a25ebcc7-535e-4619-adf6-4e2b5a62ba37
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c1c4130b66a7c9c2011aaf1e2af30f799d753162
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="catalogadddatatap"></a>catalog.add_data_tap
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

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
 [ @execution_id = ] *execution_id*  
 Die Ausführungs-ID für die Ausführung, die das Paket enthält. Das Argument *execution_id* ist vom Typ **bigInt**.  
  
 [ @task_package_path = ] *task_package_path*  
 Der Paketpfad für den Datenflusstask. Die **PackagePath**-Eigenschaft für den Datenflusstask gibt den Pfad an. Der Pfad berücksichtigt die Groß- und Kleinschreibung. Um den Paketpfad zu suchen, klicken Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] mit der rechten Maustaste auf den Datenflusstask, und klicken Sie dann auf **Eigenschaften**. Die **PackagePath**-Eigenschaft wird im Fenster **Eigenschaften** angezeigt.  
  
 Das Argument *task_package_path* ist vom Typ **nvarchar(max)**.  
  
 [ @dataflow_path_id_string = ] *dataflow_path_id_string*  
 Die Identifikationszeichenfolge für den Datenflusspfad. Mit einem Pfad werden zwei Datenflusskomponenten verbunden. Die **IdentificationString**-Eigenschaft für den Pfad gibt die Zeichenfolge an.  
  
 Um die Identifikationszeichenfolge zu suchen, klicken Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] mit der rechten Maustaste auf den Pfad zwischen zwei Datenflusskomponenten, und klicken dann auf **Eigenschaften**. Die **IdentificationString**-Eigenschaft wird im Fenster **Eigenschaften** angezeigt.  
  
 Das Argument *dataflow_path_id_string* ist vom Typ **nvarchar(4000)**.  
  
 [ @data_filename = ] *data_filename*  
 Der Name der Datei, in der die abgezweigten Daten gespeichert werden. Wenn der Datenflusstask in einer Foreach-Schleife oder einem For-Schleifencontainer ausgeführt wird, werden die abgezweigten Daten für jede Iteration der Schleife in separaten Dateien gespeichert. Jeder Datei wird eine Zahl für die jeweilige Iteration als Präfix vorangestellt.  
  
 Die Datei wird standardmäßig im Ordner „\<*Laufwerk*>:\Programme\Microsoft SQL Server\130\DTS\DataDumps“ gespeichert.  
  
 Das Argument *data_filename* ist vom Typ **nvarchar(4000)**.  
  
 [ @max_rows = ] *max_rows*  
 Die Anzahl der Zeilen, die während der Datenabzweigung aufgezeichnet werden. Wenn dieser Wert nicht angegeben wird, werden alle Zeilen aufgezeichnet. Das Argument *max_rows* ist vom Typ **int**.  
  
 [ @data_tap_id = ] *data_tap_id*  
 Gibt die ID der Datenabzweigung zurück. Das Argument *data_tap_id* ist vom Typ **bigint**.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird eine Datenabzweigung für den Datenflusspfad `'Paths[OLE DB Source.OLE DB Source Output]` im Datenflusstask `\Package\Data Flow Task` erstellt. Die abgezweigten Daten werden in der Datei `output0.txt` im Ordner „\<*Laufwerk*>:\Programme\Microsoft SQL Server\130\DTS\DataDumps“ gespeichert.  
  
```sql
Declare @execution_id bigint  
Exec SSISDB.Catalog.create_execution @folder_name='Packages',@project_name='SSISPackages', @package_name='Package.dtsx',@reference_id=Null, @use32bitruntime=False, @execution_id=@execution_id OUTPUT  
  
Exec SSISDB.Catalog.set_execution_parameter_value @execution_id,50, 'LOGGING_LEVEL', 0  
  
Exec SSISDB.Catalog.add_data_tap @execution_id, @task_package_path='\Package\Data Flow Task', @dataflow_path_id_string = 'Paths[OLE DB Source.OLE DB Source Output]', @data_filename = 'output0.txt'  
  
Exec SSISDB.Catalog.start_execution @execution_id  
```  
  
## <a name="remarks"></a>Remarks  
 Um Datenabzweigungen hinzuzufügen, muss die Ausführungsinstanz den Status „Erstellt“ (der Wert 1 in der Spalte **Zustand** der Sicht [catalog.operations &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md)) aufweisen. Der Statuswert ändert sicher, wenn Sie die Ausführung starten. Sie können eine Ausführung erstellen, indem Sie [catalog.create_execution &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md) aufrufen.  
  
 Folgende Überlegungen sind bei der gespeicherten Prozedur "add_data_tap" zu beachten.  
  
-   Wenn eine Ausführung ein übergeordnetes Paket und mindestens ein untergeordnetes Paket enthält, müssen Sie eine Datenabzweigung für jedes Paket hinzufügen, für das Sie Daten abzweigen möchten.  
  
-   Wenn ein Paket mehr als einen Datenflusstask mit dem gleichen Namen enthält, wird der Datenflusstask durch "task_package_path" mit Angaben zur abgezweigten Komponentenausgabe eindeutig identifiziert.  
  
-   Eine neu hinzugefügte Datenabzweigung wird erst beim Ausführen des Pakets überprüft.  
  
-   Es wird empfohlen, die Anzahl von Zeilen, die während der Datenabzweigung aufgezeichnet werden, zu beschränken, damit keine zu großen Datendateien generiert werden. Wenn auf dem Computer, auf dem die gespeicherte Prozedur ausgeführt wird, nicht genügend Speicherplatz für die Datendateien verfügbar ist, wird die Ausführung des Pakets beendet und eine Fehlermeldung in ein Protokoll geschrieben.  
  
-   Die Ausführung der gespeicherten Prozedur "add_data_tap" wirkt sich auf die Leistung des Pakets aus. Es wird empfohlen, die gespeicherte Prozedur nur zum Beheben von Datenproblemen auszuführen.  
  
-   Um auf die Datei zuzugreifen, in der die abgezweigten Daten speichert sind, müssen Sie auf dem Computer, auf dem die gespeicherte Prozedur ausgeführt wird, als Administrator angelegt sein. Außerdem müssen Sie die Ausführung gestartet haben, die das Paket mit der Datenabzweigung enthält.  
  
## <a name="return-codes"></a>Rückgabecodes  
 0 (Erfolg)  
  
 Wenn die gespeicherte Prozedur fehlschlägt, wird ein Fehler ausgelöst.  
  
## <a name="result-set"></a>Resultset  
 InclusionThresholdSetting  
  
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
 Blogeintrag [SSIS 2012: A Peek to Data Taps](http://go.microsoft.com/fwlink/?LinkId=239983) (SSIS 2012: Ein kurzer Blick auf Datenabzweigungen) auf rafael-salas.com.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md)  
  
  

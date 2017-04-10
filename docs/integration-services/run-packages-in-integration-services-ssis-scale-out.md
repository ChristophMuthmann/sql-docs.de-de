---
title: "Ausf&#252;hren von Paketen in horizontaler Hochskalierung f&#252;r Integration Services (SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4c2f4cd7-9c47-416d-bb1e-40acc3e05342
caps.latest.revision: 5
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 5
---
# Ausf&#252;hren von Paketen in horizontaler Hochskalierung f&#252;r Integration Services (SSIS)
Sobald die Pakete auf dem Integration Services-Server bereitgestellt sind, können Sie diese in horizontaler Hochskalierung ausführen.

## <a name="run-packages-with-execute-package-in-scale-out-dialog"></a>Ausführen von Paketen im Dialogfeld **Paket in horizontaler Hochskalierung ausführen** 

1. ### <a name="open-the-execute-package-in-scale-out-dialog-box"></a>Öffnen des Dialogfelds „Paket in horizontaler Hochskalierung ausführen“ ###
    Stellen Sie in [!INCLUDE[ssManStudioFull_md](../includes/ssmanstudiofull-md.md)] eine Verbindung mit dem Integration Services-Server her. Erweitern Sie im Objekt-Explorer die Struktur, um die Knoten unter **Integration Services-Kataloge** anzuzeigen. Klicken Sie mit der rechten Maustaste auf den **SSISDB**-Knoten oder auf das Projekt oder Paket, das Sie ausführen möchten, und klicken Sie dann auf **In horizontaler Hochskalierung ausführen**.
2. ### <a name="select-packages-and-set-the-options"></a>Auswählen von Paketen und Festlegen der Optionen ###
    Auf der Seite **Paketauswahl** wählen Sie mehrere auszuführende Pakete aus, und legen Sie für jedes Paket die Umgebung, die Parameter, die Verbindungs-Manager und die erweiterten Optionen fest. Klicken Sie auf ein Paket, um diese Optionen festzulegen.
    
    Auf der Registerkarte **Erweitert** legen Sie die für horizontale Hochskalierung verwendete Option **Wiederholungsanzahl** fest. Hiermit wird festgelegt, wie oft das Ausführen eines Pakets versucht wird, wenn ein Fehler auftritt.
3. ### <a name="select-machines"></a>Auswählen von Computern ###
    Auf der Seite **Computerauswahl** wählen Sie die Computer mit Worker für horizontales Hochskalieren aus, auf denen die Pakete ausgeführt werden sollen. Standardmäßig können die Pakete auf jedem Computer ausgeführt werden. 

   > [!NOTE]
> Die Pakete werden mit den Anmeldeinformationen der Benutzerkonten der Dienste für Worker für horizontales Hochskalieren ausgeführt, die auf der Seite **Computerauswahl** angezeigt werden. Standardmäßig ist dies das Konto „NT-Dienst\SSISScaleOutWorker140“. Es bietet sich an, dass Sie zu Ihren entsprechenden eigenen Konten wechseln.

4. ### <a name="run-the-packages-and-view-reports"></a>Ausführen der Pakete und Anzeigen von Berichten 
    Klicken Sie auf **OK**, um die Paketausführungen zu starten. Um den Ausführungsbericht für ein Paket anzuzeigen, klicken Sie im Objekt-Explorer mit der rechten Maustaste auf das Paket, klicken Sie auf **Berichte**, klicken Sie auf **Alle Ausführungen**, und suchen Sie nach der Ausführung.
    
    
## <a name="run-packages-with-stored-procedures"></a>Ausführen von Paketen mit gespeicherten Prozeduren

1. ### <a name="create-executions"></a>Erstellen von Ausführungen ###
    Rufen Sie [catalog].[create_execution] für jedes Paket auf. Legen Sie den Parameter **@runincluster** auf „true“ fest. Sind nicht alle Computer mit Worker für horizontales Hochskalieren berechtigt, das Paket auszuführen, legen Sie den Parameter **@useanyworker** auf „false“ fest.   
2. ### <a name="set-execution-parameters"></a>Festlegen von Ausführungsparametern ###
    Rufen Sie [catalog].[set_execution_parameter_value] für jede Ausführung auf.
3. ### <a name="set-scale-out-workers"></a>Festlegen von Workern für horizontales Hochskalieren ###
    Rufen Sie [catalog].[add_execution_worker] auf. Sind alle Computer berechtigt, das Paket auszuführen, müssen Sie diese gespeicherte Prozedur nicht aufrufen. 
4. ### <a name="start-executions"></a>Starten der Ausführungen ###
    Rufen Sie [catalog].[start_execution] auf. Legen Sie den Parameter **@retry_count** fest, um anzugeben, wie oft das Ausführen eines Pakets versucht wird, wenn ein Fehler auftritt.
    
    ### <a name="example"></a>Beispiel  ###  
    Im folgenden Beispiel werden zwei Pakete („package1.dtsx“ und „package2.dtsx“) in horizontaler Hochskalierung mit einem Worker für horizontales Hochskalieren ausgeführt.  
    ```
    Declare @execution_id bigint
    EXEC [SSISDB].[catalog].[create_execution] @package_name=N'package1.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'folder1', @project_name=N'project1', @use32bitruntime=False, @reference_id=Null, @useanyworker=False, @runincluster=True
    Select @execution_id
    DECLARE @var0 smallint = 1
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0
    EXEC [SSISDB].[catalog].[add_execution_worker] @execution_id,  @workeragent_id=N'64c020e2-f819-4c2d-a22f-efb31a91e70a'
    EXEC [SSISDB].[catalog].[start_execution] @execution_id,  @retry_count=0
    GO

    Declare @execution_id bigint
    EXEC [SSISDB].[catalog].[create_execution] @package_name=N'package2.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'folder2', @project_name=N'project2', @use32bitruntime=False, @reference_id=Null, @useanyworker=False, @runincluster=True
    Select @execution_id
    DECLARE @var0 smallint = 1
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0
    EXEC [SSISDB].[catalog].[add_execution_worker] @execution_id,  @workeragent_id=N'64c020e2-f819-4c2d-a22f-efb31a91e70a'
    EXEC [SSISDB].[catalog].[start_execution] @execution_id,  @retry_count=0
    GO
    ```


## <a name="permissions"></a>Berechtigungen
Für ein Ausführen von Paketen in horizontaler Hochskalierung ist eine der folgenden Berechtigungen erforderlich:

-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  

-   Mitgliedschaft in der Datenbankrolle **ssis_cluster_executor**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
    
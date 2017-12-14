---
title: "Ausführen von Paketen in SSIS Scale Out (SQL Server Integration Services) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "1"
author: haoqian
ms.author: haoqian
manager: jhubbard
f1_keywords: sql13.ssis.ssms.ispackageexecuteinscaleout.f1
ms.workload: Inactive
ms.openlocfilehash: 88537ff52ada042d642b8915342e374ecca3246e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="run-packages-in-integration-services-ssis-scale-out"></a>Ausführen von Paketen in SSIS Scale Out (SQL Server Integration Services)
Sobald die Pakete auf dem Integration Services-Server bereitgestellt sind, können Sie diese in horizontaler Hochskalierung ausführen.

## <a name="run-packages-with-execute-package-in-scale-out-dialog"></a>Ausführen von Paketen mit dem Dialogfeld „Paket in Scale Out ausführen“ 

1. Öffnen des Dialogfelds „Paket in horizontaler Hochskalierung ausführen“

    Stellen Sie in [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] eine Verbindung mit dem Integration Services-Server her. Erweitern Sie im Objekt-Explorer die Struktur, um die Knoten unter **Integration Services-Kataloge**anzuzeigen. Klicken Sie mit der rechten Maustaste auf den **SSISDB** -Knoten oder auf das Projekt oder Paket, das Sie ausführen möchten, und klicken Sie dann auf **In horizontaler Hochskalierung ausführen**.

2. Auswählen von Paketen und Festlegen der Optionen

    Auf der Seite **Paketauswahl** wählen Sie mehrere auszuführende Pakete aus, und legen Sie für jedes Paket die Umgebung, die Parameter, die Verbindungs-Manager und die erweiterten Optionen fest. Klicken Sie auf ein Paket, um diese Optionen festzulegen.
    
    Auf der Registerkarte **Erweitert** legen Sie die für horizontale Hochskalierung verwendete Option **Wiederholungsanzahl**fest. Hiermit wird festgelegt, wie oft das Ausführen eines Pakets versucht wird, wenn ein Fehler auftritt.

    > [!Note]
    > Die Option **Bei Fehler Abbild sichern** wird nur wirksam, wenn das Konto, unter dem der Scale Out-Workerdienst ausgeführt wird, einem Administrator des lokalen Computers zugeordnet ist.

3. Auswählen von Computern

    Auf der Seite **Computerauswahl** wählen Sie die Computer mit Worker für horizontales Hochskalieren aus, auf denen die Pakete ausgeführt werden sollen. Standardmäßig können die Pakete auf jedem Computer ausgeführt werden. 

   > [!Note] 
   > Die Pakete werden mit den Anmeldeinformationen der Benutzerkonten der Dienste für Worker für horizontales Hochskalieren ausgeführt, die auf der Seite **Computerauswahl** angezeigt werden. Standardmäßig ist dies das Konto „NT-Dienst\SSISScaleOutWorker140“. Es bietet sich an, dass Sie zu Ihren entsprechenden eigenen Konten wechseln.

   >[!WARNING]
   >Die von verschiedenen Benutzern im selben Worker ausgelösten Paketausführungen werden mit demselben Konto ausgeführt. Es gibt keine Sicherheitsbegrenzung zwischen diesen. 

4. Ausführen der Pakete und Anzeigen von Berichten 

    Klicken Sie auf **OK** , um die Paketausführungen zu starten. Um den Ausführungsbericht für ein Paket anzuzeigen, klicken Sie im Objekt-Explorer mit der rechten Maustaste auf das Paket, klicken Sie auf **Berichte**, klicken Sie auf **Alle Ausführungen**, und suchen Sie nach der Ausführung.
    
## <a name="run-packages-with-stored-procedures"></a>Ausführen von Paketen mit gespeicherten Prozeduren

1. Erstellen von Ausführungen

    Rufen Sie [catalog].[create_execution] für jedes Paket auf. Legen Sie den Parameter **@runinscaleout** auf „true“ fest. Sind nicht alle Computer mit Worker für horizontales Hochskalieren berechtigt, das Paket auszuführen, legen Sie den Parameter **@useanyworker** auf „false“ fest.   

2. Festlegen von Ausführungsparametern

    Rufen Sie [catalog].[set_execution_parameter_value] für jede Ausführung auf.

3. Festlegen von Workern für horizontales Hochskalieren

    Rufen Sie [catalog].[add_execution_worker] auf. Sind alle Computer berechtigt, das Paket auszuführen, müssen Sie diese gespeicherte Prozedur nicht aufrufen. 

4. Starten der Ausführungen

    Rufen Sie [catalog].[start_execution] auf. Legen Sie den Parameter **@retry_count** fest, um anzugeben, wie oft das Ausführen eines Pakets versucht wird, wenn ein Fehler auftritt.
    
#### <a name="example"></a>Beispiel
Im folgenden Beispiel werden zwei Pakete („package1.dtsx“ und „package2.dtsx“) in horizontaler Hochskalierung mit einem Worker für horizontales Hochskalieren ausgeführt.  

```sql
Declare @execution_id bigint
EXEC [SSISDB].[catalog].[create_execution] @package_name=N'package1.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'folder1', @project_name=N'project1', @use32bitruntime=False, @reference_id=Null, @useanyworker=False, @runinscaleout=True
Select @execution_id
DECLARE @var0 smallint = 1
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0
EXEC [SSISDB].[catalog].[add_execution_worker] @execution_id,  @workeragent_id=N'64c020e2-f819-4c2d-a22f-efb31a91e70a'
EXEC [SSISDB].[catalog].[start_execution] @execution_id,  @retry_count=0
GO

Declare @execution_id bigint
EXEC [SSISDB].[catalog].[create_execution] @package_name=N'package2.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'folder2', @project_name=N'project2', @use32bitruntime=False, @reference_id=Null, @useanyworker=False, @runinscaleout=True
Select @execution_id
DECLARE @var0 smallint = 1
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0
EXEC [SSISDB].[catalog].[add_execution_worker] @execution_id,  @workeragent_id=N'64c020e2-f819-4c2d-a22f-efb31a91e70a'
EXEC [SSISDB].[catalog].[start_execution] @execution_id,  @retry_count=0
GO
```

### <a name="permissions"></a>Berechtigungen
Für ein Ausführen von Paketen in horizontaler Hochskalierung ist eine der folgenden Berechtigungen erforderlich:

-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  

-   Mitgliedschaft in der Datenbankrolle **ssis_cluster_executor**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  

## <a name="set-default-execution-mode"></a>Festlegen des Standardausführungsmodus
Um den Standardausführungsmodus auf „Scale Out“ festzulegen, klicken Sie im Objekt-Explorer von SSMS mit der rechten Maustaste auf den **SSISDB**-Knoten und wählen **Eigenschaften**.
Legen Sie im Dialogfeld **Katalogeigenschaften** für **Serverweiter Standardausführungsmodus** die Option **Scale Out** fest.

Nach dieser Einstellung ist es nicht erforderlich, den **@runinscaleout**-Parameter für [catalog].[create_execution] anzugeben. Ausführungen werden automatisch in Scale Out ausgeführt. 

![Ausführungsmodus](media\exe-mode.PNG)

Um Standardausführungsmodus wieder auf den Modus ohne Scale Out zurückzusetzen, legen Sie einfach **Serverweiter Standardausführungsmodus** auf **Server** fest.

## <a name="run-package-in-sql-agent-job"></a>Ausführen eines Pakets im SQL-Agent-Auftrag
Im SQL-Agent-Auftrag können Sie festlegen, dass im Rahmen des Auftrags ein SSIS-Paket ausgeführt werden soll. Um das Paket in Scale Out auszuführen, können Sie den oben genannten Standardausführungsmodus nutzen. Nachdem der Standardausführungsmodus auf „Scale Out“ festgelegt wurde, werden Pakete in SQL-Agent-Aufträgen in Scale Out ausgeführt.

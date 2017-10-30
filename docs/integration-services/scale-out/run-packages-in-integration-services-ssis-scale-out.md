---
title: "Horizontales Skalieren Ausführen von Paketen in SQL Server Integration Services (SSIS) | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
f1_keywords:
- sql13.ssis.ssms.ispackageexecuteinscaleout.f1
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2c158ae6a711ecb5f5065561c0c8c303e9a09980
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---

# <a name="run-packages-in-integration-services-ssis-scale-out"></a>Ausführen von Paketen in Integration Services (SSIS) horizontal skalieren
Sobald die Pakete auf dem Integration Services-Server bereitgestellt sind, können Sie diese in horizontaler Hochskalierung ausführen.

## <a name="run-packages-with-execute-package-in-scale-out-dialog"></a>Ausführen von Paketen mit ausführen Paket In horizontal skalieren Dialogfeld 

1. Öffnen des Dialogfelds „Paket in horizontaler Hochskalierung ausführen“

    Stellen Sie in [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] eine Verbindung mit dem Integration Services-Server her. Erweitern Sie im Objekt-Explorer die Struktur, um die Knoten unter **Integration Services-Kataloge**anzuzeigen. Klicken Sie mit der rechten Maustaste auf den **SSISDB** -Knoten oder auf das Projekt oder Paket, das Sie ausführen möchten, und klicken Sie dann auf **In horizontaler Hochskalierung ausführen**.

2. Auswählen von Paketen und Festlegen der Optionen

    Auf der Seite **Paketauswahl** wählen Sie mehrere auszuführende Pakete aus, und legen Sie für jedes Paket die Umgebung, die Parameter, die Verbindungs-Manager und die erweiterten Optionen fest. Klicken Sie auf ein Paket, um diese Optionen festzulegen.
    
    Auf der Registerkarte **Erweitert** legen Sie die für horizontale Hochskalierung verwendete Option **Wiederholungsanzahl**fest. Hiermit wird festgelegt, wie oft das Ausführen eines Pakets versucht wird, wenn ein Fehler auftritt.

    > [!Note]
    > Die **speichern bei Fehlern** Option wird nur wirksam, wenn das Scale-Out-Worker-Dienst-Konto ein Administrator des lokalen Computers ist.

3. Auswählen von Computern

    Auf der Seite **Computerauswahl** wählen Sie die Computer mit Worker für horizontales Hochskalieren aus, auf denen die Pakete ausgeführt werden sollen. Standardmäßig können die Pakete auf jedem Computer ausgeführt werden. 

   > [!Note] 
   > Die Pakete werden mit den Anmeldeinformationen der Benutzerkonten der Dienste für Worker für horizontales Hochskalieren ausgeführt, die auf der Seite **Computerauswahl** angezeigt werden. Standardmäßig ist dies das Konto „NT-Dienst\SSISScaleOutWorker140“. Es bietet sich an, dass Sie zu Ihren entsprechenden eigenen Konten wechseln.

   >[!WARNING]
   >Ausgelöst von verschiedenen Benutzern auf der gleichen Arbeitsthread paketausführungen werden mit demselben Konto ausgeführt. Es gibt keine Sicherheitsgrenze zwischen ihnen. 

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

## <a name="set-default-execution-mode"></a>Set-Standard-Ausführungsmodus
Zum Festlegen der Standardmodus für die Ausführung auf "Horizontal skalieren" Maustaste die **SSISDB** Knoten im Objekt-Explorer von SSMS, und wählen Sie **Eigenschaften**.
In der **Katalog Eigenschaften** Dialog, Set **Ausführungsmodus für den serverweiten Standardwert** auf **horizontal skalieren**.

Nach dieser Einstellung ist nicht erforderlich, geben Sie die  **@runinscaleout**  -Parameter für [Catalog]. [ Create_execution]. Ausführungen werden in horizontal skalieren automatisch ausgeführt. 

![EXE-Modus](media\exe-mode.PNG)

Um Standardausführungsmodus wieder in den nicht - horizontal skalieren Modus zu wechseln, legen Sie nur **Ausführungsmodus für den serverweiten Standardwert** auf **Server**.

## <a name="run-package-in-sql-agent-job"></a>Ausführen des Pakets in SQL-Agent-Auftrag
In Sql-Agent-Auftrag können Sie auswählen, um ein SSIS-Paket als einen Schritt des Auftrags auszuführen. Zum Ausführen des Pakets in horizontal skalieren, können Sie die oben genannten Standardausführungsmodus nutzen. Nach der Einstellung der Standard-Ausführungsmodus auf "Horizontal skalieren" werden Pakete in Sql-Agent-Aufträge in horizontal skalieren ausgeführt werden.


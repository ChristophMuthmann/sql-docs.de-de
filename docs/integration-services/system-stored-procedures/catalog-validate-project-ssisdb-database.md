---
title: Catalog. validate_project (SSISDB-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 5270689a-46d4-4847-b41f-3bed1899e955
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 83439015694f4235af4a67e994e916651ec63cc1
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="catalogvalidateproject-ssisdb-database"></a>catalog.validate_project (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Überprüft asynchron ein Projekt in der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
## <a name="syntax"></a>Syntax  
  
```sql
catalog.validate_project [ @folder_name = ] folder_name  
    , [ @project_name = ] project_name  
    , [ @validate_type = ] validate_type  
    , [ @validation_id = ] validation_id OUTPUT  
 [  , [ @use32bitruntime = ] use32bitruntime ]  
 [  , [ @target_environment = ] target_environment ]  
 [  , [ @reference_id = ] reference_id ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ @folder_name =] *Ordnername*  
 Der Name eines Ordners, der das Projekt enthält. Der *folder_name* ist **nvarchar(128)**.  
  
 [ @project_name =] *Project_name*  
 Der Name des Projekts. Der *project_name* ist **nvarchar(128)**.  
  
 [ @validate_type =] *Validate_type*  
 Gibt den Typ der auszuführenden Überprüfung an. Führen Sie mithilfe des Zeichens `F` eine vollständige Überprüfung aus. Die *Validate_type* ist **char(1)**.  
  
 [ @validation_id =] *Validation_id*  
 Gibt den eindeutigen Bezeichner (ID) der Überprüfung zurück. Die *Validation_id* ist **"bigint"**.  
  
 [ @use32bitruntime =] *use32bitruntime*  
 Gibt an, ob die 32-Bit-Laufzeit verwendet werden soll, um das Paket unter einem 64-Bit-Betriebssystem auszuführen. Verwenden Sie den Wert des `1` zum Ausführen des Pakets mit der 32-Bit-Laufzeit, wenn auf einem 64-Bit-Betriebssystem ausgeführt wird. Verwenden Sie den Wert `0`, um das Paket mit der 64-Bit-Laufzeit auszuführen, wenn die Ausführung unter einem 64-Bit-Betriebssystem erfolgt. Dieser Parameter ist optional. Die *use32bitruntime* ist **Bit**.  
  
 [ @environment_scope =] *Environment_scope*  
 Gibt die Umgebungsverweise an, die bei der Überprüfung beachtet werden. Wenn der Wert `A` ist, werden alle dem Projekt zugeordneten Umgebungsverweise in die Überprüfung eingeschlossen. Wenn der Wert `S` ist, wird nur ein einzelner Umgebungsverweis eingeschlossen. Wenn der Wert `D` ist, werden keine Umgebungsverweise eingeschlossen, und jeder Parameter muss für eine erfolgreiche Überprüfung über einen Standardliteralwert verfügen. Dieser Parameter ist optional. Das Zeichen `D` wird standardmäßig verwendet. Die *Environment_scope* ist **Char(1)**.  
  
 [ @reference_id =] *Reference_id*  
 Die eindeutige ID des Umgebungsverweises. Dieser Parameter ist erforderlich, nur, wenn ein einzelner umgebungsverweis in die Überprüfung eingeschlossen wird beim *Environment_scope* ist `S`. Der *reference_id* ist **bigint**.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg)  
  
## <a name="result-sets"></a>Resultsets  
 Die Ausgabe der Überprüfungsschritte wird als unterschiedliche Abschnitte des Resultsets zurückgegeben.  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   READ-Berechtigungen für das Projekt und ggf. READ-Berechtigungen für die Umgebungen, auf die verwiesen wird  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 In der folgenden Liste werden einige Bedingungen angegeben, die möglicherweise einen Fehler oder eine Warnung auslösen:  
  
-   Die Überprüfung schlägt für ein oder mehrere Pakete im Projekt fehl.  
  
-   Die Überprüfung schlägt fehl, wenn eine oder mehrere der in die Überprüfung eingeschlossenen Umgebungen, auf die verwiesen wird, keine Variablen enthalten, auf die verwiesen wird.  
  
-   Der angegebene Überprüfungstyp ist ungültig.  
  
-   Der Projektname oder die Umgebungsverweis-ID ist ungültig.  
  
-   Der Benutzer verfügt nicht über die entsprechenden Berechtigungen.  
  
## <a name="remarks"></a>Hinweise  
 Die Überprüfung erleichtert das Identifizieren von Problemen, die das erfolgreiche Ausführen der Pakete im Projekt verhindern. Verwenden der [catalog.validations](../../integration-services/system-views/catalog-validations-ssisdb-database.md) oder [catalog.operations](../../integration-services/system-views/catalog-operations-ssisdb-database.md) Ansichten zum Überwachen von Überprüfungsstatus.  
  
 In der Überprüfung können nur Umgebungen verwendet werden, auf die vom Benutzer zugegriffen werden kann. Die Ausgabe der Überprüfung wird als Resultset an den Client gesendet.  
  
 In dieser Version unterstützt die Projektüberprüfung keine Abhängigkeitsüberprüfung.  
  
 Eine vollständige Überprüfung bestätigt, dass alle Umgebungsvariablen, auf die verwiesen wird, in den in die Überprüfung eingeschlossenen Umgebungen, auf die verwiesen wird, vorhanden sind. In den Ergebnissen der vollständigen Überprüfung werden Umgebungsverweise aufgeführt, die ungültig sind, sowie Umgebungsvariablen, auf die verwiesen wird und die in keiner der in die Überprüfung eingeschlossenen Umgebungen, auf die verwiesen wird, gefunden werden konnten.  
  
  

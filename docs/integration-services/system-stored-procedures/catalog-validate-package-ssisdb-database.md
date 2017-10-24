---
title: Catalog. validate_package (SSISDB-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- validate_package stored procedure [Integration Services]
- catalog.validate_package stored procedure [Integration Services]
ms.assetid: 0dc03df1-b793-408f-af4c-c11188729abf
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 869b758e3ac922762c293eb8aa9a9537a4397bd6
ms.contentlocale: de-de
ms.lasthandoff: 10/20/2017

---
# <a name="catalogvalidatepackage-ssisdb-database"></a>catalog.validate_package (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Überprüft asynchron ein Paket im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
## <a name="syntax"></a>Syntax  
  
```sql
catalog.validate_package [ @folder_name = ] folder_name  
    , [ @project_name = ] project_name  
    , [ @package_name = ] package_name  
    , [ @validation_id = ] validation_id OUTPUT  
 [  , [ @use32bitruntime = ] use32bitruntime ]  
 [  , [ @target_environment = ] target_environment ]  
 [  , [ @reference_id = ] reference_id ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ @folder_name =] *Ordnername*  
 Der Name des Ordners, der das Paket enthält. Der *folder_name* ist **nvarchar(128)**.  
  
 [ @project_name =] *Project_name*  
 Der Name des Projekts, das das Paket enthält. Der *project_name* ist **nvarchar(128)**.  
  
 [ @package_name =] *Paketname*  
 Der Name des Pakets. Der *package_name* ist **nvarchar(260)**.  
  
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
 Keine  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   READ-Berechtigungen für das Projekt und ggf. READ-Berechtigungen für die Umgebungen, auf die verwiesen wird  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 In der folgenden Liste werden einige Bedingungen beschrieben, die möglicherweise einen Fehler oder eine Warnung auslösen:  
  
-   Der Projekt- oder Paketname ist nicht gültig.  
  
-   Der Benutzer verfügt nicht über die entsprechenden Berechtigungen.  
  
-   Eine oder mehrere der in die Überprüfung eingeschlossenen Umgebungen, auf die verwiesen wird, enthalten keine Variablen, auf die verwiesen wird.  
  
-   Die Überprüfung des Pakets schlägt fehl.  
  
-   Die Umgebung, auf die verwiesen wird, ist nicht vorhanden.  
  
-   In den in der Überprüfung enthaltenen Umgebungen, auf die verwiesen wird, können Variablen nicht gefunden werden, auf die verwiesen wird.  
  
-   In den Paketparametern wird auf Variablen verwiesen, aber in der Überprüfung wurden keine Umgebungen eingeschlossen, auf die verwiesen wird.  
  
## <a name="remarks"></a>Hinweise  
 Die Überprüfung erleichtert das Probleme zu identifizieren, die das Paket für die erfolgreiche Ausführung verhindern kann. Verwenden der [catalog.validations](../../integration-services/system-views/catalog-validations-ssisdb-database.md) oder [catalog.operations](../../integration-services/system-views/catalog-operations-ssisdb-database.md) Ansichten zum Überwachen von Überprüfungsstatus.  
  
  

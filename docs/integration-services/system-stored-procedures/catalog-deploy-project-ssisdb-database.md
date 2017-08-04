---
title: Catalog. deploy_project (SSISDB-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 2e3439b4-7226-4b61-a993-7a1d161eac7e
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a2e3655bedbb24f2174a62c8792cd168e7642592
ms.openlocfilehash: 9871d26467a300119c742d398ff88f87825d930c
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="catalogdeployproject-ssisdb-database"></a>catalog.deploy_project (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Stellt ein Projekt in einem Ordner im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog bereit oder aktualisiert ein vorhandenes Projekt, das zuvor bereitgestellt wurde.  
  
## <a name="syntax"></a>Syntax  
  
```tsql  
deploy_project [ @folder_name = ] folder_name   
      , [ @project_name = ] project_name   
      , [ @project_stream = ] projectstream   
    [ , [@operation_id ] = operation_id OUTPUT ]   
```  
  
## <a name="arguments"></a>Argumente  
 [ @folder_name =] *Ordnername*  
 Der Name des Ordners, in dem das Projekt bereitgestellt wird. Der *folder_name* ist **nvarchar(128)**.  
  
 [ @project_name =] *Project_name*  
 Der Name des neuen oder aktualisierten Projekts im Ordner. Der *project_name* ist **nvarchar(128)**.  
  
 [ @projectstream =] *Projectstream*  
 Die binären Inhalte ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] projektbereitstellungsdatei (Erweiterung .ispac).  
  
 Sie können eine SELECT-Anweisung mit der OPENROWSET-Funktion und dem BULK-Rowsetanbieter verwenden, um binäre Dateiinhalte abzurufen. Ein Beispiel finden Sie unter [Bereitstellen von Integration Services (SSIS)-Projekten und Paketen](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md). Weitere Informationen zu OPENROWSET finden Sie unter [OPENROWSET &#40; Transact-SQL &#41; ](../../t-sql/functions/openrowset-transact-sql.md).  
  
 *projectstream* ist **varbinary(MAX)**.  
  
 [ @operation_id =] *Operation_id*  
 Gibt den eindeutigen Bezeichner für den Bereitstellungsvorgang zurück. Der *operation_id* ist **bigint**.  
  
## <a name="return-code-value"></a>Rückgabecodewert  
 0 (Erfolg)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   CREATE_OBJECTS-Berechtigungen für den Ordner, um ein neues Projekt bereitzustellen, oder MODIFY-Berechtigungen für das Projekt, um ein Projekt zu aktualisieren  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 In der folgenden Liste werden Bedingungen beschrieben, die möglicherweise bewirken, dass diese gespeicherte Prozedur einen Fehler auslöst:  
  
-   Ein Parameter verweist auf ein Objekt, das nicht vorhanden ist, ein Parameter versucht, ein bereits vorhandenes Objekt zu erstellen, oder ein Parameter ist aus anderen Gründen ungültig  
  
-   Der Wert des Parameters  *@project_name*  stimmt nicht mit den Namen des Projekts in der Bereitstellungsdatei überein  
  
-   Der Benutzer verfügt nicht über ausreichende Berechtigungen  
  
## <a name="remarks"></a>Hinweise  
 Während einer Projektbereitstellung oder eines Projektupdates überprüft die gespeicherte Prozedur nicht die Schutzebene einzelner Pakete im Projekt.  
  
  

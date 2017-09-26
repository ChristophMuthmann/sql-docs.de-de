---
title: Catalog. set_object_parameter_value (SSISDB-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: fb887543-f92f-404d-9495-a1dd23a6716e
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9c27cff7ad828ab5c19183febd2ad562d5c9b925
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="catalogsetobjectparametervalue-ssisdb-database"></a>catalog.set_object_parameter_value (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Legt den Wert eines Parameters im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog fest. Ordnet einer Umgebungsvariablen den Wert zu oder weist einen Literalwert zu, der standardmäßig verwendet wird, wenn keine anderen Werte zugewiesen werden.  
  
## <a name="syntax"></a>Syntax  
  
```tsql  
set_object_parameter_value [ @object_type = ] object_type   
    , [ @folder_name = ] folder_name   
    , [ @project_name = ] project_name   
    , [ @parameter_name = ] parameter _name   
    , [ @parameter_value = ] parameter_value   
 [  , [ @object_name = ] object_name ]  
 [  , [ @value_type = ] value_type ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ @object_type =] *Object_type*  
 Der Typ des Parameters. Verwenden Sie den Wert `20` , um einen Projektparameter anzugeben, oder den Wert `30` , um einen Paketparameter anzugeben. Der *object_type* ist **smallInt**.  
  
 [ @folder_name =] *Ordnername*  
 Der Name des Ordners, der den Parameter enthält. Der *folder_name* ist **nvarchar(128)**.  
  
 [ @project_name =] *Project_name*  
 Der Name des Projekts, das den Parameter enthält. Der *project_name* ist **nvarchar(128)**.  
  
 [ @parameter_name =] *Parameter_name*  
 Der Name des Parameters. Der *parameter_name* ist **nvarchar(128)**.  
  
 [ @parameter_value =] *Parameter_value*  
 Der Wert des Parameters. Der *parameter_value* ist **sql_variant**.  
  
 [ @object_name =] *Object_name*  
 Der Name des Pakets. Dieses Argument ist erforderlich, wenn der Parameter ein Paketparameter ist. Der *object_name* ist **nvarchar(260)**.  
  
 [ @value_type =] *Value_type*  
 Der Typ des Parameterwerts. Verwenden Sie das Zeichen `V` , um anzugeben, dass *parameter_value* ein Literalwert ist, der standardmäßig verwendet wird, wenn vor der Ausführung keine anderen Werte zugewiesen werden. Verwenden Sie das Zeichen `R` , um anzugeben, dass *parameter_value* ein Wert ist, auf den verwiesen wird und der auf den Namen einer Umgebungsvariablen festgelegt wurde. Dieses Argument ist optional. Das Zeichen `V` wird standardmäßig verwendet. Der *value_type* ist **char(1)**.  
  
## <a name="return-code-value"></a>Rückgabecodewert  
 0 (Erfolg)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   READ-Berechtigung und MODIFY-Berechtigung für das Projekt  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 In der folgenden Liste werden Bedingungen beschrieben, die möglicherweise bewirken, dass die gespeicherte Prozedur einen Fehler auslöst:  
  
-   Der Parametertyp ist ungültig.  
  
-   Der Projektname ist ungültig.  
  
-   Für Paketparameter ist der Paketname ungültig.  
  
-   Der Werttyp ist ungültig.  
  
-   Der Benutzer verfügt nicht über die entsprechenden Berechtigungen.  
  
## <a name="remarks"></a>Hinweise  
  
-   Wenn kein *value_type* angegeben ist, wird standardmäßig ein Literalwert für *parameter_value* verwendet. Wenn ein Literalwert verwendet wird, die *Value_set* in der [Object_parameters](../../integration-services/system-views/catalog-object-parameters-ssisdb-database.md) Ansicht festgelegt ist, um `1`. Ein NULL-Parameterwert ist nicht zulässig.  
  
-   Wenn *value_type* das Zeichen `R`enthält, das einen Wert bezeichnet, auf den verwiesen wird, verweist *parameter_value* auf den Namen einer Umgebungsvariablen.  
  
-   Für `20` kann der Wert *object_type* verwendet werden, um einen Projektparameter anzugeben. In diesem Fall ist für *object_name* kein Wert erforderlich, und jeder für *object_name* angegebene Wert wird ignoriert. Dieser Wert wird verwendet, wenn der Benutzer einen Projektparameter festlegen möchte.  
  
-   Für `30` kann der Wert *object_type* verwendet werden, um einen Paketparameter anzugeben. In diesem Fall wird ein Wert für *object_name* verwendet, um das entsprechende Paket anzugeben. Wenn *object_name* nicht angegeben wird, gibt die gespeicherte Prozedur einen Fehler zurück und wird beendet.  
  
  

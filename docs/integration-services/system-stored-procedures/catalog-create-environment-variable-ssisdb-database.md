---
title: Catalog. create_environment_variable (SSISDB-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 91ed017b-6567-4bf2-b9f1-e2b5c70a5343
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 5636651cccbb43c6c1627d1f28eccd9b3f9b5b0d
ms.contentlocale: de-de
ms.lasthandoff: 10/20/2017

---
# <a name="catalogcreateenvironmentvariable-ssisdb-database"></a>catalog.create_environment_variable (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Erstellen Sie eine Umgebungsvariable in der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
## <a name="syntax"></a>Syntax  
  
```sql  
catalog.create_environment_variable [@folder_name =] folder_name  
    , [@environment_name =] environment_name  
    , [@variable_name =] variable_name  
    , [@data_type =] data_type  
    , [@sensitive =] sensitive  
    , [@value =] value  
    , [@description =] description  
```  
  
## <a name="arguments"></a>Argumente  
 [@folder_name =] *Ordnername*  
 Der Name des Ordners, der die Umgebung enthält. Der *folder_name* ist **nvarchar(128)**.  
  
 [@environment_name =] *Environment_name*  
 Der Name der Umgebung. Der *environment_name* ist **nvarchar(128)**.  
  
 [@variable_name =] *Variable_name*  
 Der Name der Umgebungsvariablen. Der *variable_name* ist **nvarchar(128)**.  
  
 [@data_type =] *Data_type*  
 Der Datentyp der Variablen. Unterstützt die folgenden Anweisungstypen Variable Umgebungsdaten **booleschen**, **Byte**, **"DateTime"**, **doppelte**, **Int16**, **Int32**, **Int64**, **einzelne**, **Zeichenfolge**, **UInt32**, und  **UInt64**. Nicht unterstützte umgebungsvariablendatentypen sind **Char**, **DBNull**, **Objekt**, und **"SByte"**. Der Datentyp der *Data_type* Parameter ist **vom Datentyp nvarchar(128)**.  
  
 [@sensitive =] *vertrauliche*  
 Gibt an, ob die Variable einen vertraulichen Wert enthält. Verwenden Sie den Wert `1` , um anzugeben, dass der Wert der Umgebungsvariablen vertraulich ist, oder den Wert `0` , um anzugeben, dass er nicht vertraulich ist. Ein vertraulicher Wert wird verschlüsselt, wenn er gespeichert wird. Ein Wert, der nicht vertraulich ist, wird als nur-Text gespeichert. *Vertrauliche* ist **Bit**.  
  
 [@value =] *Wert*  
 Der Wert der Umgebungsvariablen. Der *value* ist **sql_variant**.  
  
 [@description =] *Beschreibung*  
 Die Beschreibung der Umgebungsvariablen. Die *Wert* ist **nvarchar(1024)**.  
  
## <a name="return-code-value"></a>Rückgabecodewert  
 0 (Erfolg)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   READ-Berechtigung und MODIFY-Berechtigung für die Umgebung  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 In der folgenden Liste werden einige Bedingungen beschrieben, die möglicherweise einen Fehler oder eine Warnung auslösen:  
  
-   Der Name des Ordners, der Umgebung oder der Umgebungsvariablen ist ungültig.  
  
-   Der Variablenname ist bereits in der Umgebung vorhanden.  
  
-   Der Benutzer verfügt nicht über die entsprechenden Berechtigungen.  
  
## <a name="remarks"></a>Hinweise  
 Mit einer Umgebungsvariablen kann zur Ausführung eines Pakets einem Projektparameter oder Paketparameter effizient ein Wert zugewiesen werden. Umgebungsvariablen ermöglichen die Organisation von Parameterwerten. Variablennamen müssen innerhalb einer Umgebung eindeutig sein.  
  
 Die gespeicherte Prozedur überprüft den Datentyp der Variablen, um sicherzustellen, dass sie vom [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog unterstützt wird.  
  
> [!TIP]  
>  Erwägen Sie die **Int16** -Datentyp im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] statt des nicht unterstützten **"SByte"** -Datentyp.  
  
 An diese gespeicherte Prozedur übergebene Wert der *Wert* Parameter konvertiert wird, aus einer [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Datentyp, ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datentyp gemäß der folgenden Tabelle:  
  
|Integration Services-Datentyp|SQL Server-Datentyp|  
|------------------------------------|--------------------------|  
|**Boolean**|**bit**|  
|**Byte**|**binäre**, **Varbinary**|  
|**DateTime**|**"DateTime"**, **datetime2**, **"DateTimeOffset"**, **Smalldatetime**|  
|**Double**|Genaue numerische: **decimal**, **numerischen**; Ungefähre numerische: **"float"**, **real**|  
|**Int16**|**smallint**|  
|**Int32**|**int**|  
|**Int64-Typ**|**bigint**|  
|**Single**|Genaue numerische: **decimal**, **numerischen**; Ungefähre numerische: **"float"**, **real**|  
|**String**|**Varchar**, **Nvarchar**, **Char**|  
|**UInt32**|**Int** (**Int** ist die beste Entsprechung zu **Uint32**.)|  
|**UInt64**|**"bigint"** (**Int** ist die beste Entsprechung zu **Uint64**.)|  
  
  

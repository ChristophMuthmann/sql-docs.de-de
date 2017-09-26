---
title: Catalog. create_folder (SSISDB-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 06fb3549-e970-4ca2-a61f-59affb9c6dcc
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: df7b4750e813601b7e4d2a02c8f1f277f1000d9c
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="catalogcreatefolder-ssisdb-database"></a>catalog.create_folder (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Erstellt einen Ordner im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
## <a name="syntax"></a>Syntax  
  
```tsql  
create_folder [ @folder_name = ] folder_name, [ @folder_id = ] folder_id OUTPUT  
```  
  
## <a name="arguments"></a>Argumente  
 [ @folder_name =] *Ordnername*  
 Der Name des neuen Ordners. Der *folder_name* ist **nvarchar(128)**.  
  
 [ @folder_name =] *Folder_id*  
 Der eindeutige Bezeichner (ID) des Ordners. Der *folder_id* ist **bigint**.  
  
## <a name="return-code-value"></a>Rückgabecodewert  
 Der Ordnerbezeichner wird zurückgegeben.  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 Die gespeicherte Prozedur gibt einen Fehler zurück, wenn bereits ein Ordner mit demselben Namen vorhanden ist.  
  
  

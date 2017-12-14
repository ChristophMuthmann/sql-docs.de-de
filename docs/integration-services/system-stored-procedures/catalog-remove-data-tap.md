---
title: catalog.remove_data_tap | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: b77db3e6-478c-441a-a838-82c4de750275
caps.latest.revision: "8"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 28339c0762182397a266fa42abf6411a3dd56ef4
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="catalogremovedatatap"></a>catalog.remove_data_tap
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Entfernt eine Datenabzweigung aus einer Komponentenausgabe, die aktuell ausgeführt wird. Der eindeutige Bezeichner für die Datenabzweigung ist einer Instanz der Ausführung zugeordnet.  
  
## <a name="syntax"></a>Syntax  
  
```sql  
catalog.remove_data_tap [ @data_tap_id = ] data_tap_id  
```  
  
## <a name="arguments"></a>Argumente  
 [ @data_tap_id = ] *data_tap_id*  
 Der eindeutige Bezeichner für die Datenabzweigung, die mit der gespeicherten Prozedur "catalog.add_data_tap" erstellt wird. Der *data_tap_id* ist **bigint**.  
  
## <a name="remarks"></a>Hinweise  
 Wenn ein Paket mehrere Datenflusstasks mit dem gleichen Namen enthält, wird die Datenabzweigung dem ersten Datenflusstask mit dem angegebenen Namen hinzugefügt.  
  
## <a name="return-codes"></a>Rückgabecodes  
 0 (Erfolg)  
  
 Wenn die gespeicherte Prozedur fehlschlägt, wird ein Fehler ausgelöst.  
  
## <a name="result-set"></a>Resultset  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 Um Datenabzweigungen zu entfernen, muss die Ausführungsinstanz den Status „Erstellt“ (einen Wert von 1 in der Spalte **Zustand** der Sicht [catalog.operations &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md)) aufweisen.  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   MODIFY-Berechtigungen für die Instanz der Ausführung  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 Die folgende Liste beschreibt Bedingungen, unter denen die gespeicherte Prozedur fehlschlägt.  
  
-   Der Benutzer verfügt nicht über MODIFY-Berechtigungen.  
  
## <a name="see-also"></a>Siehe auch  
 [catalog.add_data_tap](../../integration-services/system-stored-procedures/catalog-add-data-tap.md)   
 [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md)  
  
  

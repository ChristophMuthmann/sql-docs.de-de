---
title: create_execution_dump auf | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 91319b0b-5536-4ab4-a403-9559ed9dd177
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b05e1b46845c0a2b5ee47b94dc239d79d4a12a17
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="catalogcreateexecutiondump"></a>catalog.create_execution_dump
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Hält ein aktuell ausgeführtes Paket an und erzeugt eine Dumpdatei. Die Datei befindet sich in der  *\<Laufwerk >*: Ordner "\Programme\Microsoft SQL Server\130\Shared\ErrorDumps".  
  
## <a name="syntax"></a>Syntax  
  
```sql  
catalog.create_execution_dump [ @execution_id = ] execution_id  
  
```  
  
## <a name="arguments"></a>Argumente  
 [ @execution_id =] *Execution_id*  
 Die Ausführungs-ID für das ausgeführte Paket. Der *execution_id* ist **bigint**.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird das ausgeführte Paket mit der Ausführungs-ID 88 aufgefordert, eine Dumpdatei zu erstellen.  
  
```sql
EXEC create_execution_dump @execution_id = 88  
```  
  
## <a name="return-codes"></a>Rückgabecodes  
 0 (Erfolg)  
  
 Wenn die gespeicherte Prozedur fehlschlägt, wird ein Fehler ausgelöst.  
  
## <a name="result-set"></a>Resultset  
 Keine  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur muss Benutzer Mitglied der **Ssis_admin** -Datenbankrolle.  
  
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 Die folgende Liste beschreibt Bedingungen, unter denen die gespeicherte Prozedur fehlschlägt.  
  
-   Eine ungültige Ausführungs-ID wurde angegeben.  
  
-   Das Paket ist bereits abgeschlossen.  
  
-   Das Paket erstellt gerade eine Dumpdatei.  
  
## <a name="see-also"></a>Siehe auch  
 [Generieren von Dumpdateien für die Paketausführung](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  


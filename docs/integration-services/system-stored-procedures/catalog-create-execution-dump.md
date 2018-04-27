---
title: catalog.create_execution_dump | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 91319b0b-5536-4ab4-a403-9559ed9dd177
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2f3996455b61bfbe0bffe9e7199f5ecf87d4690a
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="catalogcreateexecutiondump"></a>catalog.create_execution_dump
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Hält ein aktuell ausgeführtes Paket an und erzeugt eine Dumpdatei. Die Datei wird im Ordner „*\<Laufwerk>*:\Programme\Microsoft SQL Server\130\Shared\ErrorDumps“ gespeichert.  
  
## <a name="syntax"></a>Syntax  
  
```sql  
catalog.create_execution_dump [ @execution_id = ] execution_id  
  
```  
  
## <a name="arguments"></a>Argumente  
 [ @execution_id = ] *execution_id*  
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
 InclusionThresholdSetting  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert, dass der Benutzer Mitglied der Datenbankrolle **ssis_admin** ist.  
  
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 Die folgende Liste beschreibt Bedingungen, unter denen die gespeicherte Prozedur fehlschlägt.  
  
-   Eine ungültige Ausführungs-ID wurde angegeben.  
  
-   Das Paket ist bereits abgeschlossen.  
  
-   Das Paket erstellt gerade eine Dumpdatei.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Generieren von Dumpdateien für die Paketausführung](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  

---
title: catalog.create_execution_dump | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 91319b0b-5536-4ab4-a403-9559ed9dd177
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f13a1c0730b01280896b8c759aa401cf10ba875c
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
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
  
  

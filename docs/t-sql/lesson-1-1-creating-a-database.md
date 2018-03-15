---
title: Erstellen einer Datenbank (Tutorial) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: t-sql
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- tutorial creating a database
ms.assetid: e1e2c83f-dfad-4bb8-aa7a-09d3f69517ae
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 55a63275dc9e7d130614b5dece07b7f74edd53ca
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="lesson-1-1---creating-a-database"></a>Lektion 1–1: Erstellen einer Datenbank
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] Wie viele [!INCLUDE[tsql](../includes/tsql-md.md)]-Anweisungen verfügt auch die CREATE DATABASE-Anweisung über einen erforderlichen Parameter: den Namen der Datenbank. CREATE DATABASE verfügt auch über viele optionale Parameter wie den Speicherort auf dem Datenträger, an den Sie die Datenbankdateien kopieren möchten. Wenn Sie CREATE DATABASE ohne optionale Parameter ausführen, werden von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Standardwerte für viele dieser Parameter verwendet. In diesem Lernprogramm werden nur wenige der optionalen Syntaxparameter verwendet.  
  
### <a name="to-create-a-database"></a>So erstellen Sie eine Datenbank  
  
1.  Geben Sie in einem Fenster des Abfrage-Editors den folgenden Code ein, aber führen Sie ihn nicht aus:  
  
    ```  
    CREATE DATABASE TestData  
    GO  
    ```  
  
2.  Verwenden Sie den Zeiger, um die Wörter `CREATE DATABASE`auszuwählen, und drücken Sie dann **F1**. Das CREATE DATABASE-Thema in der SQL Server-Onlinedokumentation sollte geöffnet werden. Sie können dieses Verfahren verwenden, um die vollständige Syntax für CREATE DATABASE und für die anderen in diesem Lernprogramm verwendeten Anweisungen zu finden.  
  
3.  Drücken Sie im Abfrage-Editor **F5** , um die Anweisung auszuführen und eine Datenbank mit Namen `TestData`zu erstellen.  
  
Wenn Sie eine Datenbank erstellen, wird von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] eine Kopie der **model** -Datenbank erstellt und die Kopie in den Namen der Datenbank umbenannt. Dieser Vorgang dauert nur einige Sekunden, es sei denn, Sie geben eine große Anfangsgröße der Datenbank als optionalen Parameter an.  
  
> [!NOTE]  
> Das GO-Schlüsselwort trennt Anweisungen, wenn mehrere Anweisungen in einem einzelnen Batch gesendet werden. GO ist optional, wenn der Batch nur eine Anweisung enthält.  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in dieser Lektion  
[Erstellen einer Tabelle &#40;Tutorial&#41;](../t-sql/lesson-1-2-creating-a-table.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
  
  

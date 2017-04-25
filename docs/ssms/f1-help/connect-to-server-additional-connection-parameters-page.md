---
title: "Verbindung mit Server herstellen (Seite „Zusätzliche Verbindungsparameter“) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.connecttoserver.options.registeredservers.f1
ms.assetid: ba34b01a-6289-4eb8-8341-fa3d9ec87b3f
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7befc61bcf4a973aa0593e476bcce76f5751f40b
ms.lasthandoff: 04/11/2017

---
# <a name="connect-to-server-additional-connection-parameters-page"></a>Verbindung mit Server herstellen (Seite 'Zusätzliche Verbindungsparameter')
Im Dialogfeld **Verbinden mit** von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] werden die gängigsten Verbindungszeichenfolgenwerte als Optionen angezeigt. Mithilfe der Seite **Zusätzliche Verbindungsparameter** können Sie der Verbindungszeichenfolge weitere Verbindungsparameter hinzufügen.  
  
-   Zusätzliche Verbindungsparameter können beliebige ODBC-Verbindungsparameter sein.  
  
-   Zusätzliche Verbindungsparameter sollten im Format **;Parameter1=Wert1;Parameter2=Wert2**hinzugefügt werden.  
  
-   Parameter, die mithilfe der Seite **Zusätzliche Verbindungsparameter** hinzugefügt werden, werden den Parametern hinzugefügt, die mithilfe der Optionen des Dialogfelds **Verbinden mit** ausgewählt wurden.  
  
-   Durch die letzte Instanz eines Parameters werden alle vorherigen Instanzen des Parameters überschrieben. Parameter, die mithilfe der Seite **Zusätzliche Verbindungsparameter** hinzugefügt werden, orientieren sich an den Parametern, die auf den Registerkarten **Anmeldung** und **Verbindungseigenschaften** bereitgestellt sind, und ersetzen diese. Wird auf der Registerkarte **Anmeldung** beispielsweise **SERVER1** als **Servername**bereitgestellt, und enthält die Seite **Zusätzliche Verbindungsparameter** die Option **;SERVER=SERVER2**, wird die Verbindung mit **SERVER2**hergestellt.  
  
-   Parameter, die mithilfe der Seite **Zusätzliche Verbindungsparameter** hinzugefügt wurden, werden immer als Nur-Text übergeben.  
  
    > [!IMPORTANT]  
    > Auf der Seite **Zusätzliche Verbindungsparameter** dürfen keine Anmeldeinformationen und Kennwörter eingefügt werden. Sie werden nicht verschlüsselt, wenn sie über das Netzwerk übergeben werden. Verwenden Sie stattdessen die Registerkarte **Anmeldung** .  
  
## <a name="task-list"></a>Aufgabenliste  
  
### <a name="to-show-the-additional-connection-parameters-page"></a>So zeigen Sie die Seite 'Zusätzliche Verbindungsparameter' an  
  
1.  Zeigen Sie in [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)]im Menü **Abfrage** auf **Verbindung**, und klicken Sie dann auf **Verbinden**.  
  
2.  Klicken Sie im Dialogfeld **Verbinden mit** auf **Optionen**, und klicken Sie dann auf die Registerkarte **Zusätzliche Verbindungsparameter** .  
  
## <a name="examples"></a>Beispiele  
  
### <a name="example-a-connecting-to-the-database-engine"></a>Beispiel A: Herstellen einer Verbindung mit dem Datenbankmodul  
Um eine Verbindung mit der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] -Datenbank auf einem Server mit dem Namen ACCOUNTING herzustellen, geben Sie auf der Seite **Zusätzliche Verbindungsparameter** Folgendes ein:  
  
```  
;SERVER=ACCOUNTING;DATABASE=AdventureWorks2012  
```  
  
### <a name="example-b-connecting-to-analysis-services"></a>Beispiel B: Herstellen einer Verbindung mit Analysis Services  
Um eine Verbindung mit den Analysis-Servern herzustellen und zu bewirken, dass alle Partitionen, die Benachrichtigungen überwachen, in Echtzeit abgefragt werden (wobei das Caching umgangen wird), und den Timeoutwert für das Rückschreiben auf 5 festzulegen, geben Sie auf der Seite **Zusätzliche Verbindungsparameter** Folgendes ein:  
  
```  
;Real Time Olap=TRUE;Writeback Timeout=5  
```  
  


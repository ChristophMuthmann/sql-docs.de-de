---
title: Erteilen des Zugriffs auf ein Datenbankobjekt | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- granting access to database objects
ms.assetid: a44d9bbf-f58e-4734-b7f4-eb3b492b777b
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7cc5c15a44f16e4049974ff76095a389348707c7
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-2-4---granting-access-to-a-database-object"></a>Lektion 2-4-gewähren des Zugriffs auf ein Datenbankobjekt
Als Administrator können Sie die SELECT-Anweisung in der **Products** -Tabelle und in der **vw_Names** -Sicht ausführen, und Sie können auch die **pr_Names** -Prozedur ausführen. Mary hingegen ist dazu nicht berechtigt. Verwenden Sie die GRANT-Anweisung, um Mary die erforderlichen Berechtigungen zu erteilen.  
  
### <a name="procedure-title"></a>Titel der Prozedur  
  
1.  Führen Sie die folgende Anweisung aus, um `Mary` die `EXECUTE` -Berechtigung für die gespeicherte Prozedur `pr_Names` zu erteilen.  
  
    ```  
    GRANT EXECUTE ON pr_Names TO Mary;  
    GO  
    ```  
  
In diesem Szenario kann Mary mithilfe der gespeicherten Prozedur nur auf die **Products** -Tabelle zugreifen. Wenn Sie möchten, dass Mary eine SELECT-Anweisung für die Sicht ausführen kann, müssen Sie auch `GRANT SELECT ON vw_Names TO Mary`ausführen. Verwenden Sie die REVOKE-Anweisung, um den Zugriff auf Datenbankobjekte zu entfernen.  
  
> [!NOTE]  
> Wenn der Besitzer der Tabelle, Sicht und gespeicherten Prozedur nicht das gleiche Schema ist, wird die Erteilung von Berechtigungen komplexer.  
  
## <a name="about-grant"></a>Informationen zu GRANT  
Sie müssen über die EXECUTE-Berechtigung verfügen, um eine gespeicherte Prozedur auszuführen. Sie müssen über die SELECT-, INSERT-, UPDATE- und DELETE-Berechtigungen verfügen, um auf Daten zuzugreifen und sie zu ändern. Die GRANT-Anweisung wird auch für andere Berechtigungen wie die zum Erstellen von Tabellen verwendet.  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in der Lektion  
[Zusammenfassung: Konfigurieren von Berechtigungen für Datenbankobjekte](../t-sql/lesson-2-5-summary-configuring-permissions-on-database-objects.md)  
  
## <a name="see-also"></a>Siehe auch  
[GRANT &#40;Transact-SQL&#41;](../t-sql/statements/grant-transact-sql.md)  
[REVOKE &#40;Transact-SQL&#41;](../t-sql/statements/revoke-transact-sql.md)  
  
  
  


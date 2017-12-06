---
title: "Migrieren von Access-Daten in SQLServer – Azure SQL-Datenbank (AccessToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-access
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- bulk loading data
- data, loading into SQL Azure
- data, loading into SQL Server
- migrating databases, loading data
- migrating databases, options
- options, migrating data
- SQL Azure, migrating data into
- SQL Server, migrating data into
ms.assetid: f3b18af7-1af0-499d-a00d-a0af94895625
caps.latest.revision: "17"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8b9e885b397abc05af7ec538eb2ed46c8ba12ea2
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="migrating-access-data-into-sql-server---azure-sql-db-accesstosql"></a>Migrieren von Access-Daten in SQLServer – Azure SQL-Datenbank (AccessToSQL)
Nachdem Sie die Datenbankobjekte, die in erfolgreich erstellt haben [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], Migrieren von Daten aus den Zugriff auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure.  
  
## <a name="setting-migration-options"></a>Einstellungsoptionen für die Migration  
Vor dem Migrieren von Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, überprüfen Sie die Migrationsoptionen Projekt in der **Projekteinstellungen** (Dialogfeld). In diesem Dialogfeld können Sie festlegen, die Batchgröße für die Migration, Tabellensperre, Einschränkung, die zur Überprüfung der Einfügung auslösen, Identität und null-Wert behandeln, und wie Daten behandelt, die außerhalb des dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Bereich. Weitere Informationen finden Sie unter [Projekteinstellungen (Migration)](http://msdn.microsoft.com/en-us/4caebc9c-8680-4b99-a8fa-89c43161c95d).  
  
## <a name="migrating-data"></a>Migrieren von Daten  
Migrieren von Daten eines Massenladevorgangs, die Datenzeilen in Verschiebt [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Transaktionen. Die Anzahl der Zeilen in geladen werden soll [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure in der jeweiligen Transaktion in den projekteinstellungen konfiguriert ist.  
  
Um die Migration der Meldungsansicht sicherstellen Sie, dass im Ausgabebereich angezeigt wird. Ist dies nicht der Fall, auf die **Ansicht** klicken Sie im Menü **Ausgabe**.  
  
**Zum Migrieren von Daten**  
  
1.  Stellen Sie sicher, dass Sie geladen haben, die Zugriff auf Datenbankobjekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure.  
  
2.  Wählen Sie im Metadaten-Explorer für den Zugriff die Objekte, die die Daten enthalten, die Sie migrieren möchten:  
  
    -   Wählen Sie das Kontrollkästchen neben dem Datenbanknamen zur Migration von Daten für eine gesamte Datenbank.  
  
    -   Zum Migrieren von Daten aus einzelnen Tabellen die Datenbank, erweitern Sie dann **Tabellen**, und wählen Sie dann das Kontrollkästchen neben der Tabelle. Deaktivieren Sie das Kontrollkästchen, um Daten aus den einzelnen Tabellen zu unterdrücken.  
  
3.  Mit der rechten Maustaste **Datenbanken** und wählen Sie dann **Migrieren von Daten**.  
  
Sie können auch außerhalb von SSMA mithilfe Migrieren der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **Bcp** Befehlszeilen-Hilfsprogramm oder [!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)]. Weitere Informationen zu diesen Tools finden Sie unter [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Books Online.  
  
## <a name="next-step"></a>Nächster Schritt  
Haben Zugriff datenbankanwendungen, die Sie weiterhin nach der Migration verwenden möchten, verknüpfen Sie die Datenbanktabellen den Zugriff auf die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Tabellen. Weitere Informationen finden Sie unter [Verknüpfen von Microsoft Access-Anwendungen mit SQL Server](http://msdn.microsoft.com/en-us/82374ad2-7737-4164-a489-13261ba393d4).  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Access-Datenbanken zu SQLServer](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
[Einstellung Konvertierung und Migrationsoptionen](http://msdn.microsoft.com/en-us/0a7304df-2f35-4453-96ef-7ac83dea1167)  
  

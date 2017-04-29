---
title: Erstellen von CLR-Triggern | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-dml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- CRL triggers
- DML triggers, CLR triggers
- DDL triggers, CLR triggers
ms.assetid: 31f41703-134d-49fc-9850-76c297351c2c
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: dbe103df7fe4c203373a1fedbeba16a3df39caa0
ms.lasthandoff: 04/11/2017

---
# <a name="create-clr-triggers"></a>Erstellen von CLR-Triggern
  Sie können in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ein Datenbankobjekt erstellen, das in einer Assembly programmiert wird, die in der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -CLR (Common Language Runtime) erstellt wurde. Datenbankobjekte, die das reichhaltige Programmiermodell nutzen können, das von der CLR (Common Language Runtime) bereitgestellt wird, sind z. B. DML-Trigger, DDL-Trigger, gespeicherte Prozeduren, Funktionen, Aggregatfunktionen und Typen.  
  
 Das Erstellen eines CLR-Triggers (DML oder DDL) in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] umfasst folgende Schritte:  
  
-   Definieren des Triggers als Klasse in einer von .NET Framework unterstützten Sprache. Weitere Informationen zum Programmieren von Triggern in der CLR finden Sie unter [CLR-Trigger](http://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c). Kompilieren Sie die Klasse mithilfe des entsprechenden Sprachcompilers, um eine Assembly in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] zu erstellen.  
  
-   Registrieren der Assembly in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe der CREATE ASSEMBLY-Anweisung. Weitere Informationen zum Arbeiten mit Assemblys in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] finden Sie unter [Assemblys &#40;Datenbankmodul&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md).  
  
-   Erstellen Sie den Trigger, der auf die registrierte Assembly verweist.  
  
> [!NOTE]  
>  Bei der Bereitstellung eines SQL Server-Projekts in [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] wird eine Assembly in der Datenbank registriert, die für das Projekt angegeben wurde. Bei der Bereitstellung des Projekts werden in der Datenbank auch CLR-Trigger für alle Methoden erstellt, die mit dem **SqlTrigger** -Attribut versehen sind. Weitere Informationen finden Sie unter [Deploying CLR Database Objects](../../relational-databases/clr-integration/deploying-clr-database-objects.md).  
  
> [!NOTE]  
>  Die Funktion zum Ausführen von CLR-Code ist in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] standardmäßig deaktiviert. Sie können Datenbankobjekte, die auf verwaltete Codemodule verweisen, erstellen, ändern oder löschen. Diese Verweise werden jedoch nur dann in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt, wenn die Option [clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) mithilfe von [sp_configure (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)aktiviert wird.  
  
 **So erstellen, ändern oder löschen Sie eine Assembly**  
  
-   [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
-   [DROP ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  
 **So erstellen Sie einen CLR-Trigger**  
  
-   [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
  
## <a name="see-also"></a>Siehe auch  
 [DML-Trigger](../../relational-databases/triggers/dml-triggers.md)   
 [Programmierkonzepte für die Integration der Common Language Runtime &#40;CLR&#41;](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)   
 [Datenzugriff von CLR-Datenbankobjekten aus](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  

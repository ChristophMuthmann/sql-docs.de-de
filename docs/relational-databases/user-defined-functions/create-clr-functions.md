---
title: Erstellen von CLR-Funktionen | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-udf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- CLR functions [SQL Server]
- user-defined functions [SQL Server], CLR
ms.assetid: a82df075-2243-4e19-bfe1-ae6d65dabd0f
caps.latest.revision: "34"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 99f9daf70ad70f36d4e6435eaf2230c51d171850
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="create-clr-functions"></a>Erstellen von CLR-Funktionen
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Sie können ein Datenbankobjekt in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellen, das in einer Assembly programmiert wird, die in der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -CLR (Common Language Runtime) erstellt wird. Datenbankobjekte, die das reichhaltige Programmiermodell nutzen können, das von der Common Language Runtime bereitgestellt wird, sind z. B. Aggregatfunktionen, Funktionen, gespeicherte Prozeduren, Trigger und Typen.  
  
 Zum Erstellen einer CLR-Funktion in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] müssen folgende Schritte ausgeführt werden:  
  
-   Definieren der Funktion als statische Methode einer Klasse in einer Sprache, die von [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]unterstützt wird. Weitere Informationen zum Programmieren von Funktionen in der Common Language Runtime finden Sie unter [Benutzerdefinierte CLR-Funktionen](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md). Kompilieren Sie die Klasse mithilfe des entsprechenden Sprachcompilers, um eine Assembly in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] zu erstellen.  
  
-   Registrieren der Assembly in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe der CREATE ASSEMBLY-Anweisung. Weitere Informationen zum Arbeiten mit Assemblys in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] finden Sie unter [Assemblys &#40;Datenbankmodul&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md).  
  
-   Erstellen der Funktion, die auf die registrierte Assembly verweist, mithilfe der [CREATE FUNCTION](../../t-sql/statements/create-function-transact-sql.md) -Anweisung.  
  
> [!NOTE]  
>  Bei der Bereitstellung eines SQL Server-Projekts in [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] wird eine Assembly in der Datenbank registriert, die für das Projekt angegeben wurde. Bei der Bereitstellung des Projekts werden auch CLR-Funktionen in der Datenbank für alle Methoden erstellt, die mit dem **SqlFunction** -Attribut versehen sind. Weitere Informationen finden Sie unter [Deploying CLR Database Objects](../../relational-databases/clr-integration/deploying-clr-database-objects.md).  
  
> [!NOTE]  
>  Die Funktion zum Ausführen von CLR-Code ist in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] standardmäßig deaktiviert. Sie können Datenbankobjekte, die auf verwaltete Codemodule verweisen, erstellen, ändern oder löschen; diese Verweise werden jedoch nur dann in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt, wenn die Option [clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) mithilfe von [sp_configure (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)aktiviert wird.  
  
## <a name="accessing-external-resources"></a>Zugreifen auf externe Ressourcen  
 CLR-Funktionen können verwendet werden, um auf externe Ressourcen wie z. B. Dateien, Netzwerkressourcen, Webdienste oder andere Datenbanken (einschließlich Remoteinstanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) zuzugreifen. Hierzu können in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]verschiedene Klassen verwendet werden, wie `System.IO`, `System.WebServices`, `System.Sql`usw. Die Assembly, die solche Funktionen enthält, sollte für diesen Zweck mindestens mit der EXTERNAL_ACCESS-Berechtigung konfiguriert werden. Weitere Informationen finden Sie unter [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)unterstützt wird. Der verwaltete Anbieter von SQL Client kann für den Zugriff auf Remoteinstanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwendet werden. Loopbackverbindungen mit dem ursprünglichen Server werden in CLR-Funktionen jedoch nicht unterstützt.  
  
 **So erstellen, ändern oder löschen Sie Assemblys in SQL Server**  
  
-   [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
-   [DROP ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  
 **So erstellen Sie eine CLR-Funktion**  
  
-   [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)  
  
## <a name="accessing-native-code"></a>Zugreifen auf systemeigenen Code  
 CLR-Funktionen können für den Zugriff auf nativen (nicht verwalteten) Code verwendet werden, z.B. in C oder C++ geschriebenen Code. Dazu wird PInvoke vom verwalteten Code aus ausgeführt (Einzelheiten finden Sie unter [Aufrufen nativer Funktionen aus verwaltetem Code](http://go.microsoft.com/fwlink/?LinkID=181929) ). Dies kann die Wiederverwendung von Legacycode als CLR-UDFs oder das Programmieren leistungskritischer UDFs in systemeigenem Code ermöglichen. Die Verwendung einer UNSAFE-Assembly wird in diesem Fall vorausgesetzt. Warnhinweise zur Verwendung von UNSAFE-Assemblys finden Sie unter [CLR Integration Code Access Security](../../relational-databases/clr-integration/security/clr-integration-code-access-security.md) .  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen benutzerdefinierter Funktionen &#40;Datenbankmodul&#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)   
 [Erstellen benutzerdefinierter Aggregate](../../relational-databases/user-defined-functions/create-user-defined-aggregates.md)   
 [Ausführen von benutzerdefinierten Funktionen](../../relational-databases/user-defined-functions/execute-user-defined-functions.md)   
 [Anzeigen benutzerdefinierter Funktionen](../../relational-databases/user-defined-functions/view-user-defined-functions.md)   
 [Programmierkonzepte für die Integration der Common Language Runtime &#40;CLR&#41;](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  

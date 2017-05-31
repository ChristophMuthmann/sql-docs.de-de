---
title: "Ausführen von Windows PowerShell über SQL Server Management Studio | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1f841825-da1f-4062-9a81-3cdbab03845b
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ec4be68684d53bc8252c0c08e51a47eccb0cc05d
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="run-windows-powershell-from-sql-server-management-studio"></a>Ausführen von Windows PowerShell über SQL Server Management Studio
  Sie können Windows PowerShell-Sitzungen aus dem **Objekt-Explorer** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]starten. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] startet Windows PowerShell, lädt das Modul **sqlps** und legt den Pfadkontext auf den zugeordneten Knoten in der **** Objekt-Explorer-Struktur fest.  
  
## <a name="before-you-begin"></a>Vorbereitungen  
 Wenn Sie die Ausführung von PowerShell für ein Objekt im ****Objekt-Explorer angeben, startet [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] eine Windows PowerShell-Sitzung, in denen die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -PowerShell-Snap-Ins geladen und registriert wurden. Der Pfad für die Sitzung ist auf den Speicherort des Objekts, auf das Sie mit der rechten Maustaste geklickt haben, voreingestellt. Wenn Sie beispielsweise im Objekt-Explorer mit der rechten Maustaste auf das Datenbankobjekt [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] klicken und dann **PowerShell starten**auswählen, wird der Windows PowerShell-Pfad folgendermaßen festgelegt:  
  
```  
SQLSERVER:\SQL\MyComputer\MyInstance\Databases\AdventureWorks2012>  
```  
  
## <a name="run-powershell"></a>Ausführen von PowerShell  
 **So führen Sie PowerShell in SQL Server Management Studio aus**  
  
1.  Öffnen Sie den **Objekt-Explorer**.  
  
2.  Navigieren Sie zum Knoten für das zu verarbeitende Objekt.  
  
3.  Klicken Sie mit der rechten Maustaste auf das Objekt, und wählen Sie **PowerShell starten**aus.  
  
## <a name="permissions"></a>Berechtigungen  
 Wenn PowerShell in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]geöffnet wurde, wird das Programm nicht mit Administratorrechten ausgeführt, wodurch einige Aktivitäten möglicherweise verhindert werden, z. B. Aufrufe der WMI.  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server-PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  

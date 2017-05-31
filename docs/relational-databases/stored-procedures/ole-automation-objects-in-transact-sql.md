---
title: OLE-Automatisierungsobjekte in Transact-SQL | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-ole
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- triggers [SQL Server], OLE Automation
- batches [SQL Server], OLE Automation
- OLE Automation [SQL Server]
- OLE Automation [SQL Server], about OLE Automation
ms.assetid: a887d956-4cd0-400a-aa96-00d7abd7c44b
caps.latest.revision: 24
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8b598d764afe92eee8375eb6881ed8821acdde82
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="ole-automation-objects-in-transact-sql"></a>OLE-Automatisierungsobjekte in Transact-SQL
  [!INCLUDE[tsql](../../includes/tsql-md.md)] enthält mehrere gespeicherte Systemprozeduren, die Verweise auf OLE-Automatisierungsobjekte in [!INCLUDE[tsql](../../includes/tsql-md.md)] -Batches, gespeicherten Prozeduren und Triggern ermöglichen. Diese gespeicherten Systemprozeduren werden als erweiterte gespeicherte Prozeduren ausgeführt, und die OLE-Automatisierungsobjekte, die über die gespeicherten Prozeduren ausgeführt werden, werden wie eine erweiterte gespeicherte Prozedur im Adressraum einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ausgeführt.  
  
 Die gespeicherten OLE-Automatisierungsprozeduren ermöglichen es [!INCLUDE[tsql](../../includes/tsql-md.md)] -Batches, auf SQL-DMO-Objekte und benutzerdefinierte OLE-Automatisierungsobjekte zu verweisen, wie etwa Objekte, die die **IDispatch** -Schnittstelle verfügbar machen. Ein benutzerdefinierter In-Process-OLE-Server, der mithilfe von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] erstellt wurde, muss mit einem (mit der **On Error GoTo** -Anweisung angegebenen) Fehlerhundler für die Unterroutinen **Class_Initialize** und **Class_Terminate** ausgestattet sein. Nicht behandelte Fehler in den Unterroutinen **Class_Initialize** und **Class_Terminate** können unvorhersehbare Fehler verursachen, wie z.B. eine Zugriffsverletzungen in einer Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Fehlerhandler werden auch für andere Unterroutinen empfohlen.  
  
 Der erste Schritt beim Verwenden eines OLE-Automatisierungsobjekts in [!INCLUDE[tsql](../../includes/tsql-md.md)] ist das Aufrufen der gespeicherten Systemprozedur **sp_OACreate** , um eine Instanz des Objekts im Adressraum der Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]zu erstellen.  
  
 Verwenden Sie nach dem Erstellen einer Instanz des Objekts die folgenden gespeicherten Prozeduren, um mit den Eigenschaften, Methoden und Fehlerinformationen im Zusammenhang mit dem Objekt zu arbeiten:  
  
-   **sp_OAGetProperty** ruft den Wert einer Eigenschaft ab.  
  
-   **sp_OASetProperty** legt den Wert einer Eigenschaft fest.  
  
-   **sp_OAMethod** ruft eine Methode auf.  
  
-   **sp_OAGetErrorInfo** ruft die letzten Fehlerinformationen ab.  
  
 Wenn das Objekt nicht mehr benötigt wird, rufen Sie **sp_OADestroy** auf, um die Zuordnung der mit **sp_OACreate**erstellten Instanz des Objekts aufzuheben.  
  
 OLE-Automatisierungsobjekte geben Daten durch Eigenschaftswerte und Methoden zurück. **sp_OAGetProperty** und **sp_OAMethod** geben diese Datenwerte als Resultset zurück.  
  
 Der Gültigkeitsbereich eines OLE-Automatisierungsobjekts ist ein Batch. Alle Verweise auf das Objekt müssen in einem einzelnen Batch, einer gespeicherten Prozedur oder einem Trigger enthalten sein.  
  
 Beim Verweisen auf Objekte unterstützen die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -OLE-Automatisierungsobjekte das Traversieren des Objekts, auf das verwiesen wird, auf andere Objekte, die es enthält. Wenn beispielsweise das SQL-DMO-Objekt **SQLServer** verwendet wird, können Verweise auf Datenbanken und Tabellen erfolgen, die sich auf dem betreffenden Server befinden.  
  
## <a name="related-content"></a>Verwandte Inhalte  
 [Objekthierarchiesyntax &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/object-hierarchy-syntax-transact-sql.md)  
  
 [Oberflächenkonfiguration](../../relational-databases/security/surface-area-configuration.md)  
  
 [OLE-Automatisierungsprozeduren (Serverkonfigurationsoption)](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md)  
  
 [sp_OACreate &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-oacreate-transact-sql.md)  
  
 [sp_OAGetProperty &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-oagetproperty-transact-sql.md)  
  
 [sp_OASetProperty &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-oasetproperty-transact-sql.md)  
  
 [sp_OAMethod &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-oamethod-transact-sql.md)  
  
 [sp_OAGetErrorInfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-oageterrorinfo-transact-sql.md)  
  
 [sp_OADestroy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-oadestroy-transact-sql.md)  
  
  

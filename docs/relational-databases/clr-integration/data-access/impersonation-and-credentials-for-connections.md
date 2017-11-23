---
title: "Identitätswechsel und Anmeldeinformationen für Verbindungen | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- impersonation [CLR integration]
- security [CLR integration]
- database objects [CLR integration], connections
- connections [CLR integration]
- authentication [CLR integration]
- user impersonation [CLR integration]
- credentials [CLR integration]
- database objects [CLR integration], security
ms.assetid: 293dce7d-1db2-4657-992f-8c583d6e9ebb
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0815ae6b182f371eb171cf577e89a50adb9cdac4
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="impersonation-and-credentials-for-connections"></a>Identitätswechsel und Anmeldeinformationen für Verbindungen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]In der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] common Language Runtime (CLR)-Integration mit Windows-Authentifizierung zwar komplex, jedoch ist sicherer als die Verwendung von SQL Server-Authentifizierung. Beachten Sie bei Verwendung der Windows-Authentifizierung folgende Punkte:  
  
 Standardmäßig ist für einen SQL Server-Prozess, der eine ausgehende Verbindung mit Windows herstellt, der Sicherheitskontext des Windows-Dienstkontos für SQL Server erforderlich. Es ist jedoch möglich, einer Proxyidentität eine CLR-Funktion zuzuordnen, sodass ausgehende Verbindungen einen anderen Sicherheitskontext haben als die Verbindungen des Windows-Dienstkontos.  
  
 In einigen Fällen müssen Sie eventuell die Identität des Aufrufers mithilfe der **SqlContext.WindowsIdentity** -Eigenschaft statt Ausführen des Dienstkontos. Die **WindowsIdentity** -Instanz repräsentiert die Identität des Clients, der den Aufrufcode aufgerufen hat, und ist nur verfügbar, wenn der Client Windows-Authentifizierung verwendet. Sobald Sie erhalten haben die **WindowsIdentity** Instanz, die Sie aufrufen können **Impersonate** das Sicherheitstoken des Threads zu ändern, und öffnen Sie anschließend ADO.NET-Verbindungen im Auftrag des Clients.  
  
 Nach dem Aufruf von SQLContext.WindowsIdentity.Impersonate Sie nicht auf lokale Daten zugreifen und Sie können nicht auf Systemdaten zugreifen. Für den Zugriff auf Daten müssen Sie erneut, die WindowsImpersonationContext.Undo aufrufen.  
  
 Im folgende Beispiel wird gezeigt, wie mithilfe des Aufrufers annehmen der **SqlContext.WindowsIdentity** Eigenschaft.  
  
 Visual C#  
  
```  
WindowsIdentity clientId = null;  
WindowsImpersonationContext impersonatedUser = null;  
  
clientId = SqlContext.WindowsIdentity;  
  
// This outer try block is used to protect from   
// exception filter attacks which would prevent  
// the inner finally block from executing and   
// resetting the impersonation.  
try  
{  
   try  
   {  
      impersonatedUser = clientId.Impersonate();  
      if (impersonatedUser != null)  
         return GetFileDetails(directoryPath);  
         else return null;  
   }  
   finally  
   {  
      if (impersonatedUser != null)  
         impersonatedUser.Undo();  
   }  
}  
catch  
{  
   throw;  
}  
```  
  
> [!NOTE]  
>  Informationen zu verhaltensänderungen beim Identitätswechsel finden Sie unter [fehlerhafte Änderungen an Funktionen des Datenbankmoduls in SQL Server 2016](../../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md).  
  
 Wenn Sie die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows-Identitätsinstanz erhalten haben, können Sie diese Instanz standardmäßig nicht an einen anderen Computer weitergeben. Die Windows-Sicherheitsinfrastruktur schränkt diese Möglichkeit standardmäßig ein. Es gibt jedoch einen Mechanismus, der als "Delegierung" bezeichnet wird. Dieser ermöglicht die Weitergabe von Windows-Identitäten über mehrere vertrauenswürdige Computer hinweg. Weitere Informationen finden Sie Informationen zu Delegierung in der TechNet-Artikel "[Kerberos-Protokollübergang und eingeschränkte Delegierung](http://go.microsoft.com/fwlink/?LinkId=50419)".  
  
## <a name="see-also"></a>Siehe auch  
 [SqlContext-Objekt](../../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlcontext-object.md)  
  
  

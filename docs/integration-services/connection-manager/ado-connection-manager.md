---
title: ADO-Verbindungs-Manager | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connections [Integration Services], ADO
- connection managers [Integration Services], ADO
- ADO connection manager [Integration Services]
ms.assetid: 490418bc-5ef1-41b8-a9c8-de38aa96e0f6
caps.latest.revision: 54
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b42410ae3654bed35103ea9b0dcafedff32e3af7
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="ado-connection-manager"></a>ADO-Verbindungs-Manager
  Durch einen ADO-Verbindungs-Manager kann ein Paket eine Verbindung mit ADO-Objekten (ActiveX Data Objects) herstellen, wie z. B. einem Recordset. Dieser Verbindungs-Manager wird normalerweise für benutzerdefinierte Tasks verwendet, die in einer früheren Version einer Programmiersprache, wie z. B. Microsoft Visual Basic 6.0, erstellt wurden, oder für benutzerdefinierte Tasks, die Bestandteil einer vorhandenen Anwendung sind, die mithilfe von ADO eine Verbindung mit einer Datenquelle herstellt.  
  
 Wenn Sie einem Paket einen ADO-Verbindungs-Manager hinzufügen, erstellt [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] einen Verbindungs-Manager, der zur Laufzeit in eine ADO-Verbindung aufgelöst wird, die Eigenschaften des Verbindungs-Managers festlegt und der Sammlung **Verbindungen** im Paket den Verbindungs-Manager hinzufügt. Die **ConnectionManagerType** -Eigenschaft des Verbindungs-Managers ist auf **ADO**festgelegt.  
  
## <a name="troubleshooting-the-ado-connection-manager"></a>Problembehandlung des ADO-Verbindungs-Managers  
 Daten bestimmter [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datumsdatentypen generieren beim Lesen durch einen ADO-Verbindungs-Manager die in der folgenden Tabelle dargestellten Ergebnisse.  
  
|SQL Server-Datentyp|Ergebnis|  
|--------------------------|------------|  
|**time**, **datetimeoffset**|Das Paket erzeugt einen Fehler, sofern das Paket keine parametrisierten SQL-Befehle verwendet. Um parametrisierte SQL-Befehle zu verwenden, verwenden Sie den Task SQL ausführen im Paket. Weitere Informationen finden Sie unter [SQL ausführen (Task)](../../integration-services/control-flow/execute-sql-task.md) und [Parameter und Rückgabecodes im Task „SQL ausführen“](http://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663).|  
|**datetime2**|Der ADO-Verbindungs-Manager schneidet den Millisekundenwert ab.|  
  
> [!NOTE]  
>  Weitere Informationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datentypen sowie deren Zuordnung zu [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Datentypen finden Sie unter [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md) und [SQL Server Integration Services-Datentypen](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="configuring-the-ado-connection-manager"></a>Konfigurieren des ADO-Verbindungs-Managers  
 Es gibt folgende Möglichkeiten, um einen ADO-Verbindungs-Manager zu konfigurieren:  
  
-   Stellen Sie eine Verbindungszeichenfolge bereit, die die Anforderungen des ausgewählten Anbieters erfüllt.  
  
-   Schließen Sie in Abhängigkeit vom Anbieter den Namen der Datenquelle ein, mit der eine Verbindung hergestellt werden soll.  
  
-   Stellen Sie entsprechende Sicherheitsanmeldeinformationen für den ausgewählten Anbieter bereit.  
  
-   Geben Sie an, ob die im Verbindungs-Manager erstellte Verbindung zur Laufzeit beibehalten wird.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [OLE DB-Verbindungs-Manager konfigurieren](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)  
  
 Weitere Informationen zum programmgesteuerten Konfigurieren eines Verbindungs-Managers finden Sie unter <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> und [Programmgesteuertes Hinzufügen von Verbindungen](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)festgelegt.  
  
## <a name="see-also"></a>Siehe auch  
 [Integration Services-Verbindungen &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  


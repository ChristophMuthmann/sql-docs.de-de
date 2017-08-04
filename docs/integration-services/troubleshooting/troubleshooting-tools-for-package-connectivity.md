---
title: "Tools zur Problembehandlung für Package Connectivity | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Integration Services packages, troubleshooting
- SSIS packages, troubleshooting
- Integration Services, troubleshooting
- connectivity [Integration Services], troubleshooting
- errors [Integration Services], troubleshooting
- packages [Integration Services], troubleshooting
ms.assetid: 08a019f5-8ba7-4527-97c1-e9846d4022ff
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e3799e224930806445bc1c27f37c05b95a0bbbae
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="troubleshooting-tools-for-package-connectivity"></a>Tools zur Behandlung von Problemen mit Paketverbindungen
[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] enthält Funktionen und Tools, mit denen Sie Verbindungsprobleme zwischen Paketen und den Datenquellen behandeln können, aus denen Daten von Paketen extrahiert und geladen werden.  
  
## <a name="troubleshooting-issues-with-external-data-providers"></a>Behandlung von Problemen mit externen Datenanbietern  
 Viele Paketfehler treten während Interaktionen mit externen Datenanbietern auf. Die von diesen Anbietern an [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] zurückgegebenen Meldungen bieten jedoch häufig nicht genug Informationen, um mit der Problembehandlung der Interaktion zu beginnen. Damit die Problembehandlung vorgenommen werden kann, enthält [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] neue Meldungen für die Protokollierung, die Sie zur Problembehandlung der Interaktion eines Pakets mit externen Datenquellen verwenden können.  
  
-   **Aktivieren Sie die Protokollierung, und wählen Sie das Diagnostic-Ereignis des Pakets aus, um die Meldungen zur Problembehandlung anzuzeigen**. Mit den folgenden Komponenten von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] kann vor und nach jedem Aufruf an einen externen Datenanbieter eine Meldung in das Protokoll geschrieben werden:  
  
    -   OLE DB-Verwaltungs-Manager, OLE DB-Quelle und OLE DB-Ziel  
  
    -   [!INCLUDE[vstecado](../../includes/vstecado-md.md)]Verbindungs-Manager und ADO NET-Quelle  
  
    -   Task SQL ausführen  
  
    -   Transformation für Suche, Transformation für OLE DB-Befehl und Transformation für langsam veränderliche Dimensionen  
  
     Die Protokollmeldungen enthalten den Namen der aufgerufenen Methode. Diese Protokollmeldungen können beispielsweise die **Open**-Methode eines **Connection**-Objekts von OLE DB oder die **ExecuteNonQuery**-Methode eines **Command**-Objekts enthalten. Die Nachrichten haben das folgende Format, wobei „%1! s!“ ein Platzhalter für die Methodeninformationen ist:  
  
    ```  
    ExternalRequest_pre: The object is ready to make the following external request: '%1!s!'.  
    ExternalRequest_post: '%1!s!'. The external request has completed.  
    ```  
  
     Überprüfen Sie zur Problembehandlung der Interaktion mit dem externen Datenanbieter, ob für jede „Vorher“-Meldung (`ExternalRequest_pre`) eine entsprechende „Nachher“-Meldung (`ExternalRequest_post`) vorhanden ist. Wenn keine entsprechende "Nachher"-Meldung vorhanden ist, hat der externe Datenanbieter nicht wie erwartet reagiert.  
  
     Im folgenden Beispiel sind einige Beispielzeilen aus einem Protokoll dargestellt, in dem diese Meldungen für die Protokollierung enthalten sind:  
  
    ```  
    ExternalRequest_pre: The object is ready to make the following external request: 'ITransactionJoin::JoinTransaction'.  
    ExternalRequest_post: 'ITransactionJoin::JoinTransaction succeeded'. The external request has completed.  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDbConnection.Open'.  
    ExternalRequest_post: 'IDbConnection.Open succeeded'. The external request has completed.  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDbConnection.CreateCommand'.  
    ExternalRequest_post: 'IDbConnection.CreateCommand finished'. The external request has completed."  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDbCommand.ExecuteReader'.  
    ExternalRequest_post: 'IDbCommand.ExecuteReader finished'. The external request has completed."  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDataReader.GetSchemaTable'.  
    ExternalRequest_post: 'IDataReader.GetSchemaTable finished'. The external request has completed."  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDataReader.Close'.  
    ExternalRequest_post: 'IDataReader.Close finished'. The external request has completed."  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDbConnection.Close'.  
    ExternalRequest_post: 'IDbConnection.Close finished'. The external request has completed."  
    ```  
  
## <a name="see-also"></a>Siehe auch  
 [Tools zur Problembehandlung für die Paketentwicklung](../../integration-services/troubleshooting/troubleshooting-tools-for-package-development.md)   
 [Tools zur Problembehandlung für die Ausführung des Pakets](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)  
  
  

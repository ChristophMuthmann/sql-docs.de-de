---
title: ADO.NET-Ziel-Editor (Seite Verbindungs-Manager) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.adonetdest.connection.f1
ms.assetid: a3b11286-32c8-40e1-8ae7-090e2590345a
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 16ed4103735f389959531b92fad81884fc583a5b
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="ado-net-destination-editor-connection-manager-page"></a>ADO.NET-Ziel-Editor (Seite 'Verbindungs-Manager')
  Mithilfe der Seite **Verbindungs-Manager** des Dialogfelds **ADO.NET-Ziel-Editor** können Sie die [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Verbindung für das Ziel auswählen. Außerdem können Sie auf dieser Seite eine Tabelle oder Sicht aus der Datenbank auswählen.  
  
 Weitere Informationen zum ADO NET-Ziel finden Sie unter [ADO NET Destination](../../integration-services/data-flow/ado-net-destination.md).  
  
 **So öffnen Sie die Seite "Verbindungs-Manager"**  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket, das ADO.NET als Ziel hat.  
  
2.  Doppelklicken Sie auf der Registerkarte **Datenfluss** auf das ADO NET-Ziel.  
  
3.  Klicken Sie im **ADO.NET-Ziel-Editor**auf **Verbindungs-Manager**.  
  
## <a name="static-options"></a>Statische Optionen  
 **Connection manager**  
 Wählen Sie einen vorhandenen Verbindungs-Manager aus der Liste aus, oder erstellen Sie eine neue Verbindung, indem Sie auf **Neu**klicken.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **ADO.NET-Verbindungs-Manager konfigurieren** einen neuen Verbindungs-Manager.  
  
 **Tabelle oder Sicht verwenden**  
 Wählen Sie eine vorhandene Tabelle oder Sicht aus der Liste aus, oder erstellen Sie eine neue Tabelle, indem Sie auf **Neu**klicken.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **Tabelle erstellen** eine neue Tabelle oder Sicht.  
  
> [!NOTE]  
>  Wenn Sie auf **Neu**klicken, generiert [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] eine Standard-CREATE TABLE-Anweisung auf Grundlage der verbundenen Datenquelle. Diese Standard-CREATE TABLE-Anweisung enthält nicht das FILESTREAM-Attribut, selbst wenn die Quelltabelle eine Spalte mit der Erklärung des FILESTREAM-Attributs enthält. Um eine [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Komponente mit dem FILESTREAM-Attribut auszuführen, implementieren Sie zunächst die FILESTREAM-Speicherung in der Zieldatenbank. Fügen Sie dann das FILESTREAM-Attribut der CREATE TABLE-Anweisung im Dialogfeld **Tabelle erstellen** hinzu. Weitere Informationen finden Sie unter [Blob-Daten &#40;Binary Large Object, SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 **Vorschau**  
 Zeigen Sie mithilfe des Dialogfelds **Vorschau der Abfrageergebnisse anzeigen** eine Vorschau der Ergebnisse an. In der Vorschau können bis zu 200 Zeilen angezeigt werden.  
  
 **Masseneinfügung verwenden, falls verfügbar**  
 Geben Sie an, ob die Schnittstelle <xref:System.Data.SqlClient.SqlBulkCopy> verwendet werden soll, um die Leistung von Masseneinfügungsvorgängen zu verbessern.  
  
 Nur ADO.NET-Anbieter, die ein <xref:System.Data.SqlClient.SqlConnection> -Objekt zurückgeben, unterstützen die Verwendung der <xref:System.Data.SqlClient.SqlBulkCopy> -Schnittstelle. Der .NET-Datenanbieter für SQL Server (SqlClient) gibt ein <xref:System.Data.SqlClient.SqlConnection> -Objekt zurück, und ein benutzerdefinierter Anbieter gibt möglicherweise ein <xref:System.Data.SqlClient.SqlConnection> -Objekt zurück.  
  
 Sie können den .NET-Datenanbieter für SQL Server (SqlClient) verwenden, um eine Verbindung mit [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]herzustellen.  
  
 Wenn Sie **Masseneinfügung verwenden, falls verfügbar**auswählen und für **Zeile umleiten** die Option **Fehler**festlegen, enthält der Datenbatch, der vom Ziel an die Fehlerausgabe umgeleitet wird, möglicherweise intakte Zeilen. Weitere Informationen zur Behandlung von Fehlern in Massenvorgängen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md). Weitere Informationen zur Option **Zeile umleiten** finden Sie unter [Ziel-Editor für ADO.NET &#40;Seite „Fehlerausgabe“&#41;](../../integration-services/data-flow/ado-net-destination-editor-error-output-page.md).  
  
> [!NOTE]  
>  Wenn eine SQL Server oder Sybase-Quelltabelle eine Identitätsspalte enthält, müssen Sie "SQL ausführen"-Tasks verwenden, um IDENTITY_INSERT vor der ADO NET-Ziel zu aktivieren und deaktivieren Sie es danach erneut. (Die identitätsspalteneigenschaft gibt einen inkrementellen Wert für die Spalte an. Die SET IDENTITY_INSERT-Anweisung kann die expliziten Werte aus der Quelltabelle in die Identitätsspalte in der Zieltabelle eingefügt werden.)  
>   
>   Um die SET IDENTITY_INSERT-Anweisungen und erfolgreich Laden der Daten auszuführen, müssen Sie folgende Schritte auszuführen.
>       1. Verwenden Sie den gleichen ADO.NET-Verbindungs-Manager aus, für die SQL ausführen-Tasks und die ADO.NET-Ziel.
>       2. Legen Sie auf den Verbindungs-Manager die **RetainSameConnection** Eigenschaft und die **MultipleActiveResultSets** Eigenschaft auf "true".
>       3. Legen Sie die ADO.NET-Ziel die **UseBulkInsertWhenPossible** Eigenschaft auf "false".
>
>  Weitere Informationen finden Sie unter [SET IDENTITY_INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/set-identity-insert-transact-sql.md) und [IDENTITY &#40;Eigenschaft&#41; &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md).  
  
## <a name="external-resources"></a>Externe Ressourcen  
 Technischer Artikel [Schnelles Laden von Daten in eine Windows Azure SQL-Datenbank](http://go.microsoft.com/fwlink/?LinkId=244333)auf sqlcat.com  
  
## <a name="see-also"></a>Siehe auch  
 [ADO.NET-Ziel-Editor &#40;Seite „Zuordnungen“&#41;](../../integration-services/data-flow/ado-net-destination-editor-mappings-page.md)   
 [ADO NET-Ziel-Editor &#40; Seite "Fehlerausgabe" Fehler &#41;](../../integration-services/data-flow/ado-net-destination-editor-error-output-page.md)   
 [ADO.NET-Verbindungs-Manager](../../integration-services/connection-manager/ado-net-connection-manager.md)   
 [Tasks "SQL ausführen"](../../integration-services/control-flow/execute-sql-task.md)  
  
  

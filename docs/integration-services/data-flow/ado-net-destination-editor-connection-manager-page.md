---
title: "ADO.NET-Ziel-Editor (Seite &#39;Verbindungs-Manager&#39;) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.adonetdest.connection.f1"
ms.assetid: a3b11286-32c8-40e1-8ae7-090e2590345a
caps.latest.revision: 31
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 31
---
# ADO.NET-Ziel-Editor (Seite &#39;Verbindungs-Manager&#39;)
  Mithilfe der Seite **Verbindungs-Manager** des Dialogfelds **ADO.NET-Ziel-Editor** können Sie die [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Verbindung für das Ziel auswählen. Außerdem können Sie auf dieser Seite eine Tabelle oder Sicht aus der Datenbank auswählen.  
  
 Weitere Informationen zum ADO NET-Ziel finden Sie unter [ADO NET Destination](../../integration-services/data-flow/ado-net-destination.md).  
  
 **So öffnen Sie die Seite "Verbindungs-Manager"**  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket, das ADO.NET als Ziel hat.  
  
2.  Doppelklicken Sie auf der Registerkarte **Datenfluss** auf das ADO NET-Ziel.  
  
3.  Klicken Sie im **ADO.NET-Ziel-Editor**auf **Verbindungs-Manager**.  
  
## Statische Optionen  
 **Verbindungs-Manager**  
 Wählen Sie einen vorhandenen Verbindungs-Manager aus der Liste aus, oder erstellen Sie eine neue Verbindung, indem Sie auf **Neu** klicken.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **ADO.NET-Verbindungs-Manager konfigurieren** einen neuen Verbindungs-Manager.  
  
 **Tabelle oder Sicht verwenden**  
 Wählen Sie eine vorhandene Tabelle oder Sicht aus der Liste aus, oder erstellen Sie eine neue Tabelle, indem Sie auf **Neu** klicken.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **Tabelle erstellen** eine neue Tabelle oder Sicht.  
  
> [!NOTE]  
>  Wenn Sie auf **Neu**klicken, generiert [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] eine Standard-CREATE TABLE-Anweisung auf Grundlage der verbundenen Datenquelle. Diese Standard-CREATE TABLE-Anweisung enthält nicht das FILESTREAM-Attribut, selbst wenn die Quelltabelle eine Spalte mit der Erklärung des FILESTREAM-Attributs enthält. Um eine [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Komponente mit dem FILESTREAM-Attribut auszuführen, implementieren Sie zunächst die FILESTREAM-Speicherung in der Zieldatenbank. Fügen Sie dann das FILESTREAM-Attribut der CREATE TABLE-Anweisung im Dialogfeld **Tabelle erstellen** hinzu. Weitere Informationen finden Sie unter [Binary Large Object-Daten &#40;Blob&#41; &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 **Vorschau**  
 Zeigen Sie mithilfe des Dialogfelds **Vorschau der Abfrageergebnisse anzeigen** eine Vorschau der Ergebnisse an. In der Vorschau können bis zu 200 Zeilen angezeigt werden.  
  
 **Masseneinfügung verwenden, falls verfügbar**  
 Geben Sie an, ob die Schnittstelle <xref:System.Data.SqlClient.SqlBulkCopy> verwendet werden soll, um die Leistung von Masseneinfügungsvorgängen zu verbessern.  
  
 Nur ADO.NET-Anbieter, die ein <xref:System.Data.SqlClient.SqlConnection>-Objekt zurückgeben, unterstützen die Verwendung der <xref:System.Data.SqlClient.SqlBulkCopy>-Schnittstelle. Der .NET-Datenanbieter für SQL Server (SqlClient) gibt ein <xref:System.Data.SqlClient.SqlConnection>-Objekt zurück, und ein benutzerdefinierter Anbieter gibt möglicherweise ein <xref:System.Data.SqlClient.SqlConnection>-Objekt zurück.  
  
 Sie können den .NET-Datenanbieter für SQL Server (SqlClient) verwenden, um eine Verbindung mit [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] herzustellen.  
  
 Wenn Sie **Masseneinfügung verwenden, falls verfügbar** auswählen und für **Zeile umleiten** die Option **Fehler** festlegen, enthält der Datenbatch, der vom Ziel an die Fehlerausgabe umgeleitet wird, möglicherweise intakte Zeilen. Weitere Informationen zur Behandlung von Fehlern in Massenvorgängen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md). Weitere Informationen zur Option **Fehler** finden Sie unter [Ziel-Editor für ADO.NET &#40;Seite „Fehlerausgabe“&#41;](../../integration-services/data-flow/ado-net-destination-editor-error-output-page.md).  
  
> [!NOTE]  
>  Wenn eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]- oder Sybase-Quelltabelle eine Identitätsspalte enthält, müssen Sie SQL ausführen-Tasks zum Ausführen einer SET IDENTITY_INSERT-Anweisung vor und nach dem ADO NET-Ziel verwenden. Die Identitätsspalteneigenschaft gibt einen inkrementellen Wert für die Spalte an. Die SET IDENTITY_INSERT-Anweisung ermöglicht, dass explizite Werte in die Identitätsspalte eingefügt werden können. Legen Sie die **RetainSameConnection**-Eigenschaft des [!INCLUDE[vstecado](../../includes/vstecado-md.md)]-Verbindungs-Managers auf **TRUE** fest, um die CREATE TABLE- und SET IDENTITY-Anweisungen für dieselbe Datenbankverbindung auszuführen. Verwenden Sie den gleichen [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Verbindungs-Manager auch für die "SQL ausführen"-Tasks und das ADO.NET-Ziel.  
>   
>  Weitere Informationen finden Sie unter [SET IDENTITY_INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/set-identity-insert-transact-sql.md) und [IDENTITY &#40;Eigenschaft&#41; &#40;Transact-SQL&#41;](../Topic/IDENTITY%20\(Property\)%20\(Transact-SQL\).md).  
  
## Externe Ressourcen  
 Technischer Artikel [Schnelles Laden von Daten in eine Windows Azure SQL-Datenbank](http://go.microsoft.com/fwlink/?LinkId=244333)auf sqlcat.com  
  
## Siehe auch  
 [ADO.NET-Ziel-Editor &#40;Seite „Zuordnungen“&#41;](../../integration-services/data-flow/ado-net-destination-editor-mappings-page.md)   
 [Ziel-Editor für ADO.NET &#40;Seite „Fehlerausgabe“&#41;](../../integration-services/data-flow/ado-net-destination-editor-error-output-page.md)   
 [ADO.NET-Verbindungs-Manager](../../integration-services/connection-manager/ado-net-connection-manager.md)   
 [SQL ausführen (Task)](../../integration-services/control-flow/execute-sql-task.md)  
  
  
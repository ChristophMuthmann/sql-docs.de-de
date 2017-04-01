---
title: "ADO NET-Quelle | Microsoft Docs"
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
  - "sql13.dts.designer.adonetsource.f1"
helpviewer_keywords: 
  - "ADO NET-Quelle"
  - "Quellen [Integration Services], ADO.NET"
  - "Quellen [Integration Services], DataReader"
  - ".NET Framework [Integration Services]"
  - "DataReader-Quelle"
ms.assetid: 2a2f1750-2cda-4dda-9dca-623a96a6b3c0
caps.latest.revision: 101
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 101
---
# ADO NET-Quelle
  Die ADO NET-Quelle verwendet Daten von einem .NET-Anbieter und stellt sie dem Datenfluss zur Verfügung.  
  
 Sie können mithilfe der ADO.NET-Quelle eine Verbindung mit [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] herstellen. Das Herstellen einer Verbindung mit [!INCLUDE[ssSDS](../../includes/sssds-md.md)] über OLE DB wird nicht unterstützt. Weitere Informationen zu [!INCLUDE[ssSDS](../../includes/sssds-md.md)] finden Sie unter [Azure SQL-Datenbanken – Allgemeine Einschränkungen und Leitlinien](http://go.microsoft.com/fwlink/?LinkId=248228).  
  
## Datentypunterstützung  
 Die Quelle konvertiert alle Datentypen, die nicht einem bestimmten [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Datentyp zugeordnet sind, in den DT_NTEXT-Datentyp von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Diese Konvertierung findet auch dann statt, wenn der Datentyp **System.Object**ist.  
  
 Sie können den Datentyp DT_NTEXT in den Datentyp DT_WSTR oder DT_WSTR in DT_NTEXT ändern. Datentypen werden durch Festlegen der Eigenschaft **DataType** im Dialogfeld **Erweiterter Editor** der ADO NET-Quelle geändert. Weitere Informationen finden Sie unter [Common Properties](../Topic/Common%20Properties.md).  
  
 Der DT_NTEXT-Datentyp kann mithilfe einer Transformation für Datenkonvertierung nach der ADO NET-Quelle auch in die Datentypen DT_BYTES oder DT_STR konvertiert werden. Weitere Informationen finden Sie unter [Data Conversion Transformation](../../integration-services/data-flow/transformations/data-conversion-transformation.md).  
  
 In [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] werden die Datenquellentypen DT_DBDATE, DT_DBTIME, DT_DBTIMESTAMP2 und DT_DBTIMESTAMPOFFSET bestimmten Datumsdatentypen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zugeordnet. Sie können die ADO NET-Quelle so konfigurieren, dass die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendeten Datumsdatentypen in die von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] verwendeten Datumsdatentypen konvertiert werden. Die ADO NET-Quelle wird zum Konvertieren dieser Datumsdatentypen konfiguriert, indem die Eigenschaft **Typsystemversion** des [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Verbindungs-Managers auf **Neueste**festgelegt wird. (Die Eigenschaft **Typsystemversion** befindet sich auf der Seite **Alle** des Dialogfelds **Verbindungs-Manager**. Doppelklicken Sie mit der rechten Maustaste auf den [!INCLUDE[vstecado](../../includes/vstecado-md.md)]-Verbindungs-Manager, und klicken Sie anschließend auf **Bearbeiten**, um das Dialogfeld **Verbindungs-Manager** zu öffnen.)  
  
> [!NOTE]  
>  Wenn die Eigenschaft **Typsystemversion** des [!INCLUDE[vstecado](../../includes/vstecado-md.md)]-Verbindungs-Managers auf **SQL Server 2005** festgelegt ist, konvertiert das System die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datumsdatentypen in DT_WSTR.  
  
 Die benutzerdefinierten Datentypen (UDTs) werden vom System in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Blobs (Binary Large Objects) konvertiert, wenn der [!INCLUDE[vstecado](../../includes/vstecado-md.md)]-Verbindungs-Manager den Anbieter als .NET-Datenanbieter für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) festlegt. Das System wendet die folgenden Regeln an, wenn es den UDT-Datentyp konvertiert:  
  
-   Wenn die UDT-Daten nicht umfangreich sind, konvertiert das System die Daten in DT_BYTES.  
  
-   Sind die UDT-Daten nicht umfangreich und ist die Eigenschaft **Länge** der Datenbankspalte auf -1 oder einen Wert über 8.000 Byte festgelegt, werden die Daten vom System in DT_IMAGE konvertiert.  
  
-   Wenn die UDT-Daten umfangreich sind, konvertiert das System die Daten in DT_IMAGE.  
  
    > [!NOTE]  
    >  Ist die ADO NET-Quelle nicht zum Verwenden einer Fehlerausgabe konfiguriert, gibt das System die Daten an die DT_IMAGE-Spalte in Abschnitten von jeweils 8.000 Bytes weiter. Ist die ADO NET-Quelle zum Verwenden einer Fehlerausgabe konfiguriert, gibt das System das gesamte Array an Bytes an die DT_IMAGE-Spalte weiter. Weitere Informationen zum Konfigurieren von Komponenten zur Verwendung der Fehlerausgabe finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).  
  
 Weitere Informationen zu den Datentypen von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], den unterstützten Datentypkonvertierungen sowie der Datentypzuordnung über bestimmte Datenbanken, darunter auch [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], finden Sie unter [SQL Server Integration Services-Datentypen](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Weitere Informationen zur Zuordnung von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Datentypen zu verwalteten Datentypen finden Sie unter [Verwenden von Datentypen im Datenfluss](../../integration-services/extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md).  
  
## Problembehandlung der ADO NET-Quelle  
 Sie können die von der ADO NET-Quelle an externe Datenanbieter gerichteten Aufrufe protokollieren. Mithilfe dieser Protokollierungsfunktion können Sie Probleme beim Laden von Daten aus externen Datenquellen durch die ADO NET-Quelle behandeln. Aktivieren Sie zum Protokollieren der von der ADO NET-Quelle an externe Datenanbieter gerichteten Aufrufe die Paketprotokollierung, und wählen Sie das **Diagnostic** -Ereignis auf Paketebene aus. Weitere Informationen finden Sie unter [Behandlung von Problemen mit Paketausführungstools](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## ADO NET-Quellkonfiguration  
 Zum Konfigurieren der ADO NET-Quelle geben Sie die SQL-Anweisung an, die das Resultset definiert. Beispielsweise extrahiert eine ADO NET-Quelle, die eine Verbindung mit der [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] -Datenbank herstellt und die SQL-Anweisung `SELECT * FROM Production.Product` verwendet, alle Zeilen aus der **Production.Product** -Tabelle und stellt das Dataset einer Downstreamkomponente bereit.  
  
> [!NOTE]  
>  Wenn Sie mithilfe einer SQL-Anweisung eine gespeicherte Prozedur aufrufen, die Ergebnisse von einer temporären Tabelle zurückgibt, verwenden Sie die Option WITH RESULT SETS, um Metadaten für das Resultset zu definieren.  
  
> [!NOTE]  
>  Wenn Sie zum Ausführen einer gespeicherten Prozedur eine SQL-Anweisung verwenden und der folgende Paketfehler auftritt, können Sie den Fehler u.U. beheben, indem Sie die **SET FMTONLY OFF**-Anweisung vor der EXEC-Anweisung hinzufügen.  
>   
>  **Die Spalte <Spaltenname> wurde in der Datenquelle nicht gefunden.**  
  
 Die ADO NET-Quelle verwendet den [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Verbindungs-Manager zum Herstellen einer Verbindung mit einer Datenquelle, und der Verbindungs-Manager gibt den .NET-Anbieter an. Weitere Informationen finden Sie unter [ADO.NET Connection Manager](../../integration-services/connection-manager/ado-net-connection-manager.md).  
  
 Die ADO NET-Quelle weist eine reguläre Ausgabe und eine Fehlerausgabe auf.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](../Topic/Common%20Properties.md)  
  
-   [Benutzerdefinierte Eigenschaften von ADO.NET](../../integration-services/data-flow/ado-net-custom-properties.md)  
  
 Weitere Informationen zum Festlegen der Eigenschaften finden Sie unter [Festlegen der Eigenschaften einer Datenflusskomponente](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## Siehe auch  
 [DataReader-Ziel](../../integration-services/data-flow/datareader-destination.md)   
 [ADO NET-Ziel](../../integration-services/data-flow/ado-net-destination.md)   
 [Datenfluss](../../integration-services/data-flow/data-flow.md)  
  
  
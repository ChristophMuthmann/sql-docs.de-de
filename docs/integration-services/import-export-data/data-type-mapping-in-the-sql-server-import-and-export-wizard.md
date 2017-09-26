---
title: Datentypzuordnung in der SQL Server-Import / Export-Assistent | Microsoft Docs
ms.custom: 
ms.date: 01/11/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 669be403-cb17-4b12-bbbf-e7a74003c4b6
caps.latest.revision: 2
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4eca10e506087ee5d8106cb05c861c4efa49a65d
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="data-type-mapping-in-the-sql-server-import-and-export-wizard"></a>Zuordnung von Datentypen mit dem SQL Server-Import/Export-Assistenten
 Im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Import/Export-Assistenten können Sie den Namen, den Datentyp und die Datentypeigenschaften von Spalten in neuen Zieltabellen und -dateien festlegen. Allerdings können Sie keine benutzerdefinierten Konvertierungen für Spaltenwerte angeben. Daher ist die integrierte Zuordnung von Datentypen von der Quelle zum Ziel wichtig.  
  
##  <a name="wizardMapping"></a> Wie ordnet der Assistent Datentypen zwischen Quelle und Ziel zu?
Der Assistent verwendet die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] installierten Zuordnungsdateien, um Datentypen aus einem Datenbanksystem oder einer Datenbankversion einem anderen System bzw. einer anderen Version zuzuordnen. Beispielsweise ist eine Zuordnung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datentypen zu Oracle-Datentypen möglich. Standardmäßig werden die Zuordnungsdateien im XML-Format in den folgenden Ordnern installiert.
-   **C:\Program Files\Microsoft SQL Server\130\DTSMappingFiles\* * (für 64-Bit)
-   **C:\Programme\Microsoft Dateien (x86) \Microsoft SQL Server\130\DTSMappingFiles\* * (für 32-Bit).  
  
 Wenn Sie eine vorhandene Zuordnungsdatei bearbeiten oder dem Ordner eine neue Zuordnungsdatei hinzufügen, müssen Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Import/Export-Assistenten bzw. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] schließen und anschließend erneut öffnen, um die neue oder geänderte Zuordnungsdatei zu laden.  
 
## <a name="you-can-change-an-existing-mapping-file"></a>Sie können eine vorhandene Zuordnungsdatei ändern
Wenn Ihr Unternehmen verschiedene Zuordnungen zwischen Datentypen erfordert, können Sie die Zuordnungsdateien aktualisieren, um die vom Assistenten durchgeführten Zuordnungen zu ändern. Wenn Sie z. B. möchten, dass der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **nchar** -Datentyp beim Übertragen von Daten von **in DB2 dem DB2-Datentyp** GRAPHIC **VARin DB2 dem DB2-Datentyp** VARGRAPHIC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zugeordnet wird, ändern Sie die **nchar** -Zuordnung in der Zuordnungsdatei **SqlClientToIBMDB2.xml** so, dass **in DB2 dem DB2-Datentyp** statt **VARin DB2 dem DB2-Datentyp.**verwendet wird.  
  
## <a name="you-can-add-a-new-mapping-file"></a>Sie können eine neue Zuordnungsdatei hinzufügen
[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] installiert Zuordnungen zwischen vielen häufig verwendeten Kombinationen von Quelle und Ziel. Sie können auch dem Verzeichnis **MappingFiles** neue Zuordnungsdateien hinzufügen, um weitere Quellen und Ziele zu unterstützen. Die neuen Zuordnungsdateien müssen dem veröffentlichten XSD-Schema entsprechen und einer eindeutigen Kombination aus Quelle und Ziel zugeordnet sein. Das Schema für Zuordnungsdateien, **DataTypeMapping.xsd**, ist [hier](http://schemas.microsoft.com/sqlserver/2008/07/IntegrationServices/DataTypeMapping/DataTypeMapping.xsd)veröffentlicht.
 
## <a name="sample-mapping-file"></a>Beispielzuordnungsdatei
Es folgt ein Teil der XML-Zuordnungsdatei, die SQL Server-Datentypen (oder genauer gesagt vom .NET Framework-Datenanbieter für SQL Server verwendete Datentypen) Oracle-Datentypen zuordnet. Beispielsweise können Sie sehen, dass der SQL Server -Datentyp **int** dem Oracle-Datentyp **INTEGER** zugeordnet wird.
  
```xml  
  
<dtm:DataTypeMappings  
    xmlns:dtm="http://www.microsoft.com/SqlServer/Dts/DataTypeMapping.xsd"   
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
    SourceType="System.Data.SqlClient.SqlConnection"   
    MinSourceVersion="*"   
    MaxSourceVersion="*"   
    DestinationType="MSDAORA;OraOLEDB.Oracle;System.Data.OracleClient.OracleConnection"   
    MinDestinationVersion="08.*"   
    MaxDestinationVersion="*">  
  
    <!-- smallint -->  
    <dtm:DataTypeMapping >  
        <dtm:SourceDataType>  
            <dtm:DataTypeName>smallint</dtm:DataTypeName>  
        </dtm:SourceDataType>  
        <dtm:DestinationDataType>  
            <dtm:SimpleType>  
                <dtm:DataTypeName>INTEGER</dtm:DataTypeName>  
            </dtm:SimpleType>  
        </dtm:DestinationDataType>  
    </dtm:DataTypeMapping>    
  
    <!-- int -->  
    <dtm:DataTypeMapping >  
        <dtm:SourceDataType>  
            <dtm:DataTypeName>int</dtm:DataTypeName>  
        </dtm:SourceDataType>  
        <dtm:DestinationDataType>  
            <dtm:SimpleType>  
                <dtm:DataTypeName>INTEGER</dtm:DataTypeName>  
            </dtm:SimpleType>  
        </dtm:DestinationDataType>  
    </dtm:DataTypeMapping>    
  
        ...  
  
</dtm:DataTypeMappings>  
  
```  



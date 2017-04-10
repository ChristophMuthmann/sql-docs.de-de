---
title: "Rohdatendatei-Quelle | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.rawfilesource.f1"
helpviewer_keywords: 
  - "Quellen [Integration Services], Rohdatendatei"
  - "Rohdaten [Integration Services]"
  - "Rohdatendatei-Quelle"
ms.assetid: 5b4daea5-7f76-4674-aa77-0a79f9f97f7d
caps.latest.revision: 43
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 43
---
# Rohdatendatei-Quelle
  Die Rohdatendatei-Quelle liest Rohdaten aus einer Datei. Die Darstellung der Daten erfolgt im systemeigenen Quellformat, sodass die Daten nicht übersetzt und fast nicht analysiert werden müssen. Dies bedeutet, dass die Rohdatendatei-Quelle Daten schneller als andere Quellen, wie z. B. Flatfile- und OLE DB-Quellen, lesen kann.  
  
 Mithilfe der Rohdatendatei-Quelle werden Rohdaten abgerufen, die zuvor vom Rohdatendatei-Ziel geschrieben wurden. Sie können die Rohdatendatei-Quelle auch auf eine leere Rohdatendatei verweisen, die nur die Spalten (Nur-Metadatendatei) enthält. Sie verwenden das Rohdatendatei-Ziel, um die Nur-Metadatendatei zu generieren, ohne das Paket ausführen zu müssen. Weitere Informationen finden Sie unter [Raw File Destination](../../integration-services/data-flow/raw-file-destination.md).  
  
 Das Format der Rohdatendatei enthält Sortierungsinformationen: Das Rohdatendatei-Ziel speichert alle Sortierungsinformationen, einschließlich der Vergleichsflags für Zeichenfolgenspalten. Die Rohdatendatei-Quelle liest und beachtet die Sortierungsinformationen. Sie können die Rohdatendatei-Quelle dergestalt konfigurieren, dass die Sortierflags in der Datei mit dem erweiterten Editor ignoriert werden. Weitere Informationen zu Vergleichsflags finden Sie unter [Comparing String Data](../../integration-services/data-flow/comparing-string-data.md).  
  
 Zum Konfigurieren der Rohdatendatei geben Sie den Namen der Datei an, die die Rohdatendatei-Quelle liest.  
  
> [!NOTE]  
>  Für diese Quelle wird kein Verbindungs-Manager verwendet.  
  
 Diese Quelle erzeugt nur eine Ausgabe. Eine Fehlerausgabe wird nicht unterstützt.  
  
## Konfiguration der Rohdatendatei-Quelle  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](../Topic/Common%20Properties.md)  
  
-   [Benutzerdefinierte Eigenschaften der Rohdatendatei](../../integration-services/data-flow/raw-file-custom-properties.md)  
  
## Verwandte Aufgaben  
 Informationen zum Festlegen der Eigenschaften der Komponente finden Sie unter [Festlegen der Eigenschaften einer Datenflusskomponente](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## Verwandte Inhalte  
  
-   Blogeintrag, [Raw Files Are Awesome](http://www.sqlservercentral.com/blogs/stratesql/archive/2011/1/1/31-days-of-ssis-_1320_-raw-files-are-awesome-_2800_1_2F00_31_2900_.aspx), auf sqlservercentral.com  
  
## Siehe auch  
 [Rohdatendatei-Ziel](../../integration-services/data-flow/raw-file-destination.md)   
 [Datenfluss](../../integration-services/data-flow/data-flow.md)  
  
  
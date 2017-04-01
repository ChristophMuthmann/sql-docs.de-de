---
title: "EventString-Element (DTA) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "XML"
helpviewer_keywords: 
  - "EventString-Element"
ms.assetid: f76c37b4-2f6e-4274-8ee2-87e89d98e8a2
caps.latest.revision: 12
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 12
---
# EventString-Element (DTA)
  Gibt eine auf einem [!INCLUDE[tsql](../../includes/tsql-md.md)]-Skript basierende Arbeitsauslastung direkt in der XML-Eingabedatei an.  
  
## Syntax  
  
```  
  
<Workload>  
    <EventString Weight="...">  
    ...code removed here...  
    </EventString>  
</Workload>  
```  
  
## Elementattribute  
  
|Attribut|Beschreibung|  
|---------------|-----------------|  
|**Weight**|Optional. Gibt den Gewichtungsfaktor der Abfrage (ein Faktor für die Wichtigkeit) für das angegebene Ereignis an. Sie können die Gewichtung mit einem **float** -Datentyp angeben. Beispiel: **Weight**="100.01". Der Mindestwert für **Weight** ist "0".|  
  
## Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|**Datentyp und -länge**|**string**, unbegrenzte Länge.|  
|**Standardwert**|Keine.|  
|**Vorkommen**|Einmalig erforderlich, wenn kein anderer Arbeitsauslastungstyp angegeben ist. Sie müssen ein untergeordnetes **EventString**-, **File**- oder **Database** -Element für das übergeordnete **Workload** -Element angeben. Es kann jedoch nur ein Typ verwendet werden. Wenn Sie beispielsweise eine Arbeitsauslastung mit dem **EventString** -Element angeben, können Sie in dieser XML-Eingabedatei keine Arbeitsauslastung mit dem **File** -Element angeben.|  
  
## Elementbeziehungen  
  
|Beziehung|Elemente|  
|------------------|--------------|  
|**Übergeordnetes Element**|[Workload-Element &#40;DTA&#41;](../../tools/dta/workload-element-dta.md)|  
|**Untergeordnete Elemente**|Keine.|  
  
## Beispiel  
 Ein Beispiel für die Verwendung dieses Elements finden Sie unter [Beispiel für eine XML-Eingabedatei mit Inlinearbeitsauslastung &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-inline-workload-dta.md).  
  
## Siehe auch  
 [XML-Eingabedateireferenz &#40;Datenbankoptimierungsratgeber&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
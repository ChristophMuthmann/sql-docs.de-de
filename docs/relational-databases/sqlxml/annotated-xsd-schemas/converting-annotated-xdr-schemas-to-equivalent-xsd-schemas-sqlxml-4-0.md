---
title: Konvertieren von XDR-Schemas in gleichbedeutende XSD-Schemas (SQLXML 4.0) versehen | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- annotated XDR schemas, converting schemas
- annotated XSD schemas, converting schemas
- XDR to XSD Converter tool [SQLXML]
- XDR schemas [SQLXML], converting
- converting annotated schemas
- mapping schema [SQLXML], conversions
- XSD schemas [SQLXML], converting schemas
ms.assetid: 151c94a8-66d3-4c46-a5ff-a22df456940a
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a841cf9e5bcfe3c1de5c199fa29984c709631598
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="converting-annotated-xdr-schemas-to-equivalent-xsd-schemas-sqlxml-40"></a>Konvertieren von XDR-Schemas mit Anmerkungen in gleichbedeutende XSD-Schemas (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Die XSD-Sprache (XML Schema Definition) ist Nachfolger der XDR-Sprache (XML-Data Reduced) für Schemadefinitionen. Nachdem XSD ab [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 unterstützt wird, wird davon ausgegangen, dass neue Schemas mit Anmerkungen mit XSD erstellt werden. SQLXML 4.0 umfasst ein Konvertierungstool für die Umwandlung von XDR in XSD, das die Konvertierung vorhandener XDR-Schemas mit Anmerkungen in entsprechende XSD-Schemas erleichtern soll.  
  
> [!IMPORTANT]  
>  Verwenden Sie dieses Tool nur, wenn Sie XDR-Schemas mit Anmerkungen in mit SQLXML 4.0 zu verwendendes XSD konvertieren möchten. Dies ist kein universelles XDR-in-XSD-Konvertierungstool. Die konvertierten XSD-Schemas verhalten sich unter Umständen anders als die ursprünglichen XDR-Schemas, wenn sie in anderen Umgebungen verwendet werden.  
  
 Wenn in der XDR-Eingabedatei die Codierung innerhalb der XML-Deklaration angegeben wird, dann wird diese Codierung für die generierte XSD-Ausgabedatei verwendet.  
  
 Das Konvertierungstool (Cvtschema.exe) wird im Ordner Programme\SQLXML 4.0\bin installiert und an der Eingabeaufforderung ausgeführt.  
  
 Das ist die allgemeine Syntax:  
  
```  
cvtschema XDRFileName, [-y], [-w] [-?]  
```  
  
 Erläuterungen:  
  
 XDRFileName  
 Der Name der XDR-Datei, die in XSD konvertiert werden soll. Das Tool liest die XDR-Eingabedatei und erstellt im aktuellen Arbeitsverzeichnis eine XSD-Ausgabedatei. Wenn die Eingabedatei über die Namenerweiterung .XDR oder .XML verfügt, wird eine XSD-Ausgabedatei gleichen Namens mit der Erweiterung .XSD erstellt. Wenn die Eingabedatei-Dateinamenerweiterung ist als XML oder .xdr (bzw. wenn die Erweiterung fehlt), wird die Ausgabedatei mit demselben Namen erstellt, und die XSD-Erweiterung wird auf den Namen der Eingabedatei angehängt. Wenn der Name der XDR-Eingabedatei beispielsweise SampleFile.abc lautet, wird das resultierende XSD unter dem Namen SampleFile.abc.xsd gespeichert.  
  
 -y  
 (Optional) Überschreibt die vorhandene XSD-Datei mit der XSD-Datei, die vom Konvertierungstool generiert wird. Wenn dieses Flag nicht angegeben wird, fordert Sie das Tool auf anzugeben, ob die vorhandene XSD-Datei überschrieben werden soll, und gibt Ihnen die Möglichkeit, den Namen der Ausgabedatei zu ändern.  
  
 -w  
 (Optional) Gibt im Konvertierungsprozess des Tools generierte Warnungen zurück, die nicht schwerwiegend sind. Standardmäßig zeigt das Tool nur Meldungen für schwerwiegende Fehler an.  
  
 -?  
 Gibt eine Liste von Optionen, die Sie angeben können, mit **Cvtschema**, zusammen mit einer Erklärung.  
  
## <a name="see-also"></a>Siehe auch  
 [Zuordnen von XSD-Datentypen zu XPath-Datentypen &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/mapping-xsd-data-types-to-xpath-data-types-sqlxml-4-0.md)   
 [XSD-Anmerkungen &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/xsd-annotations-sqlxml-4-0.md)  
  
  

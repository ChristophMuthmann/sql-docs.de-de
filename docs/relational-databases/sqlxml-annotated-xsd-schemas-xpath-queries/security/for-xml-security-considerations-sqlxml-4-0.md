---
title: "FOR XML-Sicherheitsüberlegungen (SQLXML 4.0) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- NESTED mode
- client-side XML formatting
- FOR XML clause, security
- server-side XML formatting
- AUTO mode
- security [SQLXML], FOR XML
ms.assetid: facba279-df93-475b-ad43-0043dc5bae03
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4491ae8cd6a9d2f52de101180b279efdded25316
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="for-xml-security-considerations-sqlxml-40"></a>FOR XML-Sicherheitsüberlegungen (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Der FOR XML AUTO-Modus erstellt eine XML-Hierarchie, in der Elementnamen Tabellennamen und Attributnamen Spaltennamen zugeordnet werden. Somit werden die Datenbanktabelle und die Spalteninformationen verfügbar gemacht. Sie können die Datenbankinformationen ausblenden, wenn Sie den AUTO-Modus (serverseitige Formatierung) verwenden, indem Sie Tabellen- und Spaltenaliasse in der Abfrage angeben. Diese Aliasse werden in dem resultierenden XML-Dokument als Element- und Attributsnamen zurückgegeben.  
  
 Die folgende Abfrage gibt beispielsweise den AUTO-Modus an, daher wird die XML-Formatierung auf dem Server durchgeführt:  
  
```  
SELECT C.FirstName as F,C.LastName as L   
FROM Person.Contact C   
FOR XML AUTO  
```  
  
 Im resultierenden XML-Dokument werden die Aliasse für Element- und Attributsnamen verwendet:  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
  <C F="Nancy" L="Fuller" />   
  <CE F="Andrew" L="Peacock" />   
  <C F="Janet" L="Leverling" />   
  ...  
</root>  
```  
  
 Wenn Sie den NESTED-Modus (clientseitige Formatierung) verwenden, werden Aliasse nur für Attribute im resultierenden XML-Dokument zurückgegeben. Die Namen der Basistabellen werden immer als Elementnamen zurückgegeben. Die folgende Abfrage gibt beispielsweise den NESTED-Modus an.  
  
```  
SELECT C.FirstName as F,C.LastName as L   
FROM Person.Contact C   
FOR XML AUTO  
```  
  
 Im resultierenden XML-Dokument werden die Namen der Basistabellen als Elementnamen zurückgegeben; Tabellenaliasse werden nicht verwendet:  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
  <Person.Contact F="Nancy" L="Fuller" />   
  <Person.Contact F="Andrew" L="Peacock" />   
  <Person.Contact F="Janet" L="Leverling" />   
       ...  
</root>  
```  
  
  

---
title: "Einführung in DiffGrams für SQLXML 4.0 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- annotations [SQLXML]
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: 1902d67f-baf3-46e6-a36c-b24b5ba6f8ea
caps.latest.revision: "10"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a653d706808ecb4d25490ad661125ffa4d81c5a4
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="introduction-to-diffgrams-in-sqlxml-40"></a>Einführung in DiffGrams für SQLXML 4.0
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]Dieses Thema enthält eine kurze Einführung in DiffGrams.  
  
## <a name="diffgram-format"></a>DiffGram-Format  
 Das allgemeine DiffGram-Format sieht folgendermaßen aus:  
  
```  
<?xml version="1.0"?>  
<diffgr:diffgram   
         xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"  
         xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1"  
         xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
   <DataInstance>  
      ...  
   </DataInstance>  
   [<diffgr:before>  
        ...  
   </diffgr:before>]  
  
   [<diffgr:errors>  
        ...  
   </diffgr:errors>]  
</diffgr:diffgram>  
```  
  
 Das DiffGram-Format besteht aus den folgenden Blöcken:  
  
 **\<DataInstance >**  
 Der Name dieses Elements **DataInstance**, wird in dieser Dokumentation zu Erklärungszwecken verwendet. Wenn das DiffGram-Objekt aus einem Dataset in .NET Framework, den Wert des generiert wurden z. B. die **Namen** Eigenschaft des Datasets als Namen für dieses Element verwendet werden würde. Dieser Block enthält nach der Änderung alle relevanten Daten, möglicherweise auch die Daten, die nicht geändert wurden. Das DiffGram-Verarbeitungslogik ignoriert die Elemente in diesem Block für die die **diffgr: HasChanges** -Attribut nicht angegeben ist.  
  
 **\<Diffgr: vor dem >**  
 Dieser optionale Block enthält die ursprünglichen Datensatzinstanzen (Elemente), die aktualisiert oder gelöscht werden müssen. Alle Datenbanktabellen (aktualisiert oder gelöscht) geändert wird durch das DiffGram-Objekt muss werden als Elemente der obersten Ebene in der  **\<vor >** Block.  
  
 **\<diffgr: errors >**  
 Dieser optionale Block wird von der DiffGram-Verarbeitungslogik ignoriert.  
  
## <a name="diffgram-annotations"></a>DiffGram-Anmerkungen  
 Diese Anmerkungen werden im DiffGram-Namespace definiert **"Urn: Schemas-Microsoft-com: XML-Diffgram-01"**:  
  
 **id**  
 Dieses Attribut wird verwendet, um die Elemente in der  **\<vor >** und  **\<DataInstance >** blockiert.  
  
 **hasChanges**  
 Für eine INSERT- oder Update-Vorgang, der aktualisierenvorgang muss dieses Attribut mit dem Wert **eingefügt** oder **geändert**. Wenn dieses Attribut nicht vorhanden ist, wird das entsprechende Element in der  **\<DataInstance >** wird durch die Verarbeitung ignoriert Logik und keine Updates ausgeführt werden. Funktionierende Beispiele finden Sie unter [DiffGram-Beispiele &#40; SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).  
  
 **parentID**  
 Mit diesem Attribut werden Über-/Unterordnungsbeziehungen unter den Elementen des DiffGrams angegeben. Dieses Attribut wird nur in der \<vor > Block. Es wird von SQLXML beim Übernehmen von Updates genutzt. Anhand der Über-/Unterordnungsbeziehungen wird die Reihenfolge bestimmt, in der die Elemente des DiffGrams verarbeitet werden.  
  
## <a name="understanding-the-diffgram-processing-logic"></a>Grundlegendes zur DiffGram-Verarbeitungslogik  
 Die DiffGram-Verarbeitungslogik verwendet bestimmte Regeln, um zu bestimmen, ob es sich bei einem Vorgang um einen Einfüge-, Aktualisieren- oder Löschvorgang handelt. Diese Regeln werden in der folgenden Tabelle beschrieben.  
  
|Vorgang|Description|  
|---------------|-----------------|  
|Insert|Ein DiffGram zeigt einen Einfügevorgang an, wenn ein Element wird, in angezeigt der  **\<DataInstance >** Block jedoch nicht im entsprechenden  **\<vor >** Block und der **diffgr: HasChanges** -Attribut angegeben ist (**diffgr: HasChanges = inserted**) für das Element. In diesem Fall fügt das DiffGram die Datensatzinstanz, die im angegebenen der  **\<DataInstance >** -Block in der Datenbank.<br /><br /> Wenn die **diffgr: HasChanges** -Attribut nicht angegeben ist, wird das Element von der Verarbeitungslogik ignoriert und kein Einfügevorgang ausgeführt. Funktionierende Beispiele finden Sie unter [DiffGram-Beispiele &#40; SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).|  
|Update|Das DiffGram zeigt einen Updatevorgang an, wenn ein in Element der \<vor > Block in ein entsprechendes Element vorhanden ist die  **\<DataInstance >** Block (d. h. beide Elemente haben eine **diffgr: ID** Attribut mit demselben Wert) und die **diffgr: HasChanges** -Attribut angegeben ist, mit dem Wert **geändert** auf das Element in der  **\<DataInstance >** Block.<br /><br /> Wenn die **diffgr: HasChanges** -Attribut nicht angegeben ist, auf das Element in der  **\<DataInstance >** Block, von der Verarbeitungslogik ein Fehler zurückgegeben. Funktionierende Beispiele finden Sie unter [DiffGram-Beispiele &#40; SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).<br /><br /> Wenn **diffgr: parentId** wird angegeben, der  **\<vor >** blockieren, die über-/ unterordnungsbeziehung von Elementen, die vom angegebenen **ParentID** kommen in bestimmen die Reihenfolge, in dem Datensätze aktualisiert werden.|  
|DELETE|Ein DiffGram zeigt einen Löschvorgang an, wenn ein Element wird, in angezeigt der  **\<vor >** Block jedoch nicht im entsprechenden  **\<DataInstance >** Block. In diesem Fall löscht das DiffGram die Datensatzinstanz, die im angegebenen der  **\<vor >** Block aus der Datenbank. Funktionierende Beispiele finden Sie unter [DiffGram-Beispiele &#40; SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).<br /><br /> Wenn **diffgr: parentId** wird angegeben, der  **\<vor >** blockieren, die über-/ unterordnungsbeziehung von Elementen, die vom angegebenen **ParentID** kommen in bestimmen die Reihenfolge, in dem Datensätze gelöscht werden.|  
  
> [!NOTE]  
>  DiffGrams können keine Parameter übergeben werden.  
  
  

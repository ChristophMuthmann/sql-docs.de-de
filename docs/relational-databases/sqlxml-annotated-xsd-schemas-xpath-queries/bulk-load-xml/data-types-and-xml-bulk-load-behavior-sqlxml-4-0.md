---
title: Datentypen und XML-Massenladen (SQLXML 4.0)-Ladeverhalten | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- bulk load [SQLXML], data types
- data types [SQLXML], XML Bulk Load
- XML Bulk Load [SQLXML], data types
ms.assetid: d1ac1939-1f6c-4398-b7a7-a79ca608a4f1
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7d5e25e9d3a2df2e15c2dc9bf86d6d90acd1d450
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="data-types-and-xml-bulk-load-behavior-sqlxml-40"></a>Datentypen und XML-Massenladenverhalten (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Die Datentypen, die im Zuordnungsschema angegeben werden (XSD- oder XDR-Typ und **SQL: DataType**) werden im Allgemeinen ignoriert werden, außer in den folgenden Fällen:  
  
 Bei XSD:  
  
-   Wenn der Typ ist **"DateTime"** oder **Zeit**, geben Sie die **SQL: DataType** da XML-Massenladen, die vor dem Senden der Daten an Microsoft Datenkonvertierungausführt[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Wird von Massenladen in eine Spalte mit **"uniqueidentifier"** Geben Sie in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] und der XSD-Wert ist eine GUID, die enthält geschweifte Klammern ({und}), Sie müssen angeben, **SQL: datatype = "Uniqueidentifier"** an Entfernen Sie die geschweiften Klammern, bevor der Wert in die Spalte eingefügt wird. Wenn **SQL: DataType** nicht angegeben wird, wird der Wert in geschweiften Klammern gesendet, und der Vorgang schlägt fehl.  
  
 Weitere Informationen zu **SQL: DataType**, finden Sie unter [Datentypumwandlungen und die SQL: DataType-Anmerkung &#40; SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md).  
  
 Bei XDR:  
  
-   Wenn die **dt: Type** ist **"DateTime"**, **Zeit**, **dateTime.tz**, oder **time.tz**, müssen Sie beide angeben die **dt: Type** und **SQL: DataType** Datentypen, da XML-Massenladen eine Datenkonvertierung durchführt, bevor er Daten sendet [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Wenn Ihre XML-Daten vom Typ **Uuid**, **SQL: DataType** muss angegeben werden; **dt: Type = "Uuid"** ist erforderlich, es sei denn, die Daten um Zeichenfolgendaten handelt. Wenn Sie keinen angeben **Dt:uuid**, XML-Massenladen Zeichenfolgen mit geschweiften Klammern akzeptiert (und entfernt diese ggf.).  
  
-   Wenn die XML-Daten sind **bin. Base64** oder **bin.hex**, geben Sie den XML-Datentyp mit **dt: Type**. XML-Massenladen lädt die Daten dann als Hexadezimaldarstellung der Daten in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
  

---
title: Beibehalten von gefilterten und hierarchische Recordsets | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- filtered Recordset persistence [ADO]
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: d01aeb4d-4e43-450b-b3f2-0c27eaaf9f86
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6d7ad27e3694b7a92e560170e699f62d76d5e6b0
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="persisting-filtered-and-hierarchical-recordsets"></a>Beibehalten von gefiltert und hierarchische Recordsets
Wenn die [Filter](../../../ado/reference/ado-api/filter-property.md) Eigenschaft gilt für die **Recordset**, nur die Zeilen, die unter dem Filter zugänglichen gespeichert sind. Wenn die **Recordset** wird eine hierarchische Struktur der aktuellen untergeordneten **Recordset** und seine untergeordneten Elemente gespeichert sind, einschließlich der übergeordneten **Recordset**. Wenn die **speichern** Methode einer untergeordneten **Recordset** wird aufgerufen, das untergeordnete Element und alle seine untergeordneten Elemente werden gespeichert, das übergeordnete Element ist jedoch nicht. Weitere Informationen zu hierarchischen **Recordsets**, finden Sie unter [Datenstrukturierung](../../../ado/guide/data/data-shaping.md).  
  
> [!NOTE]
>  Einige Einschränkungen gelten beim Speichern der hierarchischen **Recordsets** (Daten-Shapes) im XML-Format. Weitere Informationen finden Sie unter [beibehalten von Datensätzen im XML-Format](../../../ado/guide/data/persisting-records-in-xml-format.md).

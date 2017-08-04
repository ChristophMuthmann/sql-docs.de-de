---
title: Union All Transformation Editor | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.unionalltransformation.f1
helpviewer_keywords:
- Union All Transformation Editor
ms.assetid: 32fbc1c1-da83-4684-9479-31fc3e2df98c
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 496d8da2d879df996181854b1fcffca9fd6537d3
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="union-all-transformation-editor"></a>Transformations-Editor für UNION ALL
  Mithilfe des Dialogfelds **Transformations-Editor für UNION ALL** können Sie mehrere Eingaberowsets zu einem einzigen Ausgaberowset zusammenführen. Durch das Einschließen der Transformation für UNION ALL in einen Datenfluss können Sie Daten aus mehreren Datenflüssen zusammenführen, komplexe Datasets durch Verschachteln der Transformationen für UNION ALL erstellen und Zeilen erneut zusammenführen, nachdem Sie Fehler in den Daten korrigiert haben.  
  
 Weitere Informationen zur Transformation für UNION ALL finden Sie unter [Union All Transformation](../../../integration-services/data-flow/transformations/union-all-transformation.md).  
  
## <a name="options"></a>enthalten  
 **Name der Ausgabespalte**  
 Geben Sie einen Alias für jede Spalte ein. Standardmäßig wird der Name der Eingabespalte von der ersten (Referenz-)Eingabe verwendet. Sie können jedoch auch einen beschreibenden Namen angeben, sofern dieser eindeutig ist.  
  
 **Eingabe 1 für UNION ALL**  
 Wählen Sie eine Eingabespalte aus der Liste der verfügbaren Eingabespalten in der ersten (Referenz-)Eingabe aus. Die Metadaten der zugeordneten Spalten müssen übereinstimmen.  
  
 **Eingabe n für UNION ALL**  
 Wählen Sie eine Eingabespalte aus der Liste der verfügbaren Eingabespalten in den folgenden Eingaben aus. Die Metadaten der zugeordneten Spalten müssen übereinstimmen.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Meldungsreferenz von Integration Services-Fehler](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Zusammenführen von Daten mithilfe der Union All-Transformation](../../../integration-services/data-flow/transformations/merge-data-by-using-the-union-all-transformation.md)   
 [Transformation für zusammenführen](../../../integration-services/data-flow/transformations/merge-transformation.md)   
 [Transformation für Zusammenführungsjoin](../../../integration-services/data-flow/transformations/merge-join-transformation.md)  
  
  

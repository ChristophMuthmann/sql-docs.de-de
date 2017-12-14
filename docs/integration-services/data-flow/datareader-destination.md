---
title: DataReader-Ziel | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.dts.designer.datareaderdest.f1
helpviewer_keywords:
- DataReader destination
- destinations [Integration Services], DataReader
ms.assetid: 56fcc4bf-c901-42c3-a71d-110039293431
caps.latest.revision: "30"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 86e80aebc070af07e700ac24e913214500bae9f9
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="datareader-destination"></a>DataReader-Ziel
  Das DataReader-Ziel macht die Daten in einem Datenfluss mithilfe der **DataReader** -Schnittstelle von ADO.NET verfügbar. Die Daten können dann von anderen Anwendungen verwendet werden. Beispielsweise können Sie die Datenquelle eines [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichts so konfigurieren, dass das Ergebnis der Ausführung eines [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Pakets verwendet wird. Dazu erstellen Sie einen Datenfluss, der das DataReader-Ziel implementiert.  
  
 Informationen zum programmgesteuerten Zugriff auf Werte im DataReader-Ziel und zum programmgesteuerten Lesen dieser Werte finden Sie unter [Laden der Ausgabe eines lokalen Pakets](../../integration-services/run-manage-packages-programmatically/loading-the-output-of-a-local-package.md).  
  
## <a name="configuration-of-the-datareader-destination"></a>Konfiguration des DataReader-Ziel  
 Sie können einen Timeoutwert für das DataReader-Ziel angeben und konfigurieren, ob das Ziel einen Fehler erzeugen soll, wenn ein Timeout auftritt. Ein Timeout tritt auf, wenn die Anwendung nicht innerhalb der angegebenen Zeit Daten anfordert.  
  
 Das DataReader-Ziel hat eine Eingabe. Eine Fehlerausgabe wird nicht unterstützt.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Benutzerdefinierte Eigenschaften des DataReader-Ziels](../../integration-services/data-flow/datareader-destination-custom-properties.md)  
  
 Informationen zum Festlegen der Eigenschaften finden Sie unter [Festlegen der Eigenschaften einer Datenflusskomponente](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
  

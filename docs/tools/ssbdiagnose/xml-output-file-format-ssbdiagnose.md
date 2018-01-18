---
title: XML-Format der Ausgabedatei (Ssbdiagnose) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssbdiagnose
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XML output file format [ssbdiagnose]
- ssbdiagnose
ms.assetid: 3ceb991b-6f15-4504-8828-de5adf448bc5
caps.latest.revision: "13"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 11c9dbc6f279782a0083a12b0ce304f5959e58ad
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="xml-output-file-format-ssbdiagnose"></a>Format der XML-Ausgabedatei (ssbdiagnose)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Die **Ssbdiagnose** Hilfsprogramm die Ausgabe als XML-Datei bereitgestellt, bei der Ausführung mit der **- XML-** wechseln. Die XML-Ausgabedatei enthält Headerinformationen und die Fehler, die in der analysierten [!INCLUDE[ssSB](../../includes/sssb-md.md)] -Konfiguration oder Konversation gefunden wurden. Sie können eine Anwendung schreiben, um die in der Datei aufgelisteten Fehler zu analysieren oder einen entsprechenden Bericht zu erstellen. Die XML-Datei kann auch in einem allgemeinen XML-Editor wie XML Editor angezeigt werden.  
  
 Eine **ssbdiangose** -Ausgabedatei enthält ein DiagnosticInformation-Stammelement mit zwei untergeordneten Typen:  
  
-   Einem Banner-Element mit Headerinformationen  
  
-   Einem Issue-Element für jedes Problem, das von **ssbdiagnose**gemeldet wird  
  
## <a name="diagnosticinformation-root-element"></a>DiagnosticInformation-Stammelement  
  
-   [DiagnosticInformation-Element &#40; Ssbdiagnose &#41;](../../tools/ssbdiagnose/diagnosticinformation-element-ssbdiagnose.md)  
  
## <a name="banner-element"></a>Banner-Element  
  
-   [Banner-Element &#40; Ssbdiagnose &#41;](../../tools/ssbdiagnose/banner-element-ssbdiagnose.md)  
  
## <a name="issue-element"></a>Issue-Element  
  
-   [Issue-Element &#40; Ssbdiagnose &#41;](../../tools/ssbdiagnose/issue-element-ssbdiagnose.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Ssbdiagnose-Hilfsprogramm &#40; Service Broker &#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
  

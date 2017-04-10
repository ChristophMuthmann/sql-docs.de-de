---
title: "In Paketbereitstellungsmodell konvertieren (Dialogfeld) | Microsoft Docs"
ms.custom: ""
ms.date: "08/26/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.bids.converttolegacydeployment.f1"
ms.assetid: 9e60a34a-10f7-48d1-966f-b3ff236ab4b7
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# In Paketbereitstellungsmodell konvertieren (Dialogfeld)
  Mit dem Befehl **In Paketbereitstellungsmodell konvertieren** können Sie ein Paket auf dem Paketbereitstellungsmodell konvertieren, nachdem das Projekt und jedes Paket im Projekt auf Kompatibilität mit dem Modell überprüft wurden. Wenn ein Paket für ein Projektbereitstellungsmodell eindeutige Funktionen verwendet, z. B. Parameter, dann kann das Paket nicht konvertiert werden.  
  
## Aufgabenliste  
 Für das Konvertieren eines Pakets auf ein Paketbereitstellungsmodell sind zwei Schritte erforderlich.  
  
1.  Wenn Sie den Befehl **In Paketbereitstellungsmodell konvertieren** aus dem Menü **Projekt** auswählen, werden das Projekt und jedes Paket auf Kompatibilität mit diesem Modell überprüft. Die Ergebnisse werden in der Tabelle **Ergebnisse** angezeigt.  
  
     Wenn das Projekt oder ein Paket den Kompatibilitätstest nicht besteht, klicken Sie in der Spalte **Ergebnis** auf **Fehler** , um weitere Informationen zu erhalten. Klicken Sie auf **Bericht speichern** , um eine Kopie dieser Informationen in einer Textdatei zu speichern.  
  
2.  Wenn das Projekt und alle Pakete den Kompatibilitätstest bestehen, klicken Sie auf **OK** , um das Paket zu konvertieren.  
  
> **HINWEIS:** Verwenden Sie den **Assistenten für die Konvertierung von Integration Services-Projekten**, um ein Projekt ins Projektbereitstellungsmodell zu konvertieren. Weitere Informationen finden Sie unter [Integration Services Project Conversion Wizard](https://msdn.microsoft.com/library/hh213290.aspx).  
  
## Siehe auch  
 [Legacy-Paketbereitstellung &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md)   
 [Assistent für die Konvertierung von Integration Services-Projekten](../../integration-services/packages/integration-services-project-conversion-wizard.md)  
  
  
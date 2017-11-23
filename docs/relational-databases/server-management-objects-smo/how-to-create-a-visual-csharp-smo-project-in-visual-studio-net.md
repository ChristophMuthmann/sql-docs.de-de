---
title: Erstellen ein Visual c# SMO-Projekts in Visual Studio .NET | Microsoft Docs
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: Visual C# [SMO]
ms.assetid: 1e7abb16-23a0-4a18-91ad-253261e6bf84
caps.latest.revision: "43"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 2fb8a8bd7527a14df4447fd4c7a49e92647b9e09
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="how-to-create-a-visual-c-smo-project-in-visual-studio-net"></a>Vorgehensweise: erstellen ein Visual c# SMO-Projekts in Visual Studio .NET
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Dieser Abschnitt beschreibt, wie eine einfache SMO-Konsolenanwendung zu erstellen.  
  
 In diesem Beispiel werden Namespaces importiert. Hierdurch kann das Programm auf SMO-Typen verweisen. Importiert die **Agent** Namespaces ist optional. Verwenden sie beim Schreiben eines Programms von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Die **allgemeine** Namespace ist erforderlich, um das Herstellen einer sicheren Verbindung mit der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Die **SqlClient** Namespace wird verwendet, um die SQL-Ausnahmefehler zu verarbeiten.  
  
### <a name="creating-a-visual-c-smo-project-in-visual-studionet"></a>Erstellen eines Visual c# SMO-Projekts in Visual Studio.NET  
  
1. Starten Sie Visual Studio
  
2. Auf der **Datei** Menü klicken Sie auf **neu** und dann **Projekt**.  Das Dialogfeld **Neues Projekt** wird angezeigt.   
  
3. In der [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **installiert** Bereich navigieren Sie zu **Vorlagen**\\**Visual C#-**\\**Windows** und wählen Sie **Konsolenanwendung**.  
  
4. (Optional) In der **Namen** Text geben den Namen der neuen Anwendung.  

5. Klicken Sie auf **OK** die Konsole Application-Vorlage zu laden.  

6. Befolgen Sie die Anweisungen auf [Installieren von SMO](installing-smo.md) zum Installieren des Pakets für das Projekt zu verweisen.
  
7. Klicken Sie im Menü **Ansicht** auf **Code**.
    
8. Geben Sie im Code vor der Namespace-Anweisung die folgenden **mit** Anweisungen, die die Typen im SMO-Namespace zu qualifizieren:
  
    ```  
    using Microsoft.SqlServer.Management.Smo;  
    using Microsoft.SqlServer.Management.Common;  
    ```  
  
15. SMO verfügt über verschiedene Namespaces unter Microsoft.SqlServer.Management.Smo, z. B. Microsoft.SqlServer.Management.Smo.Agent. Fügen Sie diese Namespaces an, wie sie benötigt werden.  
  
16. Sie können jetzt den SMO-Code hinzufügen.  
  
  

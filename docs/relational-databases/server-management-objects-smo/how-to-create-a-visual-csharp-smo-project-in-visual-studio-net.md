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
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: Visual C# [SMO]
ms.assetid: 1e7abb16-23a0-4a18-91ad-253261e6bf84
caps.latest.revision: "43"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 220c190a88a1b5c5d38591905e9bb1060a2f4509
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/12/2018
---
# <a name="how-to-create-a-visual-c-smo-project-in-visual-studio-net"></a>Vorgehensweise: erstellen ein Visual c# SMO-Projekts in Visual Studio .NET
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  In diesem Abschnitt wird beschrieben, wie eine einfache SMO-Konsolenanwendung erstellt wird.  
  
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
  
  

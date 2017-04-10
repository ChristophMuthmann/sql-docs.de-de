---
title: "Konfigurieren der Protokollierung mithilfe einer gespeicherten Konfigurationsdatei | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Container [Integration Services], Protokolle"
  - "Protokolle [Integration Services], Container"
ms.assetid: e5fdbbcb-94ca-4912-aa7c-0d89cebbd308
caps.latest.revision: 42
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 42
---
# Konfigurieren der Protokollierung mithilfe einer gespeicherten Konfigurationsdatei
  In diesem Verfahren wird beschrieben, wie die Protokollierung für neue Container in einem Paket konfiguriert wird, indem eine zuvor gespeicherte Protokollierungskonfigurationsdatei geladen wird.  
  
 Alle Container in einem Paket verwenden standardmäßig dieselbe Protokollierungskonfiguration wie der übergeordnete Container. Die Tasks in einer Foreach-Schleife verwenden z. B. dieselbe Protokollierungskonfiguration wie die Foreach-Schleife.  
  
### So konfigurieren Sie die Protokollierung für einen Container  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Klicken Sie im Menü **SSIS** auf **Protokollierung**.  
  
3.  Erweitern Sie die Paketbaumansicht, und wählen Sie den zu konfigurierenden Container aus.  
  
4.  Wählen Sie auf der Registerkarte **Anbieter und Protokolle** die Protokolle aus, die Sie für den Container verwenden möchten.  
  
    > [!NOTE]  
    >  Sie können Protokolle nur auf Paketebene erstellen. Weitere Informationen finden Sie unter [Aktivieren der Paketprotokollierung in SQL Server Data Tools](../../integration-services/performance/enable-package-logging-in-sql-server-data-tools.md).  
  
5.  Klicken Sie auf die Registerkarte **Details** und dann auf **Laden**.  
  
6.  Suchen Sie die zu verwendende Protokollierungskonfigurationsdatei, und klicken Sie auf **Öffnen**.  
  
7.  Wählen Sie optional einen anderen zu protokollierenden Protokolleintrag aus, indem Sie das entsprechende Kontrollkästchen in der Spalte **Ereignisse** aktivieren. Klicken Sie auf **Erweitert** , um den für diesen Eintrag zu protokollierenden Informationstyp auszuwählen.  
  
    > [!NOTE]  
    >  Der neue Container enthält u. U. weitere Protokolleinträge, die für den Container nicht verfügbar sind, der ursprünglich zum Erstellen der Protokollierungskonfiguration verwendet wurde. Diese zusätzlichen Protokolleinträge müssen manuell ausgewählt werden, falls diese protokolliert werden sollen.  
  
8.  Um die aktualisierte Version der Protokollierungskonfiguration zu speichern, klicken Sie auf **Speichern**.  
  
9. Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  
  
## Siehe auch  
 [Integration Services-Protokollierung &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md)  
  
  
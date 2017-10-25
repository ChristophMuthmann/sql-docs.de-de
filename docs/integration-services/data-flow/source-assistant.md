---
title: Datenquellen-Assistenten | Microsoft Docs
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
- sql13.dts.designer.sourceassistant.f1
- sql13.dts.designer.addNewSource.f1
ms.assetid: 5ca9d821-7d61-4727-9133-5f9cb485c7f3
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9b7406edf9f7234db739730473772d77c42399ec
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="source-assistant"></a>Quellen-Assistent
  Mithilfe der Quellen-Assistenten-Komponente können Sie eine Quellkomponente und einen Verbindungs-Manager erstellen. Die Komponente befindet sich im Abschnitt **Favoriten** der SSIS-Toolbox.  
  
> [!NOTE]  
>  Der Quellen-Assistent ersetzt das Integration Services-Verbindungsprojekt und den entsprechenden Assistenten.  
  
## <a name="add-a-source-with-source-assistant"></a>Hinzufügen einer Quelle mit dem Datenquellen-Assistenten
Dieser Abschnitt enthält die Schritte zum Hinzufügen einer neuen Quelle mithilfe des Assistenten und führt ebenfalls die verfügbaren Optionen auf der **neue Quelle hinzufügen** Dialogfeld, die angezeigt werden, wenn Sie die Quellen-Assistenten in der SSIS-Designer ziehen.  

1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket, dem eine neue Quellkomponente hinzugefügt werden soll.  
  
2.  Ziehen Sie die **Quellen-Assistenten** -Komponente von der SSIS-Toolbox auf die Registerkarte **Datenfluss** . Sie sollten das Dialogfeld **Neue Quelle hinzufügen** sehen. Der nächste Abschnitt enthält Details zu den im Dialogfeld verfügbaren Optionen.  
  
3.  Wählen Sie den Zieltyp in der Liste **Typ** aus.  
  
4.  Wählen Sie einen vorhandenen Verbindungs-Manager in der **Verbindungs-Manager** aus, oder wählen Sie  **\<neu >** an einen neuen Verbindungs-Manager zu erstellen.  
  
5.  Wenn Sie einen vorhandenen Verbindungs-Manager auswählen, klicken Sie auf **OK** , um das Dialogfeld **Neues Ziel hinzufügen** zu schließen. Sie sollten nun das Ziel und die Verbindungs-Manager sehen, die dem Datenfluss hinzugefügt wurden.  
  
6.  Wenn Sie auf  **\<neu >** um einen neuen Verbindungs-Manager erstellen, sehen Sie eine **Verbindungs-Manager** (Dialogfeld), in dem Sie Parameter für die Verbindung angeben kann. Nachdem Sie einen neuen Verbindungs-Managers erstellt haben, werden das Ziel und der Verbindungs-Manager in SSIS-Designer angezeigt.  

## <a name="add-new-source-dialog-box"></a>Fügen Sie neue Datenquelle (Dialogfeld)
Die folgende Tabelle enthält Optionen zur Verfügung, in der **neue Quelle hinzufügen** (Dialogfeld).  
  
|Option|Description|  
|------------|-----------------|  
|Typen|Wählen Sie den Quelltyp aus, mit dem Sie eine Verbindung herstellen möchten.|  
|Verbindungs-Manager|Wählen Sie einen vorhandenen Verbindungs-Manager, oder klicken Sie auf  **\<neu >** an einen neuen Verbindungs-Manager zu erstellen.|  
|Nur installierte anzeigen|Geben Sie an, ob nur installierte Quellen angezeigt werden sollen.|  
|OK|Klicken Sie auf diese Schaltfläche, um die Änderungen zu speichern, und öffnen Sie die entsprechenden nachfolgenden Dialogfelder, um zusätzliche Optionen zu konfigurieren.| 
  

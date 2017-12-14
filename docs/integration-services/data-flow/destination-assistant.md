---
title: Ziel-Assistent | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.destinationassistant.f1
- sql13.DTS.DESIGNER.DESTINATIONASSIST.F1
ms.assetid: 10a40921-a2c2-4ac8-be28-311f8500fbf6
caps.latest.revision: "13"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 21ce9dc332f5a31fa95ea57e5cbe63a2757f198a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="destination-assistant"></a>Ziel-Assistent
  Der Ziel-Assistenten hilft beim Erstellen einer Zielkomponente und eines Verbindungs-Managers. Die Komponente befindet sich im Abschnitt **Favoriten** der SSIS-Toolbox.  
  
> [!NOTE]  
>  Der Ziel-Assistent ersetzt das Integration Services-Verbindungsprojekt und den entsprechenden Assistenten.  

## <a name="add-a-destination-with-destination-assistant"></a>Hinzufügen eines Ziels mit dem Ziel-Assistenten
In diesem Thema werden die Schritte beschrieben, um ein neues Ziel mithilfe des Ziel-Assistenten hinzuzufügen. Darüber hinaus werden die im Dialogfeld **Neues Ziel hinzufügen** verfügbaren Optionen aufgelistet, die angezeigt werden, wenn Sie den Ziel-Assistent per Drag &amp; Drop in den SSIS-Designer ziehen.  

1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket, dem eine neue Zielkomponente hinzugefügt werden soll.  
  
2.  Ziehen Sie die **Ziel-Assistenten** -Komponente von der SSIS-Toolbox auf die Registerkarte **Datenfluss** . Sie sollten das Dialogfeld **Neues Ziel hinzufügen** sehen. Der nächste Abschnitt enthält Details zu den im Dialogfeld verfügbaren Optionen.  
  
3.  Wählen Sie den Zieltyp in der Liste **Typ** aus.  
  
4.  Wählen Sie in der Liste **Verbindungs-Manager** einen vorhandenen Verbindungs-Manager aus. Wählen Sie alternativ **\<Neu>** aus, um einen neuen Verbindungs-Manager zu erstellen.  
  
5.  Wenn Sie einen vorhandenen Verbindungs-Manager auswählen, klicken Sie auf **OK** , um das Dialogfeld **Neues Ziel hinzufügen** zu schließen. Sie sollten nun das Ziel und die Verbindungs-Manager sehen, die dem Datenfluss hinzugefügt wurden.  
  
6.  Wenn Sie auf **\<Neu>** klicken, um einen neuen Verbindungs-Manager zu erstellen, sollten Sie ein **Verbindungs-Manager**-Dialogfeld sehen, in dem Sie Parameter für die Verbindung angeben können. Nachdem Sie einen neuen Verbindungs-Managers erstellt haben, werden das Ziel und der Verbindungs-Manager in SSIS-Designer angezeigt. 
  
## <a name="add-new-destination-dialog-box"></a>Neues Ziel hinzufügen (Dialogfeld)
In der folgenden Tabelle sind die Optionen im Dialogfeld **Neues Ziel hinzufügen** aufgeführt.  
  
|Option|Description|  
|------------|-----------------|  
|Typen|Wählen Sie den Zieltyp aus, mit dem Sie eine Verbindung herstellen möchten.|  
|Verbindungs-Manager|Wählen Sie einen vorhandenen Verbindungs-Manager aus, oder klicken Sie auf **\<Neu>**, um einen neuen Verbindungs-Manager zu erstellen.|  
|Nur installierte anzeigen|Geben Sie an, ob nur installierte Ziele angezeigt werden sollen.|  
|OK|Klicken Sie auf diese Schaltfläche, um die Änderungen zu speichern, und öffnen Sie die entsprechenden nachfolgenden Dialogfelder, um zusätzliche Optionen zu konfigurieren.|  

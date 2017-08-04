---
title: "Herstellen einer Verbindung mit einem MDS-Repository (MDS-Add-in für Excel) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8f427312-4c09-4c8b-b9f9-8b235557a74b
caps.latest.revision: 12
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 87931c60b791fd106d0476ac037e1dfcd4041fb2
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="connect-to-an-mds-repository-mds-add-in-for-excel"></a>Herstellen einer Verbindung mit einem MDS-Repository (MDS-Add-In für Excel)
  In [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]müssen Sie eine Verbindung mit einem MDS-Repository herstellen, bevor Sie Daten laden oder veröffentlichen können.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung für den Zugriff auf den Funktionsbereich **Explorer** verfügen.  
  
### <a name="to-connect-to-an-mds-repository"></a>So stellen Sie eine Verbindung mit einem MDS-Repository her  
  
1.  Klicken Sie in MDS [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]auf die Registerkarte **Masterdaten** , klicken Sie in der Gruppe **Verbinden und Laden** auf den Pfeil unter der Schaltfläche **Verbinden** , und klicken Sie auf **Verbindungen verwalten**.  
  
2.  Klicken Sie im Dialogfeld **Verbindungen verwalten** im Abschnitt **Neue Verbindung** auf **Neue Verbindung erstellen**.  
  
3.  Klicken Sie auf **Neu**.  
  
4.  Geben Sie im Dialogfeld **Neue Verbindung hinzufügen** im Feld **Beschreibung** eine Beschreibung für die Verbindung ein. Diese Verbindung wird angezeigt, wenn Sie auf den Pfeil unter der Schaltfläche **Verbinden** auf der Symbolleiste klicken.  
  
5.  In der **MDS-Serveradresse** geben die URL der [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] -Webanwendung ein, z. B. `http://contoso/mds`.  
  
    > [!NOTE]  
    >  Stellen Sie sicher, dass Sie den Computernamen verwenden und nicht "localhost".  
  
6.  Klicken Sie auf **OK**. Der Name wird im Abschnitt **Vorhandene Verbindungen** angezeigt.  
  
7.  Klicken Sie optional auf **Testen** , um die Verbindung zu testen. Ein Bestätigungs- oder Fehlerdialogfeld wird angezeigt. Klicken Sie auf **OK** , um es zu schließen.  
  
8.  Klicken Sie auf **Verbinden**. Der Bereich **Master Data Services** wird angezeigt.  
  
## <a name="next-steps"></a>Nächste Schritte  
  
-   [Export Data to Excel from Master Data Services](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md)  
  
-   [Filter Data before Exporting &#40;MDS Add-in for Excel&#41; (Filtern von Daten vor dem Exportieren (MDS-Add-In für Excel))](../../master-data-services/microsoft-excel-add-in/filter-data-before-exporting-mds-add-in-for-excel.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Verbindungen &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/connections-mds-add-in-for-excel.md)  
  
  

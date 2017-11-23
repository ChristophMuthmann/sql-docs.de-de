---
title: "Importieren Sie das SCOM Management Pack für PDW (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fa735041-8e58-4886-ae3b-36f3c6298b12
caps.latest.revision: "6"
ms.openlocfilehash: 2766219fc98a1a3f0174b2c33846fcedb0b74022
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="import-the-scom-management-pack-for-pdw"></a>Importieren Sie das SCOM Management Pack für PDW
Führen Sie diese Schritte aus, um die System Center Operations Manager (SCOM) Management Packs für SQL Server PDW zu importieren. Die Management Packs sind erforderlich, zum Überwachen von SQL Server PDW aus SCOM.  
  
## <a name="BeforeBegin"></a>Vorbereitungen  
**Erforderliche Komponenten**  
  
System Center Operationsmanager 2007 R2 muss installiert und aktiv sein.  
  
Die Management Packs müssen installiert sein. Finden Sie unter [installieren Sie die SCOM-Management Packs &#40; Analyseplattformsystem &#41; ](install-the-scom-management-packs.md).  
  
## <a name="Step1"></a>Schritt 1: Importieren Sie das SQL Server-Appliance Basis-Management Pack  
  
1.  Melden Sie sich bei dem Computer mit einem Konto an, das Mitglied der Rolle "Operations Manager-Administratoren" für die Operations Manager 2007-Verwaltungsgruppe ist.  
  
2.  Klicken Sie in der Betriebskonsole auf **Verwaltung**.  
  
3.  Mit der rechten Maustaste die **Management Packs** Knoten, und klicken Sie dann auf **Management Packs importieren**.  
  
    ![Klicken Sie auf die Management Packs importieren](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP.png "SCOM")  
  
4.  Wählen Sie in der Liste der Management Packs das ManagementPack, das Sie importieren möchten, klicken Sie auf **wählen**, und klicken Sie dann auf **hinzufügen**.  
  
    ![Management Pack-Liste](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP2.png "SCOM_IMP2")  
  
5.  Suchen Sie nach **Appliance** und danach einen Drilldown in SQL Server-Appliance Basis, und klicken Sie dann auf **hinzufügen** zwei Optionen.  
  
    ![SQL Server-Anwendungsbasis](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP3.png "SCOM_IMP3")  
  
6.  Nachdem die beiden Management Packs im unteren Bereich ausgewählten wurden, klicken Sie dann auf **OK**.  
  
    ![Auswählen beider Management Packs](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP4.png "SCOM_IMP4")  
  
7.  Klicken Sie auf **Installieren**.  
  
    ![Klicken Sie auf Installieren](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP5.png "SCOM_IMP5")  
  
8.  Sobald der Vorgang abgeschlossen ist, klicken Sie auf **schließen**.  
  
    ![Sobald der Vorgang abgeschlossen ist, klicken Sie auf Schließen](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP6.png "SCOM_IMP6")  
  
## <a name="Step2"></a>Importieren Sie das Überwachungspaket für Microsoft SQL Server 2008 R2 Parallel Data Warehouse-Appliance  
  
1.  Mit der rechten Maustaste die **Management Packs** Knoten, und klicken Sie dann auf **Management Packs importieren**.  
  
2.  Wählen Sie **von Datenträger hinzufügen**...  
  
    ![Mit der rechten Maustaste Management Packs](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW.png "SCOM_PDW")  
  
3.  Wechseln Sie zu dem Speicherort, in dem Sie die SQL Server PDW-Management Packs extrahiert, und wählen Sie die drei Management Packs, die im Abschnitt "Ausgewählten Management packs importieren" sind. Dazu können Sie die erste Vorlage, Umschalttaste Klicken und das letzte Lesezeichen auswählen. Nachdem alle ausgewählt werden, klicken Sie auf **öffnen**.  
  
    ![Management Packs auswählen](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW2.png "SCOM_PDW2")  
  
4.  Klicken Sie auf **Installieren**.  
  
    ![Klicken Sie auf Installieren](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW3.png "SCOM_PDW3")  
  
5.  Klicken Sie auf **Schließen**.  
  
    ![Klicken Sie auf Schließen](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW4.png "SCOM_PDW4")  
  
## <a name="next-step"></a>Nächster Schritt  
Nun, dass Sie die Management Packs importiert haben, mit dem nächsten Schritt fortfahren: [Konfigurieren von SCOM zum Überwachen Analytics Platform System &#40; Analyseplattformsystem &#41; ](configure-scom-to-monitor-analytics-platform-system.md).  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  

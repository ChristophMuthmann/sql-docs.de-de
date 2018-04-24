---
title: Importieren von SCOM-Management Pack - Analyseplattformsystem | Microsoft Docs
description: Führen Sie diese Schritte aus, um die System Center Operations Manager (SCOM) Management Packs für Analytics Platform System (APS) importieren. Die Management Packs sind erforderlich, Parallel Data Warehouse von SCOM überwacht.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: e60d87ae58b0804a0a7296f8b489df7441683c5b
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="import-the-scom-management-pack---analytics-platform-system"></a>Importieren Sie das SCOM-Management Pack - Analyseplattformsystem
Führen Sie diese Schritte aus, um die System Center Operations Manager (SCOM) Management Packs für Analytics Platform System (APS) importieren. Die Management Packs sind erforderlich, Parallel Data Warehouse von SCOM überwacht. 
  
## <a name="BeforeBegin"></a>Vorbereitungen  
**Erforderliche Komponenten**  
  
System Center Operationsmanager 2007 R2 muss installiert und aktiv sein.  
  
Die Management Packs müssen installiert sein. Finden Sie unter [Installation der SCOM-Management Packs &#40;Analyseplattformsystem&#41;](install-the-scom-management-packs.md).  
  
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
Nun, dass Sie die Management Packs importiert haben, mit dem nächsten Schritt fortfahren: [Konfigurieren von SCOM zum Überwachen Analytics Platform System &#40;Analyseplattformsystem&#41;](configure-scom-to-monitor-analytics-platform-system.md).  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  

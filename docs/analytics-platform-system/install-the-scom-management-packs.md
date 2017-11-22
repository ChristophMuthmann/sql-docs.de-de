---
title: Installieren Sie die SCOM-Management Packs (Analytics Platform System)
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
ms.assetid: ab3985d8-0a71-4b28-9d28-9886ae2a110f
caps.latest.revision: "16"
ms.openlocfilehash: f20048a70ef04bba475f9e8e6b58b24095f23f1a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="install-the-scom-management-packs"></a>Installieren Sie die SCOM-Management Packs
Führen Sie diese Schritte zum Herunterladen und installieren die System Center Operations Manager (SCOM) Management Packs für SQL Server PDW. Die Management Packs sind erforderlich, zum Überwachen von SQL Server PDW aus SCOM.  
  
## <a name="BeforeBegin"></a>Vorbereitungen  
**Erforderliche Komponenten**  
  
System Center Operations Manager muss installiert und aktiv sein. SQL Server PDW 2012 erfordert System Center Operations Manager 2007 R2, System Center Operations Manager 2012 oder System Center Operations Manager 2012 Servicepack 1.  
  
## <a name="Step1"></a>Schritt 1: Herunterladen der Management Packs  
Herunterladen der APS-PDW-arbeitsauslastung, die [System Center Management Pack für Microsoft Analytics Platform System](http://go.microsoft.com/fwlink/?LinkId=396857).  
  
Für die Verwaltung Appliance Herunterladen der [Base Management Pack für SQL Server Appliance](http://www.microsoft.com/en-us/download/details.aspx?displaylang=en&id=11436).  
  
Für frühere Versionen von PDW ohne APS Herunterladen der[System Center Monitoring Pack für Microsoft SQL Server 2012 Parallel Data Warehouse Appliance](http://go.microsoft.com/fwlink/p/?LinkId=282661).  
  
Für die arbeitsauslastung HDInsight Herunterladen der [System Center Management Pack für HDInsight](http://go.microsoft.com/fwlink/?LinkId=390208).  
  
## <a name="Step2"></a>Schritt 2: Installieren Sie die Management Packs  
  
### <a name="install-the-sql-server-appliance-base-management-pack"></a>Installieren Sie das SQL Server-Appliance Basis-Management Pack  
  
1.  Um die Installation auszuführen, doppelklicken Sie auf die heruntergeladene SQL Server Appliance Base Management Pack.  
  
2.  Akzeptieren Sie den Lizenzvertrag, und klicken Sie auf **Weiter**.  
  
    ![Nehme den Lizenzvertrag](./media/install-the-scom-management-packs/SCOM_licnse_agrmt.png "SCOM_licnse_agrmt")  
  
3.  Wählen Sie eigene Installationsordner aus, oder verwenden Sie die Standard-Management Pack-Installationsordner.  
  
    ![Installationsordner auswählen](./media/install-the-scom-management-packs/SCOM_licnse_agrmt2.png "SCOM_licnse_agrmt2")  
  
4.  Klicken Sie auf **Installieren**.  
  
    ![Installation bestätigen](./media/install-the-scom-management-packs/SCOM_licnse_agrmt3.png "SCOM_licnse_agrmt3")  
  
5.  Klicken Sie auf **Schließen**.  
  
    ![Klicken Sie auf Schließen](./media/install-the-scom-management-packs/SCOM_licnse_agrmt4.png "SCOM_licnse_agrmt4")  
  
### <a name="install-the-monitoring-pack-for-sql-server-pdw-appliance"></a>Installieren Sie das Überwachungspaket für SQL Server PDW-Anwendung  
  
1.  Um die Installation ausführen zu können, doppelklicken Sie auf die heruntergeladene SQL Server PDW Appliance Management Pack.  
  
2.  Akzeptieren Sie den Lizenzvertrag, und klicken Sie auf **Weiter**.  
  
    ![Akzeptieren der Lizenzbedingungen](./media/install-the-scom-management-packs/SCOM_licnse_agmtB.png "SCOM_licnse_agmtB")  
  
3.  Wählen Sie das Verzeichnis, das die extrahierten Dateien gespeichert werden. Der Standardinstallationsordner für Management Pack wird standardmäßig angezeigt. Wählen Sie die Standardeinstellung, oder wählen Sie eigene Installationsordner aus.  
  
    ![Auswählen des Installationsordners](./media/install-the-scom-management-packs/SCOM_licnse_agmtB1.png "SCOM_licnse_agmtB1")  
  
4.  Klicken Sie auf **Installieren**.  
  
    ![Installation bestätigen](./media/install-the-scom-management-packs/SCOM_licnse_agmtB2.png "SCOM_licnse_agmtB2")  
  
5.  Klicken Sie auf **Schließen**.  
  
    ![– Installation komplett](./media/install-the-scom-management-packs/SCOM_licnse_agmtB3.png "SCOM_licnse_agmtB3")  
  
## <a name="next-step"></a>Nächster Schritt  
Nun, dass Sie die Management Packs installiert haben, mit dem nächsten Schritt fortfahren: [importieren Sie das SCOM-Management Pack für PDW &#40; Analyseplattformsystem &#41; ](import-the-scom-management-pack-for-pdw.md).  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  

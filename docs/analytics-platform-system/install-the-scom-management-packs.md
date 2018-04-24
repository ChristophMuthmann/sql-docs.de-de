---
title: Installation des Management Packs SCOM - Analytics Platform System | Microsoft Docs
description: Führen Sie diese Schritte zum Herunterladen und installieren die System Center Operations Manager (SCOM) Management Packs für SQL Server PDW. Die Management Packs sind erforderlich, zum Überwachen von SQL Server PDW aus SCOM.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 163ab893074e171decb573d876c5f98334437985
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="install-sql-server-operations-manager-scom-management-packs-for-analytics-platform-system"></a>Installieren von SQL Server Operations Manager (SCOM) Management Packs für Analytics Platform System
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
Nun, dass Sie die Management Packs installiert haben, mit dem nächsten Schritt fortfahren: [importieren Sie das SCOM-Management Pack für PDW &#40;Analyseplattformsystem&#41;](import-the-scom-management-pack-for-pdw.md).  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  

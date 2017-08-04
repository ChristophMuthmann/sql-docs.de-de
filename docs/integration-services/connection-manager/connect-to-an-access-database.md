---
title: Herstellen einer Verbindung mit einer Access-Datenbank | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Access [Integration Services]
- Access databases [Integration Services]
ms.assetid: 229fbd46-ef6a-4609-a4cc-d80d52c33cf1
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e6fe201622d38c10967c9c076da0d99d215ea33f
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-an-access-database"></a>Herstellen einer Verbindung zu einer Access-Datenbank
  Um ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket mit einer Microsoft Office Access-Datenquelle zu verbinden, sind ein OLE DB-Verbindungs-Manager und ein Datenanbieter erforderlich. Welchen Datenanbieter Sie verwenden, hängt von der Access-Version ab, mit der die Datenquelle erstellt wurde:  
  
-   Für Access 2003 und früher erfordert das Paket den [!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet OLE DB-Anbieter.  
  
-   Für Access 2007 erfordert das Paket den OLE DB-Anbieter für Microsoft Office 12.0 Access Database Engine.  
  
 Sie können einen OLE DB-Verbindungs-Manager erstellen und den entsprechenden Datenanbieter entweder im Bereich Verbindungs-Manager im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Import/Export-Assistenten auswählen.  
  
> [!NOTE]  
>  Auf einem 64-Bit-Computer müssen Sie Pakete, die mit den [!INCLUDE[msCoName](../../includes/msconame-md.md)] Access-Datenquellen verbunden sind, im 32-Bit-Modus ausführen. Sowohl der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet OLE DB-Anbieter als auch der OLE DB-Anbieter für das Microsoft Office 12.0 Access-Datenbankmodul sind nur in 32-Bit-Versionen verfügbar.  
  
## <a name="connecting-to-a-data-source-in-access-2003-or-earlier-format"></a>Herstellen einer Verbindung mit einer Datenquelle in Access 2003 oder früher  
  
#### <a name="to-create-an-access-connection-manager-from-the-connection-managers-area"></a>So erstellen Sie einen Access-Verbindungs-Manager im Verbindungs-Manager-Bereich  
  
1.  Öffnen Sie das Paket in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Klicken Sie mit der rechten Maustaste auf eine beliebige Stelle im **Verbindungs-Manager** -Bereich, und wählen Sie anschließend **Neue OLE DB-Verbindung**aus.  
  
3.  Klicken Sie im Dialogfeld **OLE DB-Verbindungs-Manager konfigurieren** auf **Neu**.  
  
     Weitere Informationen finden Sie unter [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
4.  Wählen Sie im Dialogfeld **Verbindungs-Manager** unter **Anbieter**die Option **Microsoft Jet 4.0 OLE DB-Anbieter**aus, und konfigurieren Sie den Verbindungs-Manager nach Bedarf.  
  
#### <a name="to-create-an-access-connection-from-the-sql-server-import-and-export-wizard"></a>So erstellen Sie eine Access-Verbindung mit dem SQL Server Import/Export-Assistenten  
  
1.  Rufen Sie den [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]Import/Export-Assistenten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf.  
  
2.  Wählen Sie auf der Seite **Datenquelle auswählen** für **Datenquelle**die Option **Microsoft Access**aus, und konfigurieren Sie anschließend die Access-Verbindung.  
  
     Bei Auswahl von **Microsoft Access** als **Datenquelle**erstellt der Assistent automatisch den notwendigen OLE DB-Verbindungs-Manager mit dem richtigen Datenanbieter. Weitere Informationen finden Sie unter [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
## <a name="connecting-to-a-data-source-in-access-2007-format"></a>Herstellen einer Verbindung mit einer Datenquelle in Access 2007  
 Für den Zugriff auf eine Access 2007-Datenquelle erfordert der OLE DB-Verbindungs-Manager den OLE DB-Anbieter für Microsoft Office 12.0 Access Database Engine. Dieser Anbieter wird automatisch mit dem 2007 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office System installiert. Wenn 2007 Office System nicht auf dem Computer installiert ist, auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ausgeführt wird, müssen Sie den Anbieter separat installieren. Zum Installieren des OLE DB-Anbieters für Microsoft Office 12.0 Access Database Engine laden Sie die Komponenten von folgender Webseite herunter, und installieren Sie sie: [2007 Office System Driver: Data Connectivity Components](http://go.microsoft.com/fwlink/?LinkId=98155)(möglicherweise nur in englischer Sprache).  
  
#### <a name="to-create-an-ole-db-connection-manager-from-the-connection-managers-area"></a>So erstellen Sie einen OLE DB-Verbindungs-Manager im Verbindungs-Manager-Bereich  
  
1.  Öffnen Sie das Paket in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Klicken Sie mit der rechten Maustaste auf eine beliebige Stelle im **Verbindungs-Manager** -Bereich, und wählen Sie anschließend **Neue OLE DB-Verbindung**aus.  
  
3.  Klicken Sie im Dialogfeld **OLE DB-Verbindungs-Manager konfigurieren** auf **Neu**.  
  
     Weitere Informationen finden Sie unter [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
4.  Wählen Sie im Dialogfeld **Verbindungs-Manager** unter **Anbieter**die Option **Microsoft Office 12.0 Access Database Engine OLE DB**aus, und konfigurieren Sie den Verbindungs-Manager nach Bedarf.  
  
    > [!NOTE]  
    >  Zum Herstellen von Verbindungen mit Datenquellen, für die Access 2007 verwendet wird, können Sie **Microsoft Jet 4.0 OLE DB Provider** nicht als **Datenquelle**auswählen.  
  
#### <a name="to-create-an-ole-db-connection-from-the-sql-server-import-and-export-wizard"></a>So erstellen Sie eine OLE DB-Verbindung mit dem SQL Server Import/Export-Assistenten  
  
1.  Rufen Sie den [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]Import/Export-Assistenten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf.  
  
2.  Wählen Sie auf der Seite **Datenquelle auswählen** als **Datenquelle**die Option **Microsoft Office 12.0 Access Database Engine OLE DB Provider**aus, und konfigurieren Sie die Verbindung nach Bedarf.  
  
    > [!NOTE]  
    >  Zum Herstellen von Verbindungen mit Datenquellen, für die Access 2007 verwendet wird, können Sie **Microsoft Jet 4.0 OLE DB Provider** nicht als **Datenquelle**auswählen.  
  
     Bei Auswahl von **Microsoft Office 12.0 Access Database Engine OLE DB Provider** als **Datenquelle**erstellt der Assistent automatisch den notwendigen OLE DB-Verbindungs-Manager mit dem richtigen Datenanbieter. Weitere Informationen finden Sie unter [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Herstellen einer Verbindung mit einer Excel-Arbeitsmappe](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)  
  
  

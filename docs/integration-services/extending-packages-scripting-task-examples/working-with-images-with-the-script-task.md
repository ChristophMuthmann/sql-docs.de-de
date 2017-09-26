---
title: Arbeiten mit Bildern mithilfe des Skripttasks | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- graphics [Integration Services]
- Script task [Integration Services], images
- Drawing namespace
- images [Integration Services]
- SSIS Script task, images
- Script task [Integration Services], examples
- thumbnails [Integration Services]
- System.Drawing namespace
- JPEG format [Integration Services]
- .jpeg files
ms.assetid: 74aeb7ab-51b2-4b9f-84ee-0b46a7908ab9
caps.latest.revision: 42
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4a28fe7c6024d8cf5669199e5f33e3532013e4d3
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="working-with-images-with-the-script-task"></a>Arbeiten mit Bildern mithilfe des Skripttasks
  Datenbanken von Produkten oder Benutzern enthalten häufig neben Text und numerischen Daten auch Bilder. Die **"System.Drawing"** in Microsoft .NET Framework-Namespace stellt Klassen bereit, zum Bearbeiten von Bildern.  
  
 [Beispiel 1: Konvertieren von Bildern in das JPEG-Format](#example1)  
  
 [Beispiel 2: Erstellen und Speichern von Miniaturbildern](#example2)  
  
> [!NOTE]  
>  Wenn Sie einen Task erstellen möchten, den Sie einfacher in mehreren Paketen wiederverwenden können, empfiehlt es sich, den Code in diesem Skripttaskbeispiel als Ausgangspunkt für einen benutzerdefinierten Task zu verwenden. Weitere Informationen finden Sie unter [Entwickeln eines benutzerdefinierten Tasks](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
##  <a name="example1"></a>Beschreibung zu Beispiel 1: Konvertieren von Bildern in das JPEG-Format  
 Im folgenden Beispiel wird eine Bilddatei, die durch eine Variable definiert ist, geöffnet und mithilfe eines Encoders als komprimierte JPEG-Datei gespeichert. Der Code zum Abrufen der Encoderinformationen wird in einer privaten Funktion gekapselt.  
  
#### <a name="to-configure-this-script-task-example-for-use-with-a-single-image-file"></a>So konfigurieren Sie dieses Skripttaskbeispiel zur Verwendung mit einer einzelnen Bilddatei  
  
1.  Erstellen Sie eine Zeichenfolgenvariable namens `CurrentImageFile`, und legen Sie ihren Wert auf den Pfad und Dateinamen einer bestehenden Bilddatei fest.  
  
2.  Auf der **Skript** auf der Seite der **Skripttask-Editor**, Hinzufügen der `CurrentImageFile` -Variablen an die **ReadOnlyVariables** Eigenschaft.  
  
3.  Legen Sie im skriptprojekt einen Verweis auf die **"System.Drawing"** Namespace.  
  
4.  Verwenden Sie in Ihrem Code **Importe** Anweisungen zum Importieren der **"System.Drawing"** und **System.IO** Namespaces.  
  
#### <a name="to-configure-this-script-task-example-for-use-with-multiple-image-files"></a>So konfigurieren Sie dieses Skripttaskbeispiel zur Verwendung mit mehreren Bilddateien  
  
1.  Platzieren Sie den Skripttask in einen Foreach-Schleifencontainer.  
  
2.  Auf der **Auflistung** auf der Seite der **foreach-Schleifen-Editor**, wählen die **foreach-Dateienumerator** als Enumerator aus, und geben Sie den Pfad und die Dateimaske der Quelle Dateien, z. B. als "*.bmp."  
  
3.  Auf der **Variablenzuordnungen** Seite, ordnen Sie die `CurrentImageFile` -Variable an Index 0. Die Variable übergibt bei jeder Iteration des Enumerators den aktuellen Dateinamen an den Skripttask.  
  
    > [!NOTE]  
    >  Diese Schritte sind zusätzlich zu denen, die in der Vorgehensweise für eine einzelne Bilddatei beschrieben wurden, erforderlich.  
  
### <a name="example-1-code"></a>Beispiel 1-Code  
  
```vb  
Public Sub Main()  
  
    'Create and initialize variables.  
    Dim currentFile As String  
    Dim newFile As String  
    Dim bmp As Bitmap  
    Dim eps As New Imaging.EncoderParameters(1)  
    Dim ici As Imaging.ImageCodecInfo  
    Dim supportedExtensions() As String = _  
        {".BMP", ".GIF", ".JPG", ".JPEG", ".EXIF", ".PNG", _  
        ".TIFF", ".TIF", ".ICO", ".ICON"}  
  
    Try  
        'Store the variable in a string for local manipulation.  
        currentFile = Dts.Variables("CurrentImageFile").Value.ToString  
        'Check the extension of the file against a list of  
        'files that the Bitmap class supports.  
        If Array.IndexOf(supportedExtensions, _  
            Path.GetExtension(currentFile).ToUpper) > -1 Then  
  
            'Load the file.  
            bmp = New Bitmap(currentFile)  
  
            'Calculate the new name for the compressed image.  
            'Note: This will overwrite existing JPEGs.  
            newFile = Path.Combine( _  
                Path.GetDirectoryName(currentFile), _  
                String.Concat(Path.GetFileNameWithoutExtension(currentFile), _  
                ".jpg"))  
  
            'Specify the compression ratio (0=worst quality, 100=best quality).  
            eps.Param(0) = New Imaging.EncoderParameter( _  
                Imaging.Encoder.Quality, 75)  
  
            'Retrieve the ImageCodecInfo associated with the jpeg format.  
            ici = GetEncoderInfo("image/jpeg")  
  
            'Save the file, compressing it into the jpeg encoding.  
            bmp.Save(newFile, ici, eps)  
        Else  
            'The file is not supported by the Bitmap class.  
            Dts.Events.FireWarning(0, "Image Resampling Sample", _  
                "File " & currentFile & " is not a supported format.", _  
                "", 0)  
         End If  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        'An error occurred.  
        Dts.Events.FireError(0, "Image Resampling Sample", _  
            ex.Message & ControlChars.CrLf & ex.StackTrace, _  
            String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
End Sub  
  
Private Function GetEncoderInfo(ByVal mimeType As String) As Imaging.ImageCodecInfo  
  
    'The available image codecs are returned as an array,  
    'which requires code to iterate until the specified codec is found.  
  
    Dim count As Integer  
    Dim encoders() As Imaging.ImageCodecInfo  
  
    encoders = Imaging.ImageCodecInfo.GetImageEncoders()  
  
    For count = 0 To encoders.Length  
        If encoders(count).MimeType = mimeType Then  
            Return encoders(count)  
        End If  
    Next  
  
    'This point is only reached if a codec is not found.  
    Err.Raise(513, "Image Resampling Sample", String.Format( _  
        "The {0} codec is not available. Unable to compress file.", _  
            mimeType))  
    Return Nothing  
  
End Function  
  
```  
  
##  <a name="example2"></a>Beschreibung zu Beispiel 2: Erstellen und Speichern von Miniaturbildern  
 Im folgenden Beispiel wird eine Bilddatei, die durch eine Variable definiert ist, geöffnet, ein Miniaturbild dieses Bilds mit gleichem Seitenverhältnis erstellt und das Miniaturbild mit geändertem Dateinamen gespeichert. Der Code, der Höhe und Breite des Miniaturbilds berechnet und dabei das Seitenverhältnis beibehält, wird in einer privaten Unterroutine gekapselt.  
  
#### <a name="to-configure-this-script-task-example-for-use-with-a-single-image-file"></a>So konfigurieren Sie dieses Skripttaskbeispiel zur Verwendung mit einer einzelnen Bilddatei  
  
1.  Erstellen Sie eine Zeichenfolgenvariable namens `CurrentImageFile`, und legen Sie ihren Wert auf den Pfad und Dateinamen einer bestehenden Bilddatei fest.  
  
2.  Erstellen Sie zudem die ganzzahlige Variable `MaxThumbSize`, und weisen Sie ihr einen Pixelwert, z. B. 100, zu.  
  
3.  Auf der **Skript** auf der Seite der **Skripttask-Editor**, beide Variablen hinzufügen, die **ReadOnlyVariables** Eigenschaft.  
  
4.  Legen Sie im skriptprojekt einen Verweis auf die **"System.Drawing"** Namespace.  
  
5.  Verwenden Sie in Ihrem Code **Importe** Anweisungen zum Importieren der **"System.Drawing"** und **System.IO** Namespaces.  
  
#### <a name="to-configure-this-script-task-example-for-use-with-multiple-image-files"></a>So konfigurieren Sie dieses Skripttaskbeispiel zur Verwendung mit mehreren Bilddateien  
  
1.  Platzieren Sie den Skripttask in einen Foreach-Schleifencontainer.  
  
2.  Auf der **Auflistung** auf der Seite der **foreach-Schleifen-Editor**, wählen die **foreach-Dateienumerator** als die **Enumerator**, und geben Sie die Pfad und die Dateimaske der Quelldateien an, z. B. ".jpg".  
  
3.  Auf der **Variablenzuordnungen** Seite, ordnen Sie die `CurrentImageFile` -Variable an Index 0. Die Variable übergibt bei jeder Iteration des Enumerators den aktuellen Dateinamen an den Skripttask.  
  
    > [!NOTE]  
    >  Diese Schritte sind zusätzlich zu denen, die in der Vorgehensweise für eine einzelne Bilddatei beschrieben wurden, erforderlich.  
  
### <a name="example-2-code"></a>Beispiel 2-Code  
  
```vb  
Public Sub Main()  
  
    Dim currentImageFile As String  
    Dim currentImage As Image  
    Dim maxThumbSize As Integer  
    Dim thumbnailImage As Image  
    Dim thumbnailFile As String  
    Dim thumbnailHeight As Integer  
    Dim thumbnailWidth As Integer  
  
    currentImageFile = Dts.Variables("CurrentImageFile").Value.ToString  
    thumbnailFile = Path.Combine( _  
        Path.GetDirectoryName(currentImageFile), _  
        String.Concat(Path.GetFileNameWithoutExtension(currentImageFile), _  
        "_thumbnail.jpg"))  
  
    Try  
        currentImage = Image.FromFile(currentImageFile)  
  
        maxThumbSize = CType(Dts.Variables("MaxThumbSize").Value, Integer)  
        CalculateThumbnailSize( _  
            maxThumbSize, currentImage, thumbnailWidth, thumbnailHeight)  
  
        thumbnailImage = currentImage.GetThumbnailImage( _  
           thumbnailWidth, thumbnailHeight, Nothing, Nothing)  
        thumbnailImage.Save(thumbnailFile)  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        Dts.Events.FireError(0, "Script Task Example", _  
        ex.Message & ControlChars.CrLf & ex.StackTrace, _  
        String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
End Sub  
  
Private Sub CalculateThumbnailSize( _  
    ByVal maxSize As Integer, ByVal sourceImage As Image, _  
    ByRef thumbWidth As Integer, ByRef thumbHeight As Integer)  
  
    If sourceImage.Width > sourceImage.Height Then  
        thumbWidth = maxSize  
        thumbHeight = CInt((maxSize / sourceImage.Width) * sourceImage.Height)  
    Else  
        thumbHeight = maxSize  
        thumbWidth = CInt((maxSize / sourceImage.Height) * sourceImage.Width)  
    End If  
  
End Sub  
```  
  
```csharp  
bool ThumbnailCallback()  
        {  
            return false;  
        }  
        public void Main()  
        {  
  
            string currentImageFile;  
            Image currentImage;  
            int maxThumbSize;  
            Image thumbnailImage;  
            string thumbnailFile;  
            int thumbnailHeight = 0;  
            int thumbnailWidth = 0;  
  
            currentImageFile = Dts.Variables["CurrentImageFile"].Value.ToString();  
            thumbnailFile = Path.Combine(Path.GetDirectoryName(currentImageFile), String.Concat(Path.GetFileNameWithoutExtension(currentImageFile), "_thumbnail.jpg"));  
  
            try  
            {  
  
                currentImage = Image.FromFile(currentImageFile);  
  
                maxThumbSize = (int)Dts.Variables["MaxThumbSize"].Value;  
                CalculateThumbnailSize(maxThumbSize, currentImage, ref thumbnailWidth, ref thumbnailHeight);  
  
                Image.GetThumbnailImageAbort myCallback = new Image.GetThumbnailImageAbort(ThumbnailCallback);  
  
                thumbnailImage = currentImage.GetThumbnailImage(thumbnailWidth, thumbnailHeight, ThumbnailCallback, IntPtr.Zero);  
                thumbnailImage.Save(thumbnailFile);  
                Dts.TaskResult = (int)ScriptResults.Success;  
            }  
            catch (Exception ex)  
            {  
                Dts.Events.FireError(0, "Script Task Example", ex.Message + "\r" + ex.StackTrace, String.Empty, 0);  
                Dts.TaskResult = (int)ScriptResults.Failure;  
            }  
  
        }  
  
        private void CalculateThumbnailSize(int maxSize, Image sourceImage, ref int thumbWidth, ref int thumbHeight)  
        {  
  
            if (sourceImage.Width > sourceImage.Height)  
            {  
                thumbWidth = maxSize;  
                thumbHeight = (int)(sourceImage.Height * maxSize / sourceImage.Width);  
            }  
            else  
            {  
                thumbHeight = maxSize;  
                thumbWidth = (int)(sourceImage.Width * maxSize / sourceImage.Height);  
  
            }  
  
        }  
  
```  
  
  

---
title: "Verbleibende asynchrone Aufgaben abbrechen nach einer vollständigen (Visual Basic) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: c928b5a1-622f-4441-8baf-adca1dde197f
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 1b70822edd972ac33614ab49faad6ff50b0e80b7
ms.lasthandoff: 03/13/2017

---
# <a name="cancel-remaining-async-tasks-after-one-is-complete-visual-basic"></a>Abbrechen Sie verbleibende asynchrone Aufgaben nach einer vollständigen (Visual Basic)
Mithilfe der <xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=fullName>-Methode zusammen mit einem <xref:System.Threading.CancellationToken>, können Sie alle verbleibenden Aufgaben abbrechen, wenn eine Aufgabe abgeschlossen ist.</xref:System.Threading.CancellationToken> </xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=fullName> Die `WhenAny`-Methode akzeptiert ein Argument, das eine Auflistung von Aufgaben ist. Die Methode startet alle Aufgaben und gibt eine einzelne Aufgabe zurück. Die einzelne Aufgabe ist abgeschlossen, wenn eine beliebige Aufgabe in der Auflistung abgeschlossen ist.  
  
 In diesem Beispiel wird veranschaulicht, wie ein Abbruchtoken in Verbindung mit `WhenAny` verwendet wird, um an der ersten Aufgabe festzuhalten, die in der Auflistung von Aufgaben beendet wird, und die übrigen Aufgaben abzubrechen. Jede Aufgabe lädt den Inhalt einer Website herunter. Im Beispiel wird die Länge des Inhalts des ersten abgeschlossenen Downloads angezeigt und die anderen Downloads abgebrochen.  
  
> [!NOTE]
>  Zum Ausführen der Beispiele müssen Sie Visual Studio 2012 oder höher und .NET Framework 4.5 oder höher auf Ihrem Computer installiert.  
  
## <a name="downloading-the-example"></a>Herunterladen des Beispiels  
 Sie können das vollständige Windows Presentation Foundation (WPF)-Projekt aus [Async Sample: Fine Tuning Your Application](http://go.microsoft.com/fwlink/?LinkId=255046) und führen Sie dann die folgenden Schritte aus.  
  
1.  Dekomprimieren Sie die heruntergeladene Datei, und starten Sie dann Visual Studio.  
  
2.  Klicken Sie in der Menüleiste auf **Datei**, dann auf **Öffnen**und **Projekt/Projektmappe**.  
  
3.  In der **Projekt öffnen** im Dialogfeld Öffnen den Ordner, der Ihnen dekomprimierten Beispielcode enthält, und öffnen Sie anschließend die Projektmappendatei (sln) für AsyncFineTuningVB.  
  
4.  In **Projektmappen-Explorer**, öffnen Sie das Kontextmenü für die **CancelAfterOneTask** Projekt, und wählen Sie dann **Set as StartUp Project**.  
  
5.  Drücken Sie die Taste F5, um das Projekt auszuführen.  
  
     Drücken Sie STRG+F5, um das Projekt auszuführen, ohne es zu debuggen.  
  
6.  Führen Sie das Programm mehrmals aus, um zu überprüfen, dass unterschiedliche Downloads als erste beendet werden.  
  
 Wenn Sie das Projekt herunterladen möchten, können Sie die Datei "MainWindow.Xaml.vb" am Ende dieses Themas überprüfen.  
  
## <a name="building-the-example"></a>Erstellen des Beispiels  
 Im Beispiel in diesem Thema wird das Projekt, das in entwickelt wird hinzugefügt [eine asynchrone Aufgabe oder eine Liste von Tasks Abbrechen](http://msdn.microsoft.com/library/d6e4e801-df64-4705-98fc-df725a577fb0) , eine Liste von Aufgaben abzubrechen. Im Beispiel wird die gleiche UI verwendet, obwohl die **Abbrechen** Schaltfläche nicht explizit verwendet wird.  
  
 So erstellen Sie das Beispiel selbst, Schritt für Schritt führen Sie die Schritte im Abschnitt "Herunterladen des Beispiels", aber wählen Sie **CancelAListOfTasks** als die **Startprojekt**. Fügen Sie diesem Projekt die Änderungen in diesem Thema hinzu.  
  
 In der Datei "MainWindow.Xaml.vb", der die **CancelAListOfTasks** Projekt, starten Sie den Übergang durch Verschieben die Verarbeitungsschritte für jede Website, von der Schleife in `AccessTheWebAsync` zur folgenden asynchronen Methode.  
  
```vb  
' ***Bundle the processing steps for a website into one async method.  
Async Function ProcessURLAsync(url As String, client As HttpClient, ct As CancellationToken) As Task(Of Integer)  
  
    ' GetAsync returns a Task(Of HttpResponseMessage).   
    Dim response As HttpResponseMessage = Await client.GetAsync(url, ct)  
  
    ' Retrieve the website contents from the HttpResponseMessage.  
    Dim urlContents As Byte() = Await response.Content.ReadAsByteArrayAsync()  
  
    Return urlContents.Length  
End Function  
```  
  
 In `AccessTheWebAsync`, in diesem Beispiel wird eine Abfrage verwendet die <xref:System.Linq.Enumerable.ToArray%2A>-Methode, und die `WhenAny` Methode zum Erstellen und starten ein Array von Aufgaben.</xref:System.Linq.Enumerable.ToArray%2A> Die Anwendung von `WhenAny` auf den Array gibt eine einzelne Aufgabe zurück, die, wenn sie erwartet wird, zur ersten Aufgabe auswertet wird, die im Array von Aufgaben zum Abschluss kommt.  
  
 Nehmen Sie in `AccessTheWebAsync` die folgenden Änderungen vor. Die Änderungen in der Codedatei sind mit Sternchen gekennzeichnet.  
  
1.  Kommentieren Sie die Schleife aus oder löschen Sie sie.  
  
2.  Erstellen Sie eine Abfrage, die eine Auflistung generischer Aufgaben erstellt, wenn sie ausgeführt wird. Jeder Aufruf von `ProcessURLAsync` gibt eine <xref:System.Threading.Tasks.Task%601>, in denen `TResult` ist eine ganze Zahl.</xref:System.Threading.Tasks.Task%601>  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
3.  Rufen Sie `ToArray` auf, um die Abfrage auszuführen und die Aufgaben zu starten. Die Anwendung der `WhenAny`-Methode im nächsten Schritt würde die Abfrage ohne `ToArray` ausführen und die Aufgaben starten, bei anderen Methoden ist dies möglicherweise nicht der Fall. Die sicherste Methode besteht darin, die Ausführung der Abfrage explizit zu erzwingen.  
  
<CodeContentPlaceHolder>2</CodeContentPlaceHolder>  
4.  Rufen Sie `WhenAny` mit der Auflistung von Aufgaben auf. `WhenAny` gibt `Task(Of Task(Of Integer))` oder `Task<Task<int>>` zurück.  Das bedeutet, dass `WhenAny` eine Aufgabe zurückgibt, die zu einem einzelnen `Task(Of Integer)` oder `Task<int>` ausgewertet wird, wenn sie erwartet wird. Diese einzelne Aufgabe ist die erste Aufgabe in der Auflistung, die beendet wird. Die Aufgabe, die als erste beendet wird, wird `firstFinishedTask` zugewiesen. Der Typ des `firstFinishedTask` ist <xref:System.Threading.Tasks.Task%601>, `TResult` eine ganze Zahl ist, da dies der Rückgabetyp der `ProcessURLAsync`.</xref:System.Threading.Tasks.Task%601>  
  
```vb  
' ***Call WhenAny and then await the result. The task that finishes   
' first is assigned to firstFinishedTask.  
Dim firstFinishedTask As Task(Of Integer) = Await Task.WhenAny(downloadTasks)  
```  
  
5.  In diesem Beispiel sind Sie nur an der Aufgabe interessiert, die zuerst beendet wird. Verwenden Sie daher <xref:System.Threading.CancellationTokenSource.Cancel%2A?displayProperty=fullName>die verbleibenden Aufgaben abzubrechen.</xref:System.Threading.CancellationTokenSource.Cancel%2A?displayProperty=fullName>  
  
```vb  
' ***Cancel the rest of the downloads. You just want the first one.  
cts.Cancel()  
```  
  
6.  Schließlich warten Sie ab, dass `firstFinishedTask` die Länge des heruntergeladenen Inhalts abruft.  
  
```vb  
Dim length = Await firstFinishedTask  
resultsTextBox.Text &= String.Format(vbCrLf & "Length of the downloaded website:  {0}" & vbCrLf, length)  
```  
  
 Führen Sie das Programm mehrmals aus, um zu überprüfen, dass unterschiedliche Downloads als erste beendet werden.  
  
## <a name="complete-example"></a>Vollständiges Beispiel  
 Der folgende Code besteht aus der vollständigen Datei "MainWindow.xaml.cs" oder "MainWindow.xaml.vb" für das Beispiel. Sternchen markieren die Elemente, die für dieses Beispiel hinzugefügt wurden.  
  
 Beachten Sie, dass Sie eine Referenz für <xref:System.Net.Http>.</xref:System.Net.Http> hinzufügen müssen  
  
 Sie können das Projekt aus [Async Sample: Fine Tuning Your Application](http://go.microsoft.com/fwlink/?LinkId=255046).  
  
```vb  
' Add an Imports directive and a reference for System.Net.Http.  
Imports System.Net.Http  
  
' Add the following Imports directive for System.Threading.  
Imports System.Threading  
  
Class MainWindow  
  
    ' Declare a System.Threading.CancellationTokenSource.  
    Dim cts As CancellationTokenSource  
  
    Private Async Sub startButton_Click(sender As Object, e As RoutedEventArgs)  
  
        ' Instantiate the CancellationTokenSource.  
        cts = New CancellationTokenSource()  
  
        resultsTextBox.Clear()  
  
        Try  
            Await AccessTheWebAsync(cts.Token)  
            resultsTextBox.Text &= vbCrLf & "Download complete."  
  
        Catch ex As OperationCanceledException  
            resultsTextBox.Text &= vbCrLf & "Download canceled." & vbCrLf  
  
        Catch ex As Exception  
            resultsTextBox.Text &= vbCrLf & "Download failed." & vbCrLf  
        End Try  
  
        ' Set the CancellationTokenSource to Nothing when the download is complete.  
        cts = Nothing  
    End Sub  
  
    ' You can still include a Cancel button if you want to.  
    Private Sub cancelButton_Click(sender As Object, e As RoutedEventArgs)  
  
        If cts IsNot Nothing Then  
            cts.Cancel()  
        End If  
    End Sub  
  
    ' Provide a parameter for the CancellationToken.  
    ' Change the return type to Task because the method has no return statement.  
    Async Function AccessTheWebAsync(ct As CancellationToken) As Task  
  
        Dim client As HttpClient = New HttpClient()  
  
        ' Call SetUpURLList to make a list of web addresses.  
        Dim urlList As List(Of String) = SetUpURLList()  
  
        '' Comment out or delete the loop.  
        ''For Each url In urlList  
        ''    ' GetAsync returns a Task(Of HttpResponseMessage).   
        ''    ' Argument ct carries the message if the Cancel button is chosen.   
        ''    ' Note that the Cancel button can cancel all remaining downloads.  
        ''    Dim response As HttpResponseMessage = Await client.GetAsync(url, ct)  
  
        ''    ' Retrieve the website contents from the HttpResponseMessage.  
        ''    Dim urlContents As Byte() = Await response.Content.ReadAsByteArrayAsync()  
  
        ''    resultsTextBox.Text &=  
        ''        String.Format(vbCrLf & "Length of the downloaded string: {0}." & vbCrLf, urlContents.Length)  
        ''Next  
  
        ' ***Create a query that, when executed, returns a collection of tasks.  
        Dim downloadTasksQuery As IEnumerable(Of Task(Of Integer)) =  
            From url In urlList Select ProcessURLAsync(url, client, ct)  
  
        ' ***Use ToArray to execute the query and start the download tasks.   
        Dim downloadTasks As Task(Of Integer)() = downloadTasksQuery.ToArray()  
  
        ' ***Call WhenAny and then await the result. The task that finishes   
        ' first is assigned to firstFinishedTask.  
        Dim firstFinishedTask As Task(Of Integer) = Await Task.WhenAny(downloadTasks)  
  
        ' ***Cancel the rest of the downloads. You just want the first one.  
        cts.Cancel()  
  
        ' ***Await the first completed task and display the results  
        ' Run the program several times to demonstrate that different  
        ' websites can finish first.  
        Dim length = Await firstFinishedTask  
        resultsTextBox.Text &= String.Format(vbCrLf & "Length of the downloaded website:  {0}" & vbCrLf, length)  
    End Function  
  
    ' ***Bundle the processing steps for a website into one async method.  
    Async Function ProcessURLAsync(url As String, client As HttpClient, ct As CancellationToken) As Task(Of Integer)  
  
        ' GetAsync returns a Task(Of HttpResponseMessage).   
        Dim response As HttpResponseMessage = Await client.GetAsync(url, ct)  
  
        ' Retrieve the website contents from the HttpResponseMessage.  
        Dim urlContents As Byte() = Await response.Content.ReadAsByteArrayAsync()  
  
        Return urlContents.Length  
    End Function  
  
    ' Add a method that creates a list of web addresses.  
    Private Function SetUpURLList() As List(Of String)  
  
        Dim urls = New List(Of String) From  
            {  
                "http://msdn.microsoft.com",  
                "http://msdn.microsoft.com/library/hh290138.aspx",  
                "http://msdn.microsoft.com/library/hh290140.aspx",  
                "http://msdn.microsoft.com/library/dd470362.aspx",  
                "http://msdn.microsoft.com/library/aa578028.aspx",  
                "http://msdn.microsoft.com/library/ms404677.aspx",  
                "http://msdn.microsoft.com/library/ff730837.aspx"  
            }  
        Return urls  
    End Function  
  
End Class  
  
' Sample output:  
  
' Length of the downloaded website:  158856  
  
' Download complete.  
```  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Threading.Tasks.Task.WhenAny%2A></xref:System.Threading.Tasks.Task.WhenAny%2A>   
 [Feinabstimmung der Async-Anwendung (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/fine-tuning-your-async-application.md)   
 [Asynchrone Programmierung mit Async und Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/index.md)   
 [ASYNC-Beispiel: Feinabstimmung der Anwendung](http://go.microsoft.com/fwlink/?LinkId=255046)

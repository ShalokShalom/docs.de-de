---
title: "Spaltenf&#252;llmodus im DataGridView-Steuerelement in Windows Forms | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "Datenblätter, Automatische Größenänderung von Spalten"
  - "Datenblätter, Spaltenfüllmodus"
  - "DataGridView-Steuerelement [Windows Forms], Spaltenfüllmodus"
ms.assetid: b4ef7411-ebf4-4e26-bb33-aecec90de80c
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Spaltenf&#252;llmodus im DataGridView-Steuerelement in Windows Forms
Im Spaltenfüllmodus passt das <xref:System.Windows.Forms.DataGridView>\-Steuerelement seine Spalten automatisch so an, dass sie die Breite des verfügbaren Anzeigebereichs ausfüllen.  Das Steuerelement zeigt die horizontale Bildlaufleiste nur an, wenn es erforderlich ist, dass die Breite jeder Spalte gleich oder größer als sein <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A>\-Eigenschaftenwert ist.  
  
 Das Größenanpassungsverhalten jeder Spalte hängt von ihrer <xref:System.Windows.Forms.DataGridViewColumn.InheritedAutoSizeMode%2A>\-Eigenschaft ab.  Der Wert dieser Eigenschaft wird von der <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A>\-Eigenschaft der Spalte oder der <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A>\-Eigenschaft des Steuerelements geerbt, wenn der Spaltenwert <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode> ist \(Standardwert\).  
  
 Jede Spalte kann einen anderen Größenmodus aufweisen. Alle Spalten mit einem Größenmodus von <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode> verwenden jedoch die Breite des Anzeigebereichs gemeinsam, die nicht von anderen Spalten verwendet wird.  Diese Breite wird unter den Spalten im Füllmodus in einem Verhältnis relativ zu ihren <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A>\-Eigenschaftenwerten aufgeteilt.  Wenn zwei Spalten z. B. die <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A>\-Werte 100 und 200 aufweisen, ist die erste Spalte halb so breit wie die zweite Spalte.  
  
## Größenänderung in Füllmodus durch Benutzer  
 Im Gegensatz zu Größenanpassungsmodi, die die Größe basierend die auf dem Zelleninhalt anpassen, verhindert der Füllmodus nicht, dass Benutzer eine Größenänderung von Spalten vornehmen können, die <xref:System.Windows.Forms.DataGridViewColumn.Resizable%2A>\-Eigenschaftenwerte von `true` aufweisen.  Wenn ein Benutzer die Größe einer Spalte im Füllmodus ändert, werden alle Spalten im Füllmodus hinter der geänderten Spalte ebenfalls geändert \(nach rechts, wenn <xref:System.Windows.Forms.Control.RightToLeft%2A> `false` ist, andernfalls auf der linken Seite\), um die Änderung in der verfügbaren Breite zu berücksichtigen.  Wenn hinter der Spalte, deren Größe geändert wurde, keine Spalten im Füllmodus vorhanden sind, wird die Größe aller Spalten im Füllmodus im Steuerelement geändert, um dies auszugleichen.  Wenn im Steuerelement keine weiteren Spalten im Füllmodus vorhanden sind, wird die Größenänderung ignoriert.  Wenn die Größe einer Spalte geändert wird, die sich nicht im Füllmodus befindet, wird die Größe aller Spalten im Füllmodus im Steuerelement geändert, um dies auszugleichen.  
  
 Nachdem die Größe einer Spalte im Füllmodus geändert wurde, werden die <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A>\-Werte für alle Spalten, die geändert wurden, proportional angepasst.  Wenn vier Spalten im Füllmodus z. B. <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A>\-Werte von 100 aufweisen, führt das Ändern der Größe der zweiten Spalte in die Hälfte der ursprünglichen Breite zu <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A>\-Werte von 100, 50, 125 und 125.  Durch das Ändern der Größe einer Spalte, die sich nicht im Füllmodus befindet, werden keine <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A>\-Werte geändert, weil die Größe der Spalten im Füllmodus unter Beibehaltung der Proportionen einfach geändert wird, um dies auszugleichen.  
  
## Inhaltsbasierte FillWeight\-Anpassung  
 Sie können <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A>\-Werte für Spalten im Füllmodus mithilfe der <xref:System.Windows.Forms.DataGridView>\-Methoden für automatische Größenänderung initialisieren, z. B. mit der <xref:System.Windows.Forms.DataGridView.AutoResizeColumns%2A>\-Methode.  Diese Methode berechnet zuerst die Breite, die für Spalten erforderlich ist, um ihren Inhalt anzuzeigen.  Im nächsten Schritt passt das Steuerelement die <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A>\-Werte für alle Spalten im Füllmodus so an, dass ihre Proportionen mit den Proportionen der berechneten Breiten übereinstimmen.  Schließlich ändert das Steuerelement die Größe von Spalten im Füllmodus mithilfe der neuen <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A>\-Proportionen so, dass alle Spalten im Steuerelement den verfügbaren horizontalen Platz ausfüllen.  
  
## Beispiel  
  
### Beschreibung  
 Durch Verwenden der geeigneten Werte für die <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A>\-, <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A>\-, <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A>\- und <xref:System.Windows.Forms.DataGridViewColumn.Resizable%2A>\-Eigenschaften können Sie das Verhalten für die Größenänderung für viele unterschiedliche Szenarien anpassen.  
  
 Mithilfe des folgenden Beispielcodes können Sie mit verschieden Werten für die <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A>\-, <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A>\- und <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A>\-Eigenschaften verschiedener Spalten experimentieren.  In diesem Beispiel wird ein <xref:System.Windows.Forms.DataGridView>\-Steuerelement an seine eigene <xref:System.Windows.Forms.DataGridView.Columns%2A>\-Auflistung gebunden, und eine Spalte wird an jede der <xref:System.Windows.Forms.DataGridViewColumn.HeaderText%2A>\-, <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A>\-, <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A>\-, <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A>\- und <xref:System.Windows.Forms.DataGridViewColumn.Width%2A>\-Eigenschaften gebunden.  Jede der Spalten wird außerdem durch eine Zeile im Steuerelement dargestellt. Wenn Sie Werte in einer Zeile ändern, werden die Eigenschaften der entsprechenden Spalte aktualisiert, damit Sie sehen können, wie die Werte miteinander interagieren.  
  
### Code  
 [!code-csharp[System.Windows.Forms.DataGridViewFillColumnsDemo#00](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewFillColumnsDemo/CS/fillcolumns.cs#00)]
 [!code-vb[System.Windows.Forms.DataGridViewFillColumnsDemo#00](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewFillColumnsDemo/vb/fillcolumns.vb#00)]  
  
### Kommentare  
 So verwenden Sie diese Beispielanwendung:  
  
-   Ändern Sie die Größe des Formulars.  Beachten Sie, wie sich die Breite der Spalten ändert, während die Proportionen, die durch die <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A>\-Eigenschaftenwerte angegeben werden, beibehalten werden.  
  
-   Ändern Sie die Spaltengrößen, indem Sie die Spaltenunterteiler mit der Maus ziehen.  Beobachten Sie, wie sich die <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A>\-Werte ändern.  
  
-   Ändern Sie den <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A>\-Wert für eine Spalte, und ändern Sie dann die Größe des Formulars durch Ziehen.  Wenn die Größe des Formulars klein genug ist, beobachten Sie, dass die <xref:System.Windows.Forms.DataGridViewColumn.Width%2A>\-Werte die <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A>\-Werte nicht unterschreiten.  
  
-   Ändern Sie die <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A>\-Werte für alle Spalten in hohe Werte, damit die kombinierten Werte die Breite des Steuerelements überschreiten.  Beachten Sie, wie die horizontale Bildlaufleiste angezeigt wird.  
  
-   Ändern Sie die <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A> Werte für einige Spalten.  Beobachten Sie die Auswirkungen, wenn Sie die Größe von Spalten oder des Formulars ändern.  
  
## Kompilieren des Codes  
 Für dieses Beispiel benötigen Sie Folgendes:  
  
-   Verweise auf die Assemblys "System", "System.Drawing" und "System.Windows.Forms".  
  
 Informationen zum Erstellen dieses Beispiels über die Befehlszeile für [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] oder [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] finden Sie unter [Erstellen von der Befehlszeile aus](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) oder [Erstellen über die Befehlszeile mit csc.exe](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md).  Sie können dieses Beispiel auch in [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] erstellen, indem Sie den Code in ein neues Projekt einfügen.  Siehe auch [Gewusst wie: Kompilieren und Ausführen eines vollständigen Windows Forms\-Codebeispiels mit Visual Studio](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\)).  
  
## Siehe auch  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.AutoResizeColumns%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewAutoSizeColumnsMode>   
 <xref:System.Windows.Forms.DataGridViewColumn>   
 <xref:System.Windows.Forms.DataGridViewColumn.InheritedAutoSizeMode%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode>   
 <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewColumn.Width%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewColumn.Resizable%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.Control.RightToLeft%2A?displayProperty=fullName>   
 [Größenanpassung bei Spalten und Zeilen im DataGridView\-Steuerelement in Windows Forms](../../../../docs/framework/winforms/controls/resizing-columns-and-rows-in-the-windows-forms-datagridview-control.md)
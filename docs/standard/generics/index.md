---
title: "Generika in .NET&#160;Framework | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Generische Methoden, Typrückschluss"
  - "Generika [.NET Framework], Sammlungen"
  - "Generische Schnittstellen [.NET Framework]"
  - "Erstellte generische Typen"
  - "Geschachtelte generische Typen"
  - "Generische Typdefinitionen"
  - "Generische Klassen [.NET Framework]"
  - "Generika [.NET Framework], Schnittstellen"
  - "Generika [.NET Framework], Info"
  - "Generika [.NET Framework]"
  - "Generische Auflistungen [.NET Framework]"
  - "Generische Delegaten [.NET Framework]"
  - "Generische Typargumente"
  - "Generika [.NET Framework], Delegaten"
  - "Generika [.NET Framework], Funktionen"
  - "Einschränkungen [.NET Framework]"
  - "Generische Typen"
  - "Generische Typparameter"
ms.assetid: 2994d786-c5c7-4666-ab23-4c83129fe39c
caps.latest.revision: 23
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 23
---
# Generika in .NET&#160;Framework
<a name="top"></a> Mit Generika können Sie eine Methode, Klasse, Struktur oder Schnittstelle genau an den Datentyp anpassen, der von ihnen verarbeitet wird. Anstatt beispielsweise die <xref:System.Collections.Hashtable>\-Klasse zu verwenden, bei der Schlüssel und Werte einen beliebigen Typ haben dürfen, können Sie die generische Klasse <xref:System.Collections.Generic.Dictionary%602> verwenden und den für den Schlüssel und Wert zulässigen Typ angeben. Zu den Vorteilen von Generika zählen bessere Wiederverwendbarkeit des Codes und Typsicherheit.  
  
 Dieses Thema bietet eine Übersicht über Generika in .NET Framework und eine Zusammenfassung der generischen Typen oder Methoden. Es enthält die folgenden Abschnitte:  
  
-   [Definieren und Verwenden von Generika](#defining_and_using_generics)  
  
-   [Generika\-Terminologie](#generics_terminology)  
  
-   [Klassenbibliothek und Sprachunterstützung](#class_library_and_language_support)  
  
-   [Geschachtelte Typen und Generika](#nested_types_and_generics)  
  
-   [Verwandte Themen](#related_topics)  
  
-   [Verweis](#reference)  
  
<a name="defining_and_using_generics"></a>   
## Definieren und Verwenden von Generika  
 Generika sind Klassen, Strukturen, Schnittstellen und Methoden, die über Platzhalter \(Typparameter\) für einen oder mehrere der Typen verfügen, die sie speichern oder verwenden. Eine generische Auflistungsklasse kann beispielsweise einen Typparameter als Platzhalter für den Typ von Objekten verwenden, die in ihr gespeichert werden; die Typparameter werden als die Typen ihrer Felder und die Parametertypen ihrer Methoden angezeigt. Eine generische Methode kann ihren Typparameter als den Typen ihres Rückgabewerts oder als den Typen einer ihrer formalen Parameter verwenden. Der folgende Code zeigt eine einfache generische Klassendefinition.  
  
 [!code-cpp[Conceptual.Generics.Overview#2](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.generics.overview/cpp/source.cpp#2)]
 [!code-csharp[Conceptual.Generics.Overview#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.generics.overview/cs/source.cs#2)]
 [!code-vb[Conceptual.Generics.Overview#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.generics.overview/vb/source.vb#2)]  
  
 Beim Erstellen einer Instanz einer generischen Klasse geben Sie die tatsächlich zu ersetzenden Typen für die Typparameter an. Dadurch wird eine neue generische Klasse eingerichtet, die als konstruierte generische Klasse bezeichnet wird, wobei die ausgewählten Typen überall dort, wo die Typparameter angezeigt werden, ersetzt werden. Das Ergebnis ist eine typsichere Klasse, die auf die ausgewählten Typen zugeschnitten ist, wie im folgenden Code veranschaulicht wird.  
  
 [!code-cpp[Conceptual.Generics.Overview#3](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.generics.overview/cpp/source.cpp#3)]
 [!code-csharp[Conceptual.Generics.Overview#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.generics.overview/cs/source.cs#3)]
 [!code-vb[Conceptual.Generics.Overview#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.generics.overview/vb/source.vb#3)]  
  
<a name="generics_terminology"></a>   
### Generika\-Terminologie  
 Die folgenden Begriffe werden bei der Erörterung von Generika in .NET Framework verwendet:  
  
-   Eine *generische Typdefinition* ist eine Klassen\-, Struktur\- oder Schnittstellendeklaration, die als Vorlage fungiert und Platzhalter für die Typen besitzt, die sie enthalten oder verwenden kann. Die <xref:System.Collections.Generic.Dictionary%602?displayProperty=fullName>\-Klasse kann beispielsweise zwei Typen enthalten: Schlüssel und Werte. Da eine generische Typdefinition lediglich eine Vorlage ist, können Sie keine Instanzen einer Klasse, Struktur oder Schnittstelle erstellen, die eine generische Typdefinition ist.  
  
-   *Generische Typparameter*, oder *Typparameter*, sind die Platzhalter in einer generischen Typ\- oder Methodendefinition. Der generische Typ <xref:System.Collections.Generic.Dictionary%602?displayProperty=fullName> verfügt über zwei Typparameter, `TKey` und `TValue`, die die Typen seiner Schlüssel und Werte darstellen.  
  
-   Ein *konstruierter generischer Typ*, oder *konstruierter Typ*, ist das Ergebnis der Angabe von Typen für die generischen Typparameter einer generischen Typdefinition.  
  
-   Ein *generisches Typargument* ist jeder Typ, der durch einen generischen Typparameter ersetzt wird.  
  
-   Der allgemeine Begriff *generischer Typ* schließt sowohl konstruierte Typen als auch generische Typdefinitionen ein.  
  
-   *Kovarianz* und *Kontravarianz* der generischen Typparameter ermöglichen es Ihnen, konstruierte generische Typen zu verwenden, deren Typargumente stärker abgeleitet \(Kovarianz\) oder weniger stark abgeleitet \(Kontravarianz\) sind als ein konstruierter Zieltyp. Kovarianz und Kontravarianz werden zusammen als *Varianz* bezeichnet. Weitere Informationen finden Sie unter [Kovarianz und Kontravarianz](../../../docs/standard/generics/covariance-and-contravariance.md).  
  
-   *Einschränkungen* sind Begrenzungen für generische Typparameter. Sie können beispielsweise einen Typparameter auf Typen beschränken, die die generische Schnittstelle <xref:System.Collections.Generic.IComparer%601?displayProperty=fullName> implementieren, um sicherzustellen, dass Instanzen des Typs sortiert werden können. Sie können Typparameter auch auf Typen mit einer bestimmten Basisklasse beschränken, die über einen Standardkonstruktor verfügen oder die Verweis\- oder Werttypen sind. Benutzer des generischen Typs können keine Typargumente ersetzen, die die Einschränkungen nicht erfüllen.  
  
-   Eine *generische Methodendefinition* ist eine Methode mit zwei Parameterlisten: eine Liste der generischen Typparameter und eine Liste der formalen Parameter. Typparameter können als Rückgabetyp oder als Typen der formalen Parameter auftreten, wie im folgenden Code dargestellt.  
  
 [!code-cpp[Conceptual.Generics.Overview#4](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.generics.overview/cpp/source.cpp#4)]
 [!code-csharp[Conceptual.Generics.Overview#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.generics.overview/cs/source.cs#4)]
 [!code-vb[Conceptual.Generics.Overview#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.generics.overview/vb/source.vb#4)]  
  
 Generische Methoden können in generischen oder nicht generischen Typen stehen. Beachten Sie unbedingt, dass eine Methode nicht nur deshalb generisch ist, weil sie zu einem generischen Typ gehört oder weil sie formale Parameter besitzt, deren Typen die generischen Parameter des einschließenden Typs sind. Eine Methode ist nur generisch, wenn sie über eine eigene Liste an Typparametern verfügt. Im folgenden Code ist nur die Methode `G` generisch.  
  
 [!code-cpp[Conceptual.Generics.Overview#5](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.generics.overview/cpp/source.cpp#5)]
 [!code-csharp[Conceptual.Generics.Overview#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.generics.overview/cs/source.cs#5)]
 [!code-vb[Conceptual.Generics.Overview#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.generics.overview/vb/source.vb#5)]  
  
 [Zurück nach oben](#top)  
  
<a name="advantages_limitations"></a>   
## Vor\- und Nachteile von Generika  
 Es gibt viele Vorteile für die Verwendung von generischen Auflistungen und Delegaten:  
  
-   Typsicherheit. Generika übertragen die Last der Typsicherheit an den Compiler. Es ist nicht erforderlich, dass Sie Code schreiben, um auf den richtigen Datentyp hin zu testen, da dieser zum Zeitpunkt der Kompilierung erzwungen wird. Die Notwendigkeit einer Typumwandlung und die Möglichkeit von Laufzeitfehlern werden verringert.  
  
-   Es ist weniger Code erforderlich, und Code kann leichter wiederverwendet werden. Die Vererbung von einem Basistyp oder das Überschreiben von Membern ist nicht erforderlich.<xref:System.Collections.Generic.LinkedList%601> ist beispielsweise sofort einsatzbereit. So können Sie mit der folgenden Variablendeklaration eine verknüpfte Liste von Zeichenfolgen erstellen:  
  
     [!code-cpp[HowToGeneric#24](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/source2.cpp#24)]
     [!code-csharp[HowToGeneric#24](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/source2.cs#24)]
     [!code-vb[HowToGeneric#24](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/source2.vb#24)]  
  
-   Bessere Leistung. Generische Auflistungstypen bieten im Allgemeinen eine bessere Leistung zum Speichern und Bearbeiten von Werttypen, da das Boxing von Werttypen nicht erforderlich ist.  
  
-   Generische Delegaten ermöglichen typsichere Rückrufe, ohne mehrere Delegatklassen erstellen zu müssen. Der generische Delegat <xref:System.Predicate%601> ermöglicht es Ihnen beispielsweise, Ihre eigenen Suchkriterien für einen bestimmten Typ zu implementieren und Ihre Methode für Methoden vom Typ <xref:System.Array> zu verwenden, z. B. <xref:System.Array.Find%2A>, <xref:System.Array.FindLast%2A> und <xref:System.Array.FindAll%2A>.  
  
-   Generika optimieren dynamisch generierten Code. Wenn Sie Generika mit dynamisch generiertem Code verwenden, müssen Sie nicht den Typ generieren. Dies erhöht die Anzahl der Szenarios, in denen Sie einfache dynamische Methoden verwenden können, anstatt ganze Assemblys zu generieren. Weitere Informationen finden Sie unter "Gewusst wie: Definieren und Ausführen von dynamischen Methoden" und "DynamischeMethode".  
  
 Es folgen einige Einschränkungen von Generika:  
  
-   Generische Typen können von den meisten Basisklassen abgeleitet werden, z. B. <xref:System.MarshalByRefObject> \(und Einschränkungen können verwendet werden, um festzulegen, dass generische Typparameter von Basisklassen wie <xref:System.MarshalByRefObject> abgeleitet werden\).[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] unterstützt allerdings keine kontextgebundenen generischen Typen. Ein generischer Typ kann von <xref:System.ContextBoundObject> abgeleitet werden, aber wenn Sie versuchen, eine Instanz dieses Typs zu erstellen, wird eine <xref:System.TypeLoadException> ausgelöst.  
  
-   Enumerationen können keine generischen Typparameter haben. Eine Enumeration kann nur durch Zufall generisch sein \(z. B. weil sie in einem generischen Typ verschachtelt ist, der mit Visual Basic, C\# oder C\+\+ definiert wurde\). Weitere Informationen finden Sie unter "Enumerationen" in [Allgemeines Typsystem](../../../docs/standard/base-types/common-type-system.md).  
  
-   Einfache dynamische Methoden können nicht generisch sein.  
  
-   In Visual Basic, C\# und C\+\+ kann ein geschachtelter Typ, der in einem generischen Typ eingeschlossen ist, nicht instanziiert werden, es sei denn, die Typen wurden den Typparametern aller einschließenden Typen zugewiesen. Anders ausgedrückt: Ein geschachtelter Typ, der mit diesen Sprachen definiert wurde, enthält bei näherer Betrachtung die Typparameter aller einschließenden Typen. Dadurch können die Typparameter von einschließenden Typen in den Memberdefinitionen eines geschachtelten Typs verwendet werden. Weitere Informationen finden Sie unter "Geschachtelte Typen" in <xref:System.Type.MakeGenericType%2A>.  
  
    > [!NOTE]
    >  Ein geschachtelter Typ, der durch Ausgabe von Code in einer dynamischen Assembly oder durch Verwendung von [Ilasm.exe \(IL Assembler\)](../../../docs/framework/tools/ilasm-exe-il-assembler.md) definiert ist, ist nicht erforderlich, um die Typparameter seiner einschließenden Typen zu beinhalten; wenn sie jedoch nicht enthalten sind, befinden sich die Typparameter nicht im Gültigkeitsbereich der geschachtelten Klasse.  
  
     Weitere Informationen finden Sie unter "Geschachtelte Typen" in <xref:System.Type.MakeGenericType%2A>.  
  
 [Zurück nach oben](#top)  
  
<a name="class_library_and_language_support"></a>   
## Klassenbibliothek und Sprachunterstützung  
 .NET Framework bietet eine Reihe generischer Auflistungsklassen in den folgenden Namespaces:  
  
-   Der Namespace <xref:System.Collections.Generic> verzeichnet die meisten generischen Auflistungstypen, die von .NET Framework bereitgestellt werden, z. B. die generischen Klassen <xref:System.Collections.Generic.List%601> und <xref:System.Collections.Generic.Dictionary%602>.  
  
-   Der Namespace <xref:System.Collections.ObjectModel> verzeichnet zusätzliche generische Auflistungstypen, z. B. die generische Klasse <xref:System.Collections.ObjectModel.ReadOnlyCollection%601>, die zum Offenlegen von Objektmodellen für die Benutzer der Klasse nützlich sind.  
  
 Generische Schnittstellen für die Implementierung von Sortier\- und Übereinstimmungsvergleichen finden Sie im <xref:System>\-Namespace zusammen mit generischen Delegattypen für Ereignishandler, Konvertierungen und Suchprädikate.  
  
 Dem <xref:System.Reflection>\-Namespace wurde Unterstützung für Generika hinzugefügt, um generische Typen und generische Methoden zu überprüfen. Sie wurde auch <xref:System.Reflection.Emit> zum Ausgeben von dynamischen Assemblys mit generischen Typen und Methoden und <xref:System.CodeDom> zum Generieren von Quelldiagrammen mit Generika hinzugefügt.  
  
 Die Common Language Runtime bietet neue Opcodes und Präfixe für die Unterstützung generischer Typen in Microsoft Intermediate Language \(MSIL\), darunter <xref:System.Reflection.Emit.OpCodes.Stelem>, <xref:System.Reflection.Emit.OpCodes.Ldelem>, <xref:System.Reflection.Emit.OpCodes.Unbox_Any>, <xref:System.Reflection.Emit.OpCodes.Constrained> und <xref:System.Reflection.Emit.OpCodes.Readonly>.  
  
 Visual C\+\+, C\# und Visual Basic bieten alle vollständige Unterstützung für das Definieren und Verwenden von Generika. Weitere Informationen über die Sprachunterstützung finden Sie unter [Generische Typen in Visual Basic](../Topic/Generic%20Types%20in%20Visual%20Basic%20\(Visual%20Basic\).md), [Einführung in Generika](../Topic/Introduction%20to%20Generics%20\(C%23%20Programming%20Guide\).md) und [Overview of Generics in Visual C\+\+](../Topic/Overview%20of%20Generics%20in%20Visual%20C++.md).  
  
 [Zurück nach oben](#top)  
  
<a name="nested_types_and_generics"></a>   
## Geschachtelte Typen und Generika  
 Ein Typ, der in einem generischen Typ geschachtelt ist, kann von den Typparametern des einschließenden generischen Typs abhängen. Die Common Language Runtime betrachtet geschachtelte Typen als generisch, auch wenn sie keinen eigenen generischen Typparameter haben. Beim Erstellen einer Instanz eines geschachtelten Typs müssen Sie Typargumente für alle einschließenden generischen Typen festlegen.  
  
 [Zurück nach oben](#top)  
  
<a name="related_topics"></a>   
## Verwandte Themen  
  
|Titel|Beschreibung|  
|-----------|------------------|  
|[Generische Auflistungen in .NET Framework](../../../docs/standard/generics/collections.md)|Beschreibt generische Auflistungsklassen und andere generische Auflistungstypen in .NET Framework.|  
|[Generische Delegaten zum Bearbeiten von Arrays und Listen](../../../docs/standard/generics/delegates-for-manipulating-arrays-and-lists.md)|Beschreibt generische Delegate für Konvertierungen, Suchprädikate und Aktionen, die für Elemente eines Arrays oder einer Auflistung ausgeführt werden.|  
|[Generische Schnittstellen](../../../docs/standard/generics/interfaces.md)|Beschreibt generische Schnittstellen, die allgemeine Funktionalität für Familien generischer Typen bereitstellen.|  
|[Kovarianz und Kontravarianz](../../../docs/standard/generics/covariance-and-contravariance.md)|Beschreibt Kovarianz und Kontravarianz in generischen Typparametern.|  
|[Häufig verwendete Auflistungstypen](../../../docs/standard/collections/commonly-used-collection-types.md)|Enthält zusammenfassende Informationen über die Merkmale und Verwendungsszenarios der Auflistungstypen in .NET Framework, einschließlich generischer Typen.|  
|[Verwenden von generischen Auflistungen](../../../docs/standard/collections/when-to-use-generic-collections.md)|Beschreibt die allgemeinen Regeln, um festzulegen, wann generische Auflistungstypen verwendet werden können.|  
|[Gewusst wie: Definieren eines generischen Typs mit Reflektionsausgabe](../../../docs/framework/reflection-and-codedom/how-to-define-a-generic-type-with-reflection-emit.md)|Erläutert das Generieren dynamischer Assemblys, die generische Typen und Methoden enthalten.|  
|[Generische Typen in Visual Basic](../Topic/Generic%20Types%20in%20Visual%20Basic%20\(Visual%20Basic\).md)|Beschreibt die Generika\-Funktion für Visual Basic\-Benutzer, darunter Gewusst\-wie\-Themen zum Verwenden und Definieren generischer Typen.|  
|[Einführung in Generika](../Topic/Introduction%20to%20Generics%20\(C%23%20Programming%20Guide\).md)|Bietet eine Übersicht über das Definieren und Verwenden generischer Typen für C\#\-Benutzer.|  
|[Overview of Generics in Visual C\+\+](../Topic/Overview%20of%20Generics%20in%20Visual%20C++.md)|Beschreibt die Generika\-Funktion für C\+\+\-Benutzer, darunter die Unterschiede zwischen Generika und Vorlagen.|  
  
<a name="reference"></a>   
## Verweis  
 <xref:System.Collections.Generic>  
  
 <xref:System.Collections.ObjectModel>  
  
 <xref:System.Reflection.Emit.OpCodes?displayProperty=fullName>  
  
 [Zurück nach oben](#top)
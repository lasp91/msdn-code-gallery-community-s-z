# Simple project to import / export Excel data in visual basic with office.Interop
## Requires
- Visual Studio 2008
## License
- Apache License, Version 2.0
## Technologies
- Excel
## Topics
- Visual Basic .NET
## Updated
- 06/25/2013
## Description

<h1>Introduction</h1>
<p><span style="color:#0000ff; font-size:medium"><em>this is a simple project to connect Excel to visual basic</em></span></p>
<h1><span>Building the Sample</span></h1>
<p>&nbsp;</p>
<p><span style="font-size:20px; font-weight:bold">Description</span></p>
<p><span style="font-size:medium; color:#800080"><em>to connect your project to Excel you can use Oledb or office libraries included with visual basic</em></span></p>
<p><span style="font-size:medium; color:#800080"><em>this example show you how to import or export data from Excel using the library&nbsp;Microsoft.Office.Interop.Excel.dll</em></span></p>
<p>&nbsp;</p>
<p>I<span style="font-size:small; color:#000000">mports Microsoft.Office.Interop</span></p>
<p><span style="font-size:small; color:#000000">to imports this library</span></p>
<p><span style="font-size:small; color:#000000">click menu &quot;project&quot; -&gt; &quot;your project properties&quot; -&gt; references -&gt; add -&gt; browse'and add it,</span></p>
<p><span style="font-size:small; color:#000000">with 2007 office version and 2008 VS version this library is exist in this folder</span></p>
<p><span style="font-size:small; color:#000000">'C:\Program Files\Microsoft Visual Studio 9.0\Visual Studio Tools for Office\PIA\Office12'</span></p>
<p><span style="font-size:small; color:#000000">and select this library: Microsoft.Office.Interop.Excel.dll</span></p>
<p>&nbsp;</p>
<p><span style="font-size:small"><strong><span style="color:#000080">an important issue about globalization &amp; localization of this libraryyou might get a runtime error depending on user's culture (windows &amp; office language)</span></strong></span></p>
<p><span style="font-size:small"><strong><span style="color:#000080">Exception from HRESULT: 0x800A03EC.</span></strong></span></p>
<p><span style="font-size:small"><strong><span style="color:#000080">-or-</span></strong></span></p>
<p><span style="font-size:small"><strong><span style="color:#000080">Old format or invalid type library.</span></strong></span></p>
<p><span style="font-size:small"><strong><span style="color:#000080">to resolve this error add a culture info before calling Excel procedure, so your script will be as the below:</span></strong></span></p>
<p><span style="font-size:small"><strong><span style="color:#000080">&nbsp;</span></strong></span><br>
<span style="font-size:small; color:#000000">Dim thisThread As <a class="libraryLink" href="http://msdn.microsoft.com/en-US/library/System.Threading.Thread.aspx" target="_blank" title="Auto generated link to System.Threading.Thread">System.Threading.Thread</a> = _&nbsp; &nbsp; System.Threading.Thread.CurrentThreadDim originalCulture As _ <a class="libraryLink" href="http://msdn.microsoft.com/en-US/library/System.Globalization.CultureInfo.aspx" target="_blank" title="Auto generated link to System.Globalization.CultureInfo">System.Globalization.CultureInfo</a> = thisThread.CurrentCulture</span><br>
<span style="font-size:small; color:#000000">Try&nbsp;</span></p>
<p><span style="font-size:small; color:#000000">&nbsp; thisThread.CurrentCulture = New <a class="libraryLink" href="http://msdn.microsoft.com/en-US/library/System.Globalization.CultureInfo.aspx" target="_blank" title="Auto generated link to System.Globalization.CultureInfo">System.Globalization.CultureInfo</a>( &quot;en-US&quot;)</span><br>
<span style="font-size:small; color:#000000">ExportDGV_toExcel ()</span></p>
<p><span style="font-size:small; color:#000000">&nbsp;</span><br>
<span style="font-size:small; color:#000000">Finally&nbsp; &nbsp;</span></p>
<p><span style="font-size:small; color:#339966">' Restore the culture information for the thread after the Excel calls have completed.&nbsp; &nbsp;</span></p>
<p><span style="font-size:small; color:#000000">thisThread.CurrentCulture = originalCulture</span></p>
<p><span style="font-size:small; color:#000000">End Try&nbsp;</span></p>
<p><span style="font-size:small; color:#000000">&nbsp;</span><br>
<span style="font-size:small"><strong><span style="color:#000080">for full details please take a look at:</span></strong></span></p>
<p><span style="font-size:medium"><a title="http://msdn.microsoft.com/en-us/library/aa168494(office.11).aspx" href="http://msdn.microsoft.com/en-us/library/aa168494(office.11).aspx">http://msdn.microsoft.com/en-us/library/aa168494(office.11).aspx</a></span></p>
<p>==========</p>
<p><span style="font-size:small; color:#000000">Please note that it reads the first used lines in the Excel file, it won't read all empty lines</span></p>
<p>&nbsp;</p>
<p><span style="font-size:small; color:#000000">this example is only to give an idea about import and export data from/to an Excel file</span></p>
<p><span style="font-size:small; color:#000000">you should modify scripts to be consistent with your project</span></p>
<p><span style="font-size:small; color:#000000">I splited the scripts to multi functions to make ideas easiers&nbsp;</span></p>
<p>&nbsp;</p>
<p>this some scripts,</p>
<p>&nbsp; &nbsp;Private Sub ExportDGV_toExcel(ByVal _dgv As DataGridView)<br>
&nbsp; &nbsp; &nbsp; &nbsp; Dim ColCou As Byte<br>
&nbsp; &nbsp; &nbsp; &nbsp; Try&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</p>
<p>AppExcel.Visible = False</p>
<p>Book = AppExcel.Workbooks.Add()&nbsp; &nbsp;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; Sheet = Book.Sheets(1)&nbsp; &nbsp; &nbsp;</p>
<p>&nbsp; Catch ex As Exception<br>
&nbsp; &nbsp; &nbsp; &nbsp; End Try&nbsp; &nbsp;</p>
<p>&nbsp; &nbsp; Try<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; For _count As Short = 0 To _dgv.ColumnCount - 1&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; If _dgv.Columns(_count).Visible Then&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Sheet.Range(Chr(ColCou &#43; 65) &amp; &quot;1&quot;).Value = _dgv.Columns(_count).HeaderText 'first row&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ColCou &#43;= 1&nbsp; &nbsp; &nbsp;
 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; End If&nbsp; &nbsp;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; Next<br>
<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Dim RowDGV As Short&nbsp; &nbsp;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; For RowXls = 2 To _dgv.RowCount &#43; 1&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</p>
<p>&nbsp; &nbsp; ColCou = 0&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</p>
<p>&nbsp; &nbsp; For Col As Byte = 0 To _dgv.ColumnCount - 1&nbsp; &nbsp; &nbsp; &nbsp;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; If _dgv.Columns(Col).Visible Then</p>
<p><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; <a class="libraryLink" href="http://msdn.microsoft.com/en-US/library/System.Windows.Forms.Application.DoEvents.aspx" target="_blank" title="Auto generated link to System.Windows.Forms.Application.DoEvents">System.Windows.Forms.Application.DoEvents</a>()&nbsp; &nbsp; &nbsp; &nbsp;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Sheet.Range(Chr(ColCou &#43; 65) &amp; RowDGV &#43; 2).Value = _dgv.Item(Col, RowXls - 2).Value</p>
<p><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ColCou &#43;= 1&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</p>
<p>&nbsp; End If&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</p>
<p>&nbsp; Next&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</p>
<p>&nbsp; &nbsp; &nbsp; RowDGV &#43;= 1&nbsp; &nbsp; &nbsp;</p>
<p>&nbsp; &nbsp; &nbsp; Next<br>
SetupSheet:&nbsp; &nbsp; &nbsp;</p>
<p>&nbsp; &nbsp; &nbsp; ColCou = 0<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Try&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</p>
<p>&nbsp; &nbsp; &nbsp; Do While Not (Sheet.Range(Chr(ColCou &#43; 65) &amp; &quot;1&quot;).Value Is Nothing)&nbsp; &nbsp;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; With Sheet.Range(Chr(ColCou &#43; 65) &amp; &quot;1&quot;) 'first row&nbsp;&nbsp; &nbsp;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; .Font.Size = 14&nbsp; &nbsp; &nbsp; &nbsp;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; .Font.Bold = True&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; .Font.ColorIndex = 5 'blue --- 2: white, 3: red ... etc&nbsp; &nbsp; &nbsp; &nbsp;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ColCou &#43;= 1&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</p>
<p>&nbsp; End With&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</p>
<p>&nbsp; &nbsp; Loop<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Sheet.Columns.AutoFit()&nbsp; &nbsp; &nbsp; &nbsp;</p>
<p>&nbsp; &nbsp; Catch ex As Exception</p>
<p><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; End Try<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; AppExcel.Visible = True&nbsp; &nbsp;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; Exit Sub&nbsp; &nbsp; &nbsp;</p>
<p>&nbsp; Catch ex As Exception&nbsp; &nbsp;</p>
<p>&nbsp; &nbsp; End Try<br>
&nbsp; &nbsp; End Sub</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>Visual Basic</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">vb</span>

<div class="preview">
<pre class="vb">&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;ImportExcelSheetToDGV(<span class="visualBasic__keyword">ByVal</span>&nbsp;_dgvToImportTo&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;DataGridView,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;ColTotal&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Byte</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;ColIdx&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Byte</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;RowIdx,&nbsp;TotalLinesXls&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Short</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Try</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;DGV_import_export&nbsp;=&nbsp;<span class="visualBasic__keyword">New</span>&nbsp;DataGridView&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Book&nbsp;=&nbsp;AppExcel.Workbooks.Open(ExcelFileName)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sheet&nbsp;=&nbsp;Book.Sheets(<span class="visualBasic__number">1</span>)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Catch</span>&nbsp;ex&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;Exception&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Try</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Try</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">With</span>&nbsp;Sheet&nbsp;<span class="visualBasic__com">'calculate&nbsp;how&nbsp;many&nbsp;lines&nbsp;in&nbsp;the&nbsp;Excel&nbsp;file</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TotalLinesXls&nbsp;=&nbsp;<span class="visualBasic__number">2</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Do</span>&nbsp;<span class="visualBasic__keyword">While</span>&nbsp;Sheet.Range(<span class="visualBasic__string">&quot;A&quot;</span>&nbsp;&amp;&nbsp;Trim(TotalLinesXls.ToString)).Value.ToString&nbsp;&lt;&gt;&nbsp;<span class="visualBasic__string">&quot;&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<a class="libraryLink" href="http://msdn.microsoft.com/en-US/library/System.Windows.Forms.Application.DoEvents.aspx" target="_blank" title="Auto generated link to System.Windows.Forms.Application.DoEvents">System.Windows.Forms.Application.DoEvents</a>()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TotalLinesXls&nbsp;&#43;=&nbsp;<span class="visualBasic__number">1</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Loop</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">With</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Catch</span>&nbsp;ex&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;Exception&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Try</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TotalLinesXls&nbsp;-=&nbsp;<span class="visualBasic__number">1</span>&nbsp;
&nbsp;
StartImport:&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">With</span>&nbsp;DGV_import_export&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;PnlDGV.Controls.Add(DGV_import_export)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;ColHeader&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Char</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">For</span>&nbsp;ColCounter&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Byte</span>&nbsp;=&nbsp;<span class="visualBasic__number">1</span>&nbsp;<span class="visualBasic__keyword">To</span>&nbsp;ColTotal&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Add&nbsp;columns</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ColHeader&nbsp;=&nbsp;Chr(ColCounter&nbsp;&#43;&nbsp;<span class="visualBasic__number">64</span>).ToString.Trim&nbsp;<span class="visualBasic__com">'A,B,C,&nbsp;...</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.Columns.Add(<span class="visualBasic__string">&quot;&quot;</span>,&nbsp;Sheet.Range(ColHeader&nbsp;&amp;&nbsp;<span class="visualBasic__string">&quot;1&quot;</span>).Value)&nbsp;<span class="visualBasic__com">'A1.&nbsp;B1,&nbsp;C1,&nbsp;...</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Next</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;TotalLinesXls&nbsp;&lt;&nbsp;<span class="visualBasic__number">2</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MsgBox(<span class="visualBasic__string">&quot;no&nbsp;lines&nbsp;found&nbsp;in&nbsp;this&nbsp;Excel&nbsp;file&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">GoTo</span>&nbsp;EndMession&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Else</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.Rows.Add(TotalLinesXls&nbsp;-&nbsp;<span class="visualBasic__number">1</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.PerformLayout()&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;CellCou&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Integer</span>&nbsp;=&nbsp;<span class="visualBasic__number">1</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">For</span>&nbsp;RowIdx&nbsp;=&nbsp;<span class="visualBasic__number">2</span>&nbsp;<span class="visualBasic__keyword">To</span>&nbsp;TotalLinesXls&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;Read&nbsp;lines</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">For</span>&nbsp;ColIdx&nbsp;=&nbsp;<span class="visualBasic__number">1</span>&nbsp;<span class="visualBasic__keyword">To</span>&nbsp;ColTotal&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<a class="libraryLink" href="http://msdn.microsoft.com/en-US/library/System.Windows.Forms.Application.DoEvents.aspx" target="_blank" title="Auto generated link to System.Windows.Forms.Application.DoEvents">System.Windows.Forms.Application.DoEvents</a>()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;<span class="visualBasic__keyword">Not</span>&nbsp;(Sheet.Range(Chr(ColIdx&nbsp;&#43;&nbsp;<span class="visualBasic__number">64</span>)&nbsp;&amp;&nbsp;RowIdx).Value)&nbsp;<span class="visualBasic__keyword">Is</span>&nbsp;<span class="visualBasic__keyword">Nothing</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.Item(ColIdx&nbsp;-&nbsp;<span class="visualBasic__number">1</span>,&nbsp;RowIdx&nbsp;-&nbsp;<span class="visualBasic__number">2</span>).Value&nbsp;=&nbsp;Sheet.Range(Chr(ColIdx&nbsp;&#43;&nbsp;<span class="visualBasic__number">64</span>)&nbsp;&amp;&nbsp;RowIdx).Value.ToString&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;CellCou&nbsp;&#43;=&nbsp;<span class="visualBasic__number">1</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Next</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Next</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.Columns(.ColumnCount&nbsp;-&nbsp;<span class="visualBasic__number">1</span>).AutoSizeMode&nbsp;=&nbsp;DataGridViewAutoSizeColumnMode.Fill&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.Dock&nbsp;=&nbsp;DockStyle.Fill&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">With</span>&nbsp;
EndMession:&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Try</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AppExcel.Quit()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Catch</span>&nbsp;ex_error&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;Exception&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MsgBox(ex_error.Message)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Try</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span></pre>
</div>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>

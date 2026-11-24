# PDF

Instale los siguientes paquetes:
- QuestPDF
- Microsoft.Web.WebView2

![alt text](./img/paquetes_pdf.png)  

**QuestPDF** se usa para generar archivos PDF.  

**Microsoft.Web.WebView2** se usa para mostrar archivos PDF en **Windows Forms**.  

Descarga de íconos  

![alt text](./img/descarga_iconos.png)   


https://www.questpdf.com/quick-start.html

https://www.questpdf.com/api-reference/page/basics.html

```csharp
private void chkTodas_CheckedChanged(object sender, EventArgs e)
{
    if (chkTodas.Checked)
    {
        cboCategorias.Visible = false;
        label1.Visible = false;
    }
    else
    {
        cboCategorias.Visible = true;
        label1.Visible = true;
    }
}
```
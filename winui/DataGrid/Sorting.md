---
layout: post
title: Sorting | WinUI | DataGrid | Syncfusion
description: Learn here about column sorting support and its events with Syncfusion WinUI DataGrid (SfDataGrid) control and more details. 
platform: winui
control: DataGrid
documentation: ug
---


# Sorting with WinUI DataGrid (SfDataGrid)

DataGrid allows you to sort the data against one or more columns either in ascending or descending order. When sorting is applied, the rows are rearranged based on sort criteria. You can allow users to sort the data by touching or clicking the column header using [SfDataGrid.AllowSorting](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Grid.SfGridBase.html#Syncfusion_UI_Xaml_Grid_SfGridBase_AllowSorting) property to `true`.

{% tabs %}
{% highlight xaml %}
<syncfusion:SfDataGrid x:Name="sfDataGrid"
                       AllowSorting="True"
                       ItemsSource="{Binding Orders}"/>
{% endhighlight %}
{% highlight c# %}
sfDataGrid.AllowSorting = true;
{% endhighlight %}
{% endtabs %}

In another way, you can enable or disable the sorting for particular column by setting the [GridColumn.AllowSorting](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Grid.GridColumnBase.html#Syncfusion_UI_Xaml_Grid_GridColumnBase_AllowSorting) property.

{% tabs %}
{% highlight xaml %}
<syncfusion:SfDataGrid  x:Name="sfDataGrid"
                        AllowSorting="False"
                        AutoGenerateColumns="False"
                        ItemsSource="{Binding Orders}">
    <syncfusion:SfDataGrid.Columns>
        <syncfusion:GridTextColumn AllowSorting="True" MappingName="OrderID" />
        <syncfusion:GridTextColumn AllowSorting="False" MappingName="CustomerID" />
        <syncfusion:GridTextColumn AllowSorting="False" MappingName="CustomerName" />
        <syncfusion:GridTextColumn AllowSorting="True" MappingName="ShipCity" />
        <syncfusion:GridTextColumn AllowSorting="True" MappingName="Country" />
    </syncfusion:SfDataGrid.Columns>

</syncfusion:SfDataGrid>
{% endhighlight %}
{% highlight c# %}
this.sfDataGrid.Columns["OrderID"].AllowSorting = true;
this.sfDataGrid.Columns["CustomerID"].AllowSorting = false;
{% endhighlight %}
{% endtabs %}


N> The [GridColumn.AllowSorting](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Grid.GridColumnBase.html#Syncfusion_UI_Xaml_Grid_GridColumnBase_AllowSorting) takes higher priority than [SfDataGrid.AllowSorting](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Grid.SfGridBase.html#Syncfusion_UI_Xaml_Grid_SfGridBase_AllowSorting) property.

End users can sort the column by clicking column header cell. Once the columns get sorted, the sort indicator will be displayed on the right side of the column header.

![Sorting for WinUI DataGrid](Sorting-images/Sorting-image1.png)


## Sort column in double click

By default, column gets sorted when column header clicked. You can change this behavior to sort the column in double click action by setting [SfDataGrid.SortClickAction](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.DataGrid.SortClickAction.html) property to `DoubleClick`.

{% tabs %}
{% highlight xaml %}
<syncfusion:SfDataGrid  x:Name="sfDataGrid"
                        AllowSorting="True"
                        AutoGenerateColumns="True"
                        ItemsSource="{Binding Orders}"
                        SortClickAction="DoubleClick" />
{% endhighlight %}
{% highlight c# %}
this.sfDataGrid.SortClickAction = SortClickAction.DoubleClick;
{% endhighlight %}
{% endtabs %}

## Sorting order

By default, the data is sorted in ascending or descending order when clicking column header. You can rearrange the data to its initial order from descending, when clicking column header by setting [SfDataGrid.AllowTriStateSorting](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Grid.SfGridBase.html#Syncfusion_UI_Xaml_Grid_SfGridBase_AllowTriStateSorting) property.

Following are the sequence of sorting orders when clicking column header,
 
* Sorts the data in ascending order

* Sorts the data in descending order
 
* Clears the sorting and records displayed in its initial order

## Multi column sorting

SfDataGrid control allows you sort more than one column, where sorting is applied one column against other columns. 

To apply sorting on multiple columns, user have to click the column header by pressing the <kbd>Ctrl</kbd> key.

In the below screen shot, the OrderID column sorted. Then the `CustomerName` column is sorted against the `OrderID` data by clicking column header by pressing &lt;kbd&gt;Ctrl&lt;/kbd&gt; key. The sorting state of `OrderID` column is preserved and `CustomerName` column sorted against `OrderID` column.  

![Multi column sorting for WinUI DataGrid](Sorting-images/Sorting-image2.png)

### Display sort order
It is also possible to display sorted order of columns in header by setting [SfDataGrid.ShowSortNumbers](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Grid.SfGridBase.html#Syncfusion_UI_Xaml_Grid_SfGridBase_ShowSortNumbers) property to `true`. 
{% tabs %}
{% highlight xaml %}
<syncfusion:SfDataGrid  x:Name="sfDataGrid"
                        AllowSorting="True"        
                        ShowSortNumbers="True"
                        ItemsSource="{Binding Orders}" />
{% endhighlight %}
{% highlight c# %}
this.sfDataGrid.ShowSortNumbers = true;
{% endhighlight %}
{% endtabs %}

![Sorting orders for WinUI DataGrid](Sorting-images/Sorting-image3.png)

## Programmatic sorting

You can sort the data programmatically by adding or removing the [SortColumnDescription](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.DataGrid.SortColumnDescription.html) in [SfDataGrid.SortColumnDescriptions](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.DataGrid.SortColumnDescriptions.html) property.
 
N> [SfDataGrid.SortColumnsChanging](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.DataGrid.SfDataGrid.html#Syncfusion_UI_Xaml_DataGrid_SfDataGrid_SortColumnsChanging) and [SfDataGrid.SortColumnsChanged](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.DataGrid.SfDataGrid.html#Syncfusion_UI_Xaml_DataGrid_SfDataGrid_SortColumnsChanged) events are not raised when the data sorted programmatically through `SfDataGrid.SortColumnDescriptions`.

### Adding sort columns

{% tabs %}
{% highlight xaml %}
<syncfusion:SfDataGrid  x:Name="sfDataGrid"
                        AutoGenerateColumns="True"
                        ItemsSource="{Binding Orders}">
    <syncfusion:SfDataGrid.SortColumnDescriptions>
        <syncfusion:SortColumnDescription ColumnName="OrderID" SortDirection="Ascending" />
        <syncfusion:SortColumnDescription ColumnName="CustomerName" SortDirection="Descending" />
    </syncfusion:SfDataGrid.SortColumnDescriptions>

</syncfusion:SfDataGrid>
{% endhighlight %}
{% highlight c# %}
this.sfDataGrid.SortColumnDescriptions.Add(new SortColumnDescription() { ColumnName = "OrderID", SortDirection = SortDirection.Ascending });
this.sfDataGrid.SortColumnDescriptions.Add(new SortColumnDescription() { ColumnName = "CustomerName", SortDirection = SortDirection.Descending });
{% endhighlight %}
{% endtabs %}

### Removing sort columns

You can unsort the data by removing the corresponding `SortColumnDescription` from the [SfDataGrid.SortColumnDescriptions](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.DataGrid.SortColumnDescriptions.html) property.

{% tabs %}
{% highlight c# %}
var sortColumnDescription = this.sfDataGrid.SortColumnDescriptions.FirstOrDefault(col => col.ColumnName == "OrderID");

if (sortColumnDescription != null)
{
    this.sfDataGrid.SortColumnDescriptions.Remove(sortColumnDescription);
}
{% endhighlight %}
{% endtabs %}

### Clear sorting

You can clear sorting, by clearing the [SfDataGrid.SortColumnDescriptions](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.DataGrid.SortColumnDescriptions.html).

{% tabs %}
{% highlight c# %}
this.sfDataGrid.SortColumnDescriptions.Clear();
{% endhighlight %}
{% endtabs %}

## Custom sorting

SfDataGrid allows you to sort the columns based on the custom logic. The custom sorting can be applied by adding the [SortComparer](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Data.SortComparer.html) instance to [SfDataGrid.SortComparers](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.DataGrid.SfDataGrid.html#Syncfusion_UI_Xaml_DataGrid_SfDataGrid_SortComparers).
 
The [SortComparer](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Data.SortComparer.html) have the following properties,

[PropertyName](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Data.SortComparer.html#Syncfusion_UI_Xaml_Data_SortComparer_PropertyName) - Gets or sets the name of the column to apply custom sorting.

[Comparer](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Data.SortComparer.html#Syncfusion_UI_Xaml_Data_SortComparer_Comparer) - Gets or sets the custom comparer in which you can code to compare the data using custom logic.

You can implement [ISortDirection](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Data.ISortDirection.html) interface in comparer to get the sort direction. So you can apply different custom logics for ascending and descending.
 
Follow the below steps to add custom comparer to sort using custom logic,

#### Define custom comparer with custom sort logic

In the below code snippet, CustomerName property is compared based on its string length, instead of default string comparison.
  
{% tabs %}
{% highlight c# %}
public class CustomComparer : IComparer<object>, ISortDirection
{
    private SortDirection _SortDirection;

    /// <summary>
    /// Gets or sets the property that denotes the sort direction.
    /// </summary>
    /// <remarks>
    /// SortDirection gets updated only when sorting the groups. For other cases, SortDirection is always ascending.
    /// </remarks>

    public SortDirection SortDirection
    {
        get { return _SortDirection; }
        set { _SortDirection = value; }
    }

    public int Compare(object x, object y)
    {
        int nameX;
        int nameY;

        //While data object passed to comparer

        if (x.GetType() == typeof(OrderInfo))
        {
            nameX = ((OrderInfo)x).CustomerName.Length;
            nameY = ((OrderInfo)y).CustomerName.Length;
        }

        //While sorting groups

        else if (x.GetType() == typeof(Group))
        {

            //Calculating the group key length
            nameX = ((Group)x).Key.ToString().Length;
            nameY = ((Group)y).Key.ToString().Length;
        }

        else
        {
            nameX = x.ToString().Length;
            nameY = y.ToString().Length;
        }

        //returns the comparison result based in SortDirection.

        if (nameX.CompareTo(nameY) > 0)
            return SortDirection == SortDirection.Ascending ? 1 : -1;

        else if (nameX.CompareTo(nameY) == -1)
            return SortDirection == SortDirection.Ascending ? -1 : 1;

        else
            return 0;
    }
}

{% endhighlight %}
{% endtabs %}

#### Adding custom comparer to SfDataGrid

Custom comparer can be added to [SfDataGrid.SortComparers](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.DataGrid.SfDataGrid.html#Syncfusion_UI_Xaml_DataGrid_SfDataGrid_SortComparers) property. `SortComparers` maintains custom comparers and the custom comparer gets called when corresponding column gets sorted by clicking column header or programmatically.
 
{% tabs %}
{% highlight xaml %}
xmlns:Linq="using:Syncfusion.UI.Xaml.Data"

<Page.Resources>
    <local:CustomComparer x:Key="comparer" />
</Page.Resources>

<syncfusion:SfDataGrid x:Name="sfDataGrid" ItemsSource="{Binding Orders}">
    <syncfusion:SfDataGrid.SortComparers>
        <Linq:SortComparer Comparer="{StaticResource comparer}" PropertyName="CustomerName" />
    </syncfusion:SfDataGrid.SortComparers>
    <syncfusion:SfDataGrid.SortColumnDescriptions>
        <syncfusion:SortColumnDescription ColumnName="CustomerName" SortDirection="Ascending" />
    </syncfusion:SfDataGrid.SortColumnDescriptions>
</syncfusion:SfDataGrid>
{% endhighlight %}
{% highlight c# %}
this.sfDataGrid.SortComparers.Add(new SortComparer() { Comparer = new CustomComparer(), PropertyName = "CustomerName" });
{% endhighlight %}
{% endtabs %}

Sorting `CustomerName` column sorts the data using custom comparer available in `SfDataGrid.SortComparers`.

![Custom sorting for WinUI DataGrid](Sorting-images/Sorting-image4.png)

## Sorting the underlying collection 

SfDataGrid sorts the records in UI and maintains in its internal CollectionView and it will not change the order of data in underlying collection. You can get sorted data from `SfDataGrid.View.Records` when groups are not in place and `SfDataGrid.View.TopLevelGroup.DisplayElements` when grouping in place.
 
If you want to sort the underlying collection when sorting takes place, then this can be achieved by handling [SfDataGrid.SortColumnsChanged](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.DataGrid.SfDataGrid.html#Syncfusion_UI_Xaml_DataGrid_SfDataGrid_SortColumnsChanged) event.
 
{% tabs %}
{% highlight c# %}
this.sfDataGrid.SortColumnsChanged += SfDataGrid_SortColumnsChanged;                         

private void SfDataGrid_SortColumnsChanged(object sender, GridSortColumnsChangedEventArgs e)
{
    var viewModel = this.DataContext as ViewModel;
    IEnumerable<OrderInfo> OrderedSource = viewModel.Orders;

    foreach (var sortColumn in this.sfDataGrid.View.SortDescriptions)
    {
        var columnName = sortColumn.PropertyName;

        if (sortColumn.Direction == SortDirection.Ascending)
            OrderedSource = OrderedSource.OrderBy(source => GetOrderSource(source, columnName));

        else
            OrderedSource = OrderedSource.OrderByDescending(source => GetOrderSource(source, columnName));
    }
}

using System.Reflection;

private object GetOrderSource(OrderInfo source, string name)
{
    var propInfo = source.GetType().GetRuntimeProperty(name);

    if (propInfo != null)

        // Get the current sort column value
        return propInfo.GetValue(source);

    return null;
}

{% endhighlight %}
{% endtabs %}

## Handling events

### SortColumnsChanging event

[SfDataGrid.SortColumnsChanging](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.DataGrid.SfDataGrid.html#Syncfusion_UI_Xaml_DataGrid_SfDataGrid_SortColumnsChanging) event occurs while sorting the columns by clicking column header. [GridSortColumnsChangingEventArgs](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.DataGrid.GridSortColumnsChangingEventArgs.html) has following members which provides information for `SortColumnsChanging` event.

[Action](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.DataGrid.GridSortColumnsChangingEventArgs.html#Syncfusion_UI_Xaml_DataGrid_GridSortColumnsChangingEventArgs_Action) – Gets the action triggered this event.
 
[Cancel](https://msdn.microsoft.com/query/dev10.query?appId=Dev10IDEF1&l=EN-US&k=k(System.ComponentModel.CancelEventArgs.Cancel)&rd=true) – Setting value to `true`, cancels the triggered action.
 
[AddedItems](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.DataGrid.GridSortColumnsChangingEventArgs.html#Syncfusion_UI_Xaml_DataGrid_GridSortColumnsChangingEventArgs_AddedItems) - Gets the list of new `SortColumnDescription’s` that are added.

[RemovedItems](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.DataGrid.GridSortColumnsChangingEventArgs.html#Syncfusion_UI_Xaml_DataGrid_GridSortColumnsChangingEventArgs_RemovedItems) - Gets the list of `SortColumnDescription’s` that are removed.
 
[CancelScroll](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.DataGrid.GridSortColumnsChangingEventArgs.html#Syncfusion_UI_Xaml_DataGrid_GridSortColumnsChangingEventArgs_CancelScroll) - Gets or sets a value that indicates, whether scroll and bring SelectedItem in view after sorting takes place.

You can prevent sorting for the particular column through [GridSortColumnsChangingEventArgs.Cancel](https://msdn.microsoft.com/query/dev10.query?appId=Dev10IDEF1&l=EN-US&k=k(System.ComponentModel.CancelEventArgs.Cancel)&rd=true) property of `SortColumnsChanging` event.

{% tabs %}
{% highlight c# %}
this.sfDataGrid.SortColumnsChanging += SfDataGrid_SortColumnsChanging;

private void SfDataGrid_SortColumnsChanging(object sender, GridSortColumnsChangingEventArgs e)
{
    if (e.AddedItems[0].ColumnName == "OrderID")
    {
        e.Cancel = true;
    }
}

{% endhighlight %}
{% endtabs %}

### SortColumnsChanged event

[SfDataGrid.SortColumnsChanged](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.DataGrid.SfDataGrid.html#Syncfusion_UI_Xaml_DataGrid_SfDataGrid_SortColumnsChanged) event occurs when the sorting is applied to the column. [GridSortColumnsChangedEventArgs](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.DataGrid.GridSortColumnsChangedEventArgs.html) provides information for `SortColumnsChanged` event.

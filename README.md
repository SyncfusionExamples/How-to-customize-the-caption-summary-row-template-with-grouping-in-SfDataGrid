# How to customize the caption summary row template with grouping in SfDataGrid
In this article, we will show you how to customize the caption summary row template with grouping in [.Net Maui DataGrid](https://www.syncfusion.com/maui-controls/maui-datagrid).

## xaml
The code below demonstrates how to customize the caption summary row template with grouping in DataGrid.
```
 <ContentPage.BindingContext>
    <local:EmployeeViewModel x:Name="viewModel" />
</ContentPage.BindingContext>

<ContentPage.Resources>
    <ResourceDictionary>
        <local:GroupCaptionConverter x:Key="SummaryConverter" />
    </ResourceDictionary>
</ContentPage.Resources>

<syncfusion:SfDataGrid x:Name="dataGrid"
                       Margin="10"
                       GridLinesVisibility="Both"
                       HeaderGridLinesVisibility="Both"
                       ColumnWidthMode="Auto"
                       AllowGroupExpandCollapse="True"
                       GroupingMode="Single"
                       AutoGenerateColumnsMode="None"
                       ItemsSource="{Binding Employees}">

    <syncfusion:SfDataGrid.GroupColumnDescriptions>
        <syncfusion:GroupColumnDescription ColumnName="Salary" />
    </syncfusion:SfDataGrid.GroupColumnDescriptions>

    <syncfusion:SfDataGrid.CaptionSummaryTemplate>
        <DataTemplate>
            <StackLayout Orientation="Horizontal">
                <Label Text="{Binding Converter={StaticResource SummaryConverter}, ConverterParameter = {x:Reference dataGrid} }"
                       FontSize="Default"
                       VerticalTextAlignment="Center"
                       HorizontalTextAlignment="Start"
                       LineBreakMode="NoWrap"
                       HorizontalOptions="FillAndExpand"
                       VerticalOptions="FillAndExpand">
                    <Label.Style>
                        <Style TargetType="Label">
                            <Setter Property="FontAttributes"
                                    Value="Bold, Italic" />
                            <Setter Property="TextColor"
                                    Value="Orange" />
                        </Style>
                    </Label.Style>
                </Label>
            </StackLayout>
        </DataTemplate>
    </syncfusion:SfDataGrid.CaptionSummaryTemplate>
    <syncfusion:SfDataGrid.CaptionSummaryRow>
        <syncfusion:DataGridSummaryRow Name="CaptionSummary"
                                       ShowSummaryInRow="True"
                                       Title="Total Salary: {CaptionSummary}">
            <syncfusion:DataGridSummaryRow.SummaryColumns>
                <syncfusion:DataGridSummaryColumn Name="CaptionSummary"
                                                  Format="{}{Sum:C0}"
                                                  MappingName="Salary"
                                                  SummaryType="DoubleAggregate" />
            </syncfusion:DataGridSummaryRow.SummaryColumns>
        </syncfusion:DataGridSummaryRow>
    </syncfusion:SfDataGrid.CaptionSummaryRow>

    <syncfusion:SfDataGrid.Columns>
        <syncfusion:DataGridNumericColumn MappingName="EmployeeID"
                                          Format="#"
                                          HeaderText="Employee ID" />
        <syncfusion:DataGridTextColumn MappingName="Name"
                                       HeaderText="Employee Name" />
        <syncfusion:DataGridTextColumn MappingName="Title"
                                       HeaderText="Designation" />
        <syncfusion:DataGridNumericColumn MappingName="Salary"
                                          HeaderText="Salary" />

    </syncfusion:SfDataGrid.Columns>

</syncfusion:SfDataGrid>
``` 

## C#
```
public class GroupCaptionConverter : IValueConverter
{
    public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
    {
        var data = value != null ? value as Group : null;
        if (data != null)
        {
            SfDataGrid dataGrid = (SfDataGrid)parameter;
            var summaryText = SummaryCreator.GetSummaryDisplayTextForRow((value as Group).SummaryDetails, dataGrid.View);

            return summaryText;
        }
        return null;
    }
    public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture)
    {
        return null;
    }
}
```

 ![CaptionRowTemplate.png](https://support.syncfusion.com/kb/agent/attachment/inline?token=eyJhbGciOiJodHRwOi8vd3d3LnczLm9yZy8yMDAxLzA0L3htbGRzaWctbW9yZSNobWFjLXNoYTI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjMzNTcyIiwib3JnaWQiOiIzIiwiaXNzIjoic3VwcG9ydC5zeW5jZnVzaW9uLmNvbSJ9.W74uVefc2xbsWd2e_b1rMh6CoUIupQpMoFVYVYDuXC4)

[View sample in GitHub](https://github.com/SyncfusionExamples/How-to-customize-the-caption-summary-row-template-with-grouping-in-SfDataGrid)

Take a moment to explore this [documentation](https://help.syncfusion.com/maui/datagrid/overview), where you can find more information about Syncfusion .NET MAUI DataGrid (SfDataGrid) with code examples. Please refer to this [link](https://www.syncfusion.com/maui-controls/maui-datagrid) to learn about the essential features of Syncfusion .NET MAUI DataGrid (SfDataGrid).
 
##### Conclusion
 
I hope you enjoyed learning about how to customize the caption summary row template with grouping in .NET MAUI DataGrid (SfDataGrid).
 
You can refer to our [.NET MAUI DataGrid’s feature tour](https://www.syncfusion.com/maui-controls/maui-datagrid) page to learn about its other groundbreaking feature representations. You can also explore our [.NET MAUI DataGrid Documentation](https://help.syncfusion.com/maui/datagrid/getting-started) to understand how to present and manipulate data. 
For current customers, you can check out our .NET MAUI components on the [License and Downloads](https://www.syncfusion.com/sales/teamlicense) page. If you are new to Syncfusion, you can try our 30-day [free trial](https://www.syncfusion.com/downloads/maui) to explore our .NET MAUI DataGrid and other .NET MAUI components.
 
If you have any queries or require clarifications, please let us know in the comments below. You can also contact us through our [support forums](https://www.syncfusion.com/forums), [Direct-Trac](https://support.syncfusion.com/create) or [feedback portal](https://www.syncfusion.com/feedback/maui?control=sfdatagrid), or the feedback portal. We are always happy to assist you!
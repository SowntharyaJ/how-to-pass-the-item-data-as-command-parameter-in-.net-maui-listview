# how-to-pass-the-item-data-as-command-parameter-in-.net-maui-listview

This repository contains a sample demonstrating how to  pass the item data as command parameter in ItemTappedCommand in .NET MAUI ListView (SfListView).

## Sample

```xaml
<ContentPage.Resources>
    <ResourceDictionary>
        <local:CustomConverter x:Key="EventArgs" />
    </ResourceDictionary>
</ContentPage.Resources>

<listView:SfListView
    x:Name="listView"
    GroupHeaderSize="50"
    IsStickyGroupHeader="True"
    IsStickyHeader="True"
    ItemSize="70"
    ItemSpacing="0,0,5,0"
    ItemsSource="{Binding contactsinfo}"
    SelectionMode="Multiple"
    TapCommand="{Binding}">
    <listView:SfListView.Behaviors>
        <local:EventToCommandBehavior
            Command="{Binding TapCommand}"
            Converter="{StaticResource EventArgs}"
            EventName="ItemTapped" />
    </listView:SfListView.Behaviors>

    <!--  ItemTemplate  -->
    <listView:SfListView.ItemTemplate>
        <DataTemplate>
            <ViewCell>
                <ViewCell.View>
                    <Grid x:Name="grid" RowSpacing="1">
                        <Grid.RowDefinitions>
                            <RowDefinition Height="*" />
                            <RowDefinition Height="1" />
                        </Grid.RowDefinitions>
                        <Grid RowSpacing="1">
                            <Grid.ColumnDefinitions>
                                <ColumnDefinition Width="50" />
                                <ColumnDefinition Width="*" />
                                <ColumnDefinition Width="70" />
                            </Grid.ColumnDefinitions>

                            <Image
                                HeightRequest="50"
                                HorizontalOptions="Center"
                                Source="{Binding ContactImage}"
                                VerticalOptions="Center" />

                            <Grid
                                Grid.Column="1"
                                Padding="10,0,0,0"
                                RowSpacing="1"
                                VerticalOptions="Center">
                                <Grid.RowDefinitions>
                                    <RowDefinition Height="*" />
                                    <RowDefinition Height="*" />
                                </Grid.RowDefinitions>

                                <Label
                                    LineBreakMode="NoWrap"
                                    Text="{Binding ContactName}"
                                    TextColor="#474747" />
                                <Label
                                    Grid.Row="1"
                                    Grid.Column="0"
                                    LineBreakMode="NoWrap"
                                    Text="{Binding ContactNumber}"
                                    TextColor="#474747" />
                            </Grid>
                            <Grid
                                Grid.Row="0"
                                Grid.Column="2"
                                Padding="0,10,10,0"
                                HorizontalOptions="End"
                                RowSpacing="0">
                                <Label
                                    LineBreakMode="NoWrap"
                                    Text="{Binding ContactType}"
                                    TextColor="#474747" />
                            </Grid>
                        </Grid>
                    </Grid>
                </ViewCell.View>
            </ViewCell>
        </DataTemplate>
    </listView:SfListView.ItemTemplate>
</listView:SfListView>
```

```c#
public class CustomConverter : IValueConverter
{
    public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
    {
        object eventArgs = null;
        Syncfusion.Maui.ListView.ItemTappedEventArgs eventArg = null;
        if (value is Syncfusion.Maui.ListView.ItemTappedEventArgs)
        {
            eventArg = value as Syncfusion.Maui.ListView.ItemTappedEventArgs;
            eventArgs = eventArg.DataItem;
        }
        
        return eventArgs;
    }
}
```

## Requirements to run the demo

* [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) or [Visual Studio for Mac](https://visualstudio.microsoft.com/vs/mac/)
* Xamarin add-ons for Visual Studio (available via the Visual Studio installer).

## Troubleshooting

### Path too long exception

If you are facing path too long exception when building this example project, close Visual Studio and rename the repository to short and build the project.

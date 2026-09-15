# How to pass the item data as command parameter in ItemTapped command in .NET MAUI ListView?

In [.NET MAUI ListView (SfListView)](https://help.syncfusion.com/maui/listview/getting-started), data items can be passed to the `ViewModel` using the `EventsToCommand` behavior to adhere to the MVVM pattern.

This article demonstrates how to pass item data as a command parameter in the [ItemTapped](https://help.syncfusion.com/maui/listview/working-with-sflistview#tapped-event) command.

**C#**
``` 
 public class ContactsViewModel
 {
     Command<object> tapCommand;
       
     public Command<object> TapCommand
      {
         get { return tapCommand; }
         protected set { tapCommand = value; }
      }
 
     public ContactsViewModel()
      {
         tapCommand = new Command<object>(OnTapped);
      }
 
     public void OnTapped(object obj)
      {
         var name = (obj as Contacts).ContactName ;
         var alert = Application.Current.MainPage.DisplayAlert("Parameter Passed","Name:" + name,"Cancel");
      }
 
 }
 ```

Associate the command with the appropriate event of `SfListView` using behaviors.

**Xaml**
```
 
<listView:SfListView x:Name="listView">
        <listView:SfListView.Behaviors>
          <local:EventToCommandBehavior EventName="ItemTapped" 
                                        Command="{Binding TapCommand}"
                                        Converter="{StaticResource EventArgs}" />
        </listView:SfListView.Behaviors>
</listView:SfListView>
 ```
 

Create a `CustomConverter` to extract `ItemData` from `ItemTappedEventArgs`.

**C#**
```
public class CustomConverter : IValueConverter
    {
        public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
        {
            object eventArgs = null;
            Syncfusion.Maui.ListView.ItemTappedEventArgs eventArg = null;
            if (value is Syncfusion.ListView.XForms.ItemTappedEventArgs)
            {
                eventArg = value as Syncfusion.Maui.ListView.ItemTappedEventArgs;
                eventArgs = eventArg.DataItem;
            }
           
            return eventArgs;
        }
 
        public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture)
        {
            throw new NotImplementedException();
        }
    }
 
```

When a `ListViewItem` is tapped, the `ItemData` is returned from `CustomConverter` to the command in the `ViewModel`, enabling the desired operation to be performed.

**Output**

![image.png](https://support.syncfusion.com/kb/attachment/article/15545/inline?token=eyJhbGciOiJodHRwOi8vd3d3LnczLm9yZy8yMDAxLzA0L3htbGRzaWctbW9yZSNobWFjLXNoYTI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjE5NzMwIiwib3JnaWQiOiIzIiwiaXNzIjoic3VwcG9ydC5zeW5jZnVzaW9uLmNvbSJ9.a9fl80lMrbcAyy3MDr1yPouNa8CTQRmrh42gBxqomyA)


**Conclusion:**

I hope you enjoyed learning how to pass the item data as a command parameter in the `ItemTapped` command.

You can refer to our [.NET MAUI ListView](https://www.syncfusion.com/maui-controls/maui-listView) feature tour page to know about its other groundbreaking feature representations and [documentation](https://help.syncfusion.com/maui/listview/getting-started), and how to quickly get started with configuration specifications. 

You can check out our components from the [License and Downloads](https://www.syncfusion.com/sales/teamlicense) page for current customers. If you are new to Syncfusion®, try our 30-day [free trial](https://www.syncfusion.com/downloads/maui) to check out our other controls.

Please let us know in the comments section below if you have any queries or require clarification. You can also contact us through our [support forums](https://www.syncfusion.com/forums/), [Direct-Trac](https://support.syncfusion.com/create), or [feedback portal](https://www.syncfusion.com/feedback/maui?control=sflistview). We are always happy to assist you!

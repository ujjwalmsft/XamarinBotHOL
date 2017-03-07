# Challenge 1: Quality Control
If you finished Mission 2, you would realize there's a problem with the `ListView` on Android: the messages cut off if they are too long.

The issue here is that the default `TextCell` in the ListView will cut off text that is too long by default.

```xml
<ListView x:Name="MessageListView"
                VerticalOptions="StartAndExpand"
                HorizontalOptions="Fill"
                >
        <ListView.ItemTemplate>
                <DataTemplate>
                <TextCell Text="{Binding Text}" Detail="{Binding Sender}" />
                </DataTemplate>
        </ListView.ItemTemplate>
</ListView>
```

As a result, we will need to use a custom cell instead for the template.

You can look at how to define a custom cell in XML here:
https://developer.xamarin.com/guides/xamarin-forms/user-interface/listview/customizing-cell-appearance/

You'll also need to configure the `ListView` to allow uneven rows.

## Finishing Requirements
At the end of this challenge, the cells in the `ListView` should be flexible and adapt its size according to the contents,
therefore allowing for longer messages to be displayed.
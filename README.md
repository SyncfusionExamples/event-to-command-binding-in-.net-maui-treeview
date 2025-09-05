# event-to-command-binding-in-.net-maui-treeview
This repository demonstrates how to convert events to commands in the .NET MAUI TreeView (SfTreeView) control using Behaviors. It provides a sample implementation that enables event handling through data binding, allowing you to respond to TreeView events in the ViewModel using commands for a clean MVVM architecture.

## Sample

### XAML

```xaml
<ContentPage.BindingContext>
    <local:FileManagerViewModel x:Name="viewModel"/>
</ContentPage.BindingContext>

<ContentPage.Content>
    <Grid>
        <syncfusion:SfTreeView x:Name="treeView"
                               ItemTemplateContextType="Item"
                               ItemsSource="{Binding ImageNodeInfo}"
                               ChildPropertyName="SubFiles"             
                               AutoExpandMode="RootNodesExpanded">
            <syncfusion:SfTreeView.Behaviors >
                <local:EventToCommand EventName="SelectionChanged" Command="{Binding SelectionChangedCommand}"/>
            </syncfusion:SfTreeView.Behaviors>

        </syncfusion:SfTreeView>
    </Grid>
</ContentPage.Content>
```

### View Model

```csharp
public class FileManagerViewModel
{
    #region Fields
    private Command<object> selectionChangedCommand;
    #endregion

    #region Constructor

    public FileManagerViewModel()
    {
        SelectionChangedCommand = new Command<object>(OnSelectionChanged);
    }

    private void OnSelectionChanged(object obj)
        {
            App.Current.MainPage.DisplayAlert("Alert", ((obj as ItemSelectionChangedEventArgs).AddedItems[0] as FileManager).ItemName + " is selected", "OK");
        }
    #endregion

    #region Properties
    public Command<object> SelectionChangedCommand
    {
        get { return selectionChangedCommand; }
        set { selectionChangedCommand = value; }
    }
    #endregion
}
```

## Requirements to run the demo

To run the demo, refer to [System Requirements for .NET MAUI](https://help.syncfusion.com/maui/system-requirements).

Make sure that you have the compatible versions of [Visual Studio 2022](https://visualstudio.microsoft.com/downloads/ ) with the Dot NET MAUI workload and [.NET Core SDK 7.0](https://dotnet.microsoft.com/en-us/download/dotnet/7.0) or later version in your machine before starting to work on this project.

## Troubleshooting:
### Path too long exception

If you are facing path too long exception when building this example project, close Visual Studio and rename the repository to short and build the project.

## License

Syncfusion® has no liability for any damage or consequence that may arise from using or viewing the samples. The samples are for demonstrative purposes. If you choose to use or access the samples, you agree to not hold Syncfusion® liable, in any form, for any damage related to use, for accessing, or viewing the samples. By accessing, viewing, or seeing the samples, you acknowledge and agree Syncfusion®'s samples will not allow you seek injunctive relief in any form for any claim related to the sample. If you do not agree to this, do not view, access, utilize, or otherwise do anything with Syncfusion®'s samples.